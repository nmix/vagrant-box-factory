# Vagrant Box Factory

Фабрика образов виртуальных машин Vagrant

## Подготовка

Перед созданием окружения необходимо установить следующие пакеты: *virtualbox, vagrant, ansible*


```bash
# virtualbox
sudo apt install virtualbox

# Загружаем deb-пакет со страницы https://www.vagrantup.com/downloads.html
# и устанавливаем его
sudo dpkg -i vagrant_X_Y_Z.deb

# ansible
sudo apt-get install software-properties-common
sudo apt-add-repository --yes --update ppa:ansible/ansible
sudo apt-get install ansible
```


## Создание образов

```bash
git clone http://gitlab.isoit.ru/zoid/vagrant-box-factory.git
cd vagrant-box-factory
```

### ubuntu-server-18.04-docker

Виртуальная машина с предустановленными *docker* и *docker-compose*

```bash
# запуск виртуальной машины
VAGRANT_VAGRANTFILE=Vagrantfile.u18-docker vagrant up
# пакетирование машины в файл образа
VAGRANT_VAGRANTFILE=Vagrantfile.u18-docker vagrant package --output ubuntu-server-18.04-docker.box
# добавление файла образа в систему
vagrant box add ubuntu-server-18.04-docker ubuntu-server-18.04-docker.box
# отображение образов системы
vagrant box list
```

Использование образа:

```bash
vagrant init -m ubuntu-server-18.04-docker
```

```ruby
Vagrant.configure("2") do |config|
  # ...
  config.vm.box = "ubuntu-server-18.04-docker"
end
```

### ubuntu-server-18.04-rails-5.1

Виртуальная машина с предустановленными *ruby-2.5.1, rails-5.1.5, postgres 10, redis*

Параметры подключения к *postgres*:
host **localhost**, 
port **5432**,
username **dbuser**,
password: **dbpassword**.

Параметры подключения к *redis*:
port **6379**

```bash
# запуск виртуальной машины
VAGRANT_VAGRANTFILE=Vagrantfile.u18-rails-5.1 vagrant up
# пакетирование машины в файл образа
VAGRANT_VAGRANTFILE=Vagrantfile.u18-rails-5.1 vagrant package --output ubuntu-server-18.04-rails-5.1.box
# добавление файла образа в систему
vagrant box add ubuntu-server-18.04-rails-5.1 ubuntu-server-18.04-rails-5.1.box
# отображение образов системы
vagrant box list
```

Использование образа:

```bash
vagrant init -m ubuntu-server-18.04-rails-5.1
```

```ruby
# Vagrantfile
Vagrant.configure("2") do |config|
  # ...
  config.vm.box = "ubuntu-server-18.04-rails-5.1"
end
```