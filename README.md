# dominikzogg/vagrant-virtualbox-ansible

**important**: the host machine, does not need ansible support, all ansible scripts get managed by the client machine.

## Features

 * Debian 8
 * Nginx 1.8
 * MariaDB 10.0
 * PHP 5.6
 * NodeJS 0.12

## Installation

### virtualbox

Download the newest virtualbox version supported by vagrant.

https://www.virtualbox.org/wiki/Downloads

### vagrant

Download the newest vagrant version.

https://www.vagrantup.com/downloads.html

### vagrant plugin

`vagrant plugin install vagrant-hostmanager`

### operating systems specific

#### linux

##### nfs support

`sudo apt-get install nfs-kernel-server`

#### windows

##### nfs support

`vagrant plugin install vagrant-winnfsd`

##### git / ssh client

https://msysgit.github.io

Windows got no ssh or git support out of the box, by installing git from `msysgit.github.io` you get ssh and a git
support on a easy way.

### vagrant-virtualbox-ansible

#### as a git submodule

##### install

```{.sh}
git submodule add -b v1 https://github.com/dominikzogg/vagrant-virtualbox-ansible.git
git submodule update --init
```

##### usage

```{.sh}
git submodule update --init
git submodule update --remote
```

#### as a copy of the project

```{.sh}
git clone https://github.com/dominikzogg/vagrant-virtualbox-ansible.git
cd vagrant-virtualbox-ansible
git checkout -b v1
rm -r .git
```

## Configuration

### vagrant.yml (within your project dir)

```{.yml}
---
hostname: 'projectname.dev'
application: 'default'
```

#### supported application

 * contao
 * default (no rewrite)
 * drupal
 * lavarel
 * symfony
 * wordpress

### Suspend the virtual machines on host logout or shutdown

#### linux

Add the following lines to `/etc/default/virtualbox` and add every user, which uses virtualboxm whitespace separated.

```{.sh}
SHUTDOWN_USERS="foo bar"
SHUTDOWN=savestate
```

#### macosx

Copy the script:

`tools/vagrant-suspend` to `/usr/local/bin/vagrant-suspend`

Register the logout hook:

`sudo defaults write com.apple.loginwindow LogoutHook /usr/local/bin/vagrant-suspend`

#### windows

There should be a python solution for windows, but i have no expirience with it.

http://blog.ionelmc.ro/2014/01/04/virtualbox-vm-auto-shutdown

## Applications

 * [symfony][1]

## Run

The vagrant setup is in a subdir, which means you need to go there, and call all vagrant commands from there.

```{.sh}
cd vagrant-virtualbox-ansible
vagrant up
vagrant halt
vagrant suspend
vagrant resume
vagrant provision
vagrant ssh
```

[1]: doc/symfony.md