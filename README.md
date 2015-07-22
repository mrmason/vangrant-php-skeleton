# Vagrant Puppet Install

## Requirements

This repository has a Vagrant VM configuration baked in.

You'll to install:

* Vagrant
* Virtualbox

Then, put this repo somewhere appropriate, perhaps in a `vagrantvms` directory on your computer. 


## Configuration
You may customise the server for your application using the clearly marked "configurable properties" in the following files:

- `/Vagrantfile` - IPs and settings
- `/manifests/default.pp` - site URLs for vhosts


### What it does
Creates a virtual machine running a basic LAMP stack. In addition to the standard LAMP installation, we:

- Create a database and user, as per the settings in `/manifests/default.pp`
- Install Composer globally;
- Set the correct ownership for the whole dir

### What it doesn't do

Modify your `/etc/hosts` file. You'll need to add your chosen development domain, as follows:

~~~~~
# /etc/hosts
192.168.56.107	krys.dev
~~~~~

This is the URL you set in `/manifests/default.pp`

### Accessing the site via a browser
Assuming you've added the appropriate entry to your `/etc/hosts` file, you can access your site at `http://krys.dev`.

### Accessing the database

#### Via phpMyAdmin in the browser

To install, you'll need to run a quick shell command to get phpMyAdmin accessible in your browser:

	vagrant ssh
	echo 'Include /etc/phpmyadmin/apache.conf' | sudo tee -a /etc/apache2/apache2.conf
	exit
	vagrant reload

Then, visit http://krys.dev/phpmyadmin, to access it.

#### Using Sequel Pro
You can connect to the database using Sequel Pro (or an equivalent piece of software) using the following settings:

- _Connection Type_: `SSH`
- _MySQL Host_: `127.0.0.1`
- _Username_: `root`
- _Password_: `root`
- _Database_: ``
- _Port_: `3306`
- _SSH Host_: `192.168.56.107` (corresponds with the IP set in the `Vagrantfile`)
- _SSH User_: `vagrant`
- _SSH Key_: `~/.vagrant.d/insecure_private_key`
- _SSH Port_: ``

### Accessing the server via SSH
`cd` to the directory comtaining this repo and run `vagrant ssh`.