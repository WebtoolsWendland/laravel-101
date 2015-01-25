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

## Troubleshooting

By default, NFS won't work on Windows. I suggest deleting the  NFS block so Vagrant defaults back to its default file sync behavior.

However, you can also try the "vagrant-winnfsd" plugin. Just run `vagrant plugin install vagrant-winnfsd` to try it out!

## References

* [Vaprobash](https://github.com/fideloper/Vaprobash)
* [Laracast on Vagrant](https://laracasts.com/search?q=vagrant&q-where=lessons)
