# Setup Your Environment

## Pre-requirement

The following tool is needed for our training, please install:

1. [VirtualBox]()
2. [Vagrant](https://www.vagrantup.com/downloads.html)
3. [Node.js](http://nodejs.org/)

> Note: Should install each package by order.

## Installation

### 1. Install Orchestra Platform

	$ composer create-project orchestra/platform basecamp dev-master ---prefer-dist -vvv --profile

#### 2. Install Vaprobash

Follow the instruction from <https://github.com/fideloper/Vaprobash#instructions>, e.g:

	$ curl -L http://bit.ly/vaprobash > Vagrantfile

Once you have `Vagrantfile` inside the root directory of `basecamp`.

##### 2.1. Setup hostname

Change the value of `hostname` to be relevant to your project. E.g:	

```ruby
hostname = "basecamp.app"
```

##### 2.2. Setup Server IP

Change the value of `server_ip` which is not currently used. E.g:

```ruby
server_ip = "192.168.210.10"
```

##### 2.3. Setup Public Directory

Change the value of `public_folder` to Orchestra Platform 3 public folder, by default this would be based on `public` directory:

```ruby
public_folder = '/vagrant/public'
```

##### 2.4. Change VM Name

(Optional) but you should be able to set a customise name for your VM:

```ruby
	# If using VirtualBox
	config.vm.provider :virtualbox do |vb|
	
		vb.name = 'Basecamp'
```

##### 2.5 Setup Base Packages

Now, it's time to customise the set of packages to be provisioned on the VM. For this course we will be using:

* Nginx
* PHP 5.6
* MariaDB
* Redis
* Beanstalkd
* Supervisord
* Node.js
* Composer
* Mailcatcher
* Setup local provision
 
##### 2.6 Setup Local Provision

Create a new `vagrant.sh` file:

```bash
#!/usr/bin/env bash

/usr/bin/mysql -uroot -proot -e "CREATE DATABASE IF NOT EXISTS basecamp DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;"

cd /vagrant/
composer install --prefer-dist --dev
```

## Troubleshooting

By default, NFS won't work on Windows. I suggest deleting the  NFS block so Vagrant defaults back to its default file sync behavior.

However, you can also try the "vagrant-winnfsd" plugin. Just run `vagrant plugin install vagrant-winnfsd` to try it out!

## Alternative Tools

* [Homestead](http://laravel.com/docs/4.2/homestead)
* [PuPHPet](https://puphpet.com/)

## References

* [Vaprobash](https://github.com/fideloper/Vaprobash)
* [Laracast on Vagrant](https://laracasts.com/search?q=vagrant&q-where=lessons)
