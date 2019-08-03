# Vagrant Box Factory

Фабрика образов виртуальных машин Vagrant


## ubuntu-server-18.04-docker

Виртуальная машина с предустановленными *docker* и *docker-compose*. Образ на [vagrant cloud](https://app.vagrantup.com/zoid/boxes/ubuntu-server-18.04-docker)

### Быстрый старт

```bash
vagrant init zoid/ubuntu-server-18.04-docker --box-version 0.1
vagrant up
```

Vagrantfile
```ruby
Vagrant.configure("2") do |config|
  config.vm.box = "zoid/ubuntu-server-18.04-docker"
  config.vm.box_version = "0.1"
end
```

### Сборка образа

```bash
git clone http://gitlab.isoit.ru/zoid/vagrant-box-factory.git
cd vagrant-box-factory
# пакетирование машины в файл образа
VAGRANT_VAGRANTFILE=Vagrantfile.u18-docker vagrant package --output ubuntu-server-18.04-docker.box
# добавление файла образа в систему
vagrant box add ubuntu-server-18.04-docker ubuntu-server-18.04-docker.box
# инициализация Vagrantfile
vagrant init -m ubuntu-server-18.04-docker
# запуск
vagrant up
```

## ubuntu-server-18.04-rails5

Виртуальная машина для проектов ruby-on-rails 5

> Учитывая, что комбинаций версий окружения может быть великое множество, рекомендуется собирать образ под конкретный проект, предварительно скорректировав версии в файле playbooks/u18-rails5.yml

Окружение по-умолчанию:
ruby-2.6.1,
rails-5.1.7,
postgres-10.9
node-12.7
yarn-1.17.3
redis-4.0.9

Параметры подключения к *postgres*:
host **localhost**, 
port **5432**,
username **dbuser**,
password: **dbpassword**.

Параметры подключения к *redis*:
port **6379**


### Сборка образа

```bash
git clone http://gitlab.isoit.ru/zoid/vagrant-box-factory.git
cd vagrant-box-factory
```

Корректируем версии окружения в файле *playbooks/u18-rails5.yml*

```bash
# пакетирование машины в файл образа
VAGRANT_VAGRANTFILE=Vagrantfile.u18-rails5 vagrant package --output my-project-environment.box
# добавление файла образа в систему
vagrant box add my-project-environment my-project-environment.box
vagrant init -m my-project-environment
```

```ruby
# Vagrantfile
Vagrant.configure("2") do |config|
  # ...
  config.vm.box = "my-project-environment"
end
```
