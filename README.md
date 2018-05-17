# DevVm
Setup linux vm for development

## Preconditions
* Vagrant installed
* Virtualbox installed
* Git installed

You should always use the latest version.

**Warning**

The Version of VirtualBox-Guest-Additions is currently hard coded in Vagrantfile. When you update Virtualbox you have to change 
the value in Vagrantfile.

## Step by step guide
* Clone repository to your favourite location
* Run `vagrant up`
* Wait until your VM is provisioned
* Start development

## Vagrant Cheatsheet
* Install existing Vagrantbox from [Vagrant-Repo](https://app.vagrantup.com/boxes/search): `vagrant init <box-name>`
* Add an existing box to Vagrant: `vagrant box add <box-name>`
* Start provisioning: `vagrant up`
* Connect to machine: `vagrant ssh`

For further information look the Vagrant [Getting-Started-Guide](https://www.vagrantup.com/intro/getting-started/)
