# Setup Your Environment

## Pre-requirement

The following tool is needed for our training, please install:

1. [VirtualBox]()
2. [Vagrant](https://www.vagrantup.com/downloads.html)
3. [Node.js](http://nodejs.org/)

> Note: Should install each package by order.

## Installation

### 1. Install Orchestra Platform

`composer create-project orchestra/platform basecamp dev-master ---prefer-dist -vvv --profile`

#### 2. Install Vaprobash

Follow the instruction from <https://github.com/fideloper/Vaprobash#instructions>, e.g:

	$ curl -L http://bit.ly/vaprobash > Vagrantfile



## Troubleshooting

By default, NFS won't work on Windows. I suggest deleting the NFS block so Vagrant defaults back to its default file sync behavior.

However, you can also try the "vagrant-winnfsd" plugin. Just run `vagrant plugin install vagrant-winnfsd` to try it out!

## References

* [Vaprobash](https://github.com/fideloper/Vaprobash)
* [Laracast on Vagrant](https://laracasts.com/search?q=vagrant&q-where=lessons)
