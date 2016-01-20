[![Build Status](https://travis-ci.org/nerdstein/security-vm.svg?branch=master)](https://travis-ci.org/nerdstein/security-vm)

Security VM is A VM for web development security tools, built with Vagrant + Ansible.

This project aims to put together a suite of tools that web developers can use to enhance
the security of a site you are developing. Please note - most of these tools are intended
to run on a non-production system.

It will install the following optional tools on an Ubuntu 14.04 (by default) linux VM:

  - nmap
  - w3af
  - nodejs packages (configurable)
  - composer packages (configurable)

## Customizing the VM

There is one configuration file where you can customize the VM for your needs:

  - `config.yml`: Contains variables like the VM domain name and IP address, packages, and features.


## Quick Start Guide

### 1 - Install dependencies (VirtualBox and Vagrant)

  1. Download and install [VirtualBox](https://www.virtualbox.org/wiki/Downloads) (Security VM also works with Parallels or VMware, if you have the [Vagrant VMware integration plugin](http://www.vagrantup.com/vmware)).
  2. Download and install [Vagrant](http://www.vagrantup.com/downloads.html).

Note for Faster Provisioning (Mac/Linux only): *[Install Ansible](http://docs.ansible.com/intro_installation.html) on your host machine, so Security VM can run the provisioning steps locally instead of inside the VM.*

Note for Linux users: *If NFS is not already installed on your host, you will need to install it to use the default NFS synced folder configuration. See guides for [Debian/Ubuntu](https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nfs-mount-on-ubuntu-14-04), [Arch](https://wiki.archlinux.org/index.php/NFS#Installation), and [RHEL/CentOS](https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nfs-mount-on-centos-6).*

Note on versions: *Please make sure you're running the latest stable version of Vagrant, VirtualBox, and Ansible, as the current version of Security VM is tested with the latest releases. As of August 2015: Vagrant 1.8.0, VirtualBox 5.0.12, and Ansible 2.0.0.*

### 2 - Build the Virtual Machine

  1. Download this project and put it wherever you want.
  2. Copy the `example.config.yml` to `config.yml` files, and modify to your liking.
  3. Create local directories for all synced directories in `config.yml` (`local_path`, inside `vagrant_synced_folders`).
  4. Open Terminal, cd to this directory (containing the `Vagrantfile` and this README file).
  5. (If you have Ansible installed on Mac/Linux) Run `$ sudo ansible-galaxy install -r provisioning/requirements.yml --force`.
  6. Type in `vagrant up`, and let Vagrant do its magic.

Note: *If there are any errors during the course of running `vagrant up`, and it drops you back to your command prompt, just run `vagrant provision` to continue building the VM from where you left off. If there are still errors after doing this a few times, post an issue to this project's issue queue on GitHub with the error.*

### 3 - Configure your host machine to access the VM.

Please note, the configuration below can change based on your settings found in config.yml. The defaults are referenced below.

  1. [Edit your hosts file](http://www.rackspace.com/knowledge_center/article/how-do-i-modify-my-hosts-file), adding the line `192.168.88.88  securityvm.dev` so you can connect to the VM.
    - You can have Vagrant automatically configure your hosts file if you install the `hostsupdater` plugin (`vagrant plugin install vagrant-hostsupdater`). All hosts defined in `apache_vhosts` or `nginx_hosts` will be automatically managed.
    - You can also have Vagrant automatically assign an available IP address to your VM if you install the `auto_network` plugin (`vagrant plugin install vagrant-auto_network`), and set `vagrant_ip` to `0.0.0.0` inside `config.yml`.
  2. Open your browser and access [http://securityvm.dev/](http://securityvm.dev/).

## Features

By default, this VM includes optional features listed in the `config.yml` option `installed_extras`:

    installed_extras:
      - nmap
      - w3af

If you don't want or need one or more of these extras, just delete them or comment them from the list. This is helpful if you want to conserve system resources.

## Other Notes

  - To shut down the virtual machine, enter `vagrant halt` in the Terminal in the same folder that has the `Vagrantfile`. To destroy it completely (if you want to save a little disk space, or want to rebuild it from scratch with `vagrant up` again), type in `vagrant destroy`.
  - Find out more about local development with Vagrant + VirtualBox + Ansible in this presentation: [Local Development Environments - Vagrant, VirtualBox and Ansible](http://www.slideshare.net/geerlingguy/local-development-on-virtual-machines-vagrant-virtualbox-and-ansible).
  - Learn about how Ansible can accelerate your ability to innovate and manage your infrastructure by reading [Ansible for DevOps](http://www.ansiblefordevops.com/).

## License

This project is licensed under the MIT open source license.

## About the Author

[Adam Bergstein](http://nerdstein.net/). Architecture borrowed from [Drupal VM](www.drupal-vm.com). This project, and others like it, are inspired by Jeff Geerling's book, [Ansible for DevOps](http://www.ansiblefordevops.com/).
