# packer-nginx64
Vagrant VirtualBox box with Nginx64

*Based on : https://github.com/Galser/packer-ubuntu*

# Purpose 

This repository attempts to have minimal amount of code that is required to create an Ubuntu Bionic Beaver 64it box  with Nginx64 installed, using Packer for running in VirtualBox with management by Vagrant.

# Prerequisites

You will need to have some Git tools , Vagrant, VirtualBox and Packer installed.
Fore refernce where to get them and how to install please check sections [Required tools](requiredtools) below

# How to use

# Required tools

1. To download the content of this repository you will need **git command-line tools**(recommended) or **Git UI Client**. To install official command-line Git tools please [find here instructions](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) for various operation systems. 
2. This box for virtualizaion uses **VirtualBox**, download the binaries for your [platform here](https://www.virtualbox.org/wiki/Downloads) and then follow [instructions for installation](https://www.virtualbox.org/manual/ch02.html)
3. For managing of VM (virtual machines) we are going to use **Vagrant**. To install **Vagrant** , please follow instructions here : [official Vargant installation manual](https://www.vagrantup.com/docs/installation/)
4. For creating base box image from scratch we need **Packer** - an open source tool for creating identical machine images for multiple platforms from a single source configuration.  You can [download binaries for your platform here](https://www.packer.io/downloads.html)  and then [follow this installation instruction](https://www.packer.io/intro/getting-started/install.html#precompiled-binaries).  In our case Packer is going to take care of installing OS into VM, communicating with it, doing basic provision and preparing for us packed Vagrant box, ready to use.


# TODO

- [ ] build first box
- [ ] make separate install script for Nginx
- [ ] create Vagrant template to run the box
- [ ] test box
- [ ] update readme with last-minute instructions

# DONE

- [X] create inital readme
- [x] get required ISO links and checksums
- [x] create Packer template

