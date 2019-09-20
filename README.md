# packer-nginx64
Vagrant VirtualBox box with Nginx64

*Based on : https://github.com/Galser/packer-ubuntu*

# Purpose 

This repository attempts to have minimal amount of code that is required to create an Ubuntu Bionic Beaver 64it box  with Nginx64 installed, using Packer for running in VirtualBox with management by Vagrant.

# Prerequisites

You will need to have some Git tools , Vagrant, VirtualBox and Packer installed.
For reference where to get them and how to install please check sections [Required tools](requiredtools) below

# How to use

- To download the copy of the code (*clone* in Git terminology) - go to the location of your choice (normally some place in home folder) and run in terminal:
 ```
 git clone https://github.com/Galser/packer-nginx64.git
 ```
 *in case you are using alternative Git Client - please follow appropriate instruction for it and download(*clone*) [this repo](https://github.com/Galser/packer-nginx64.git).*

- Previous step should create the folder that contains copy of repository. Default name is going to be the same as the name of repository e.g. `packer-nginx64`. Locate and open it.
 ```
 cd packer-nginx64
 ```
- Now to create the Vagrant base box we are going to use Packer and [template](templates.json) with [provision scripts](scripts) provided in this repo.
*Note: It is going to take some time, as Packer need to download the full ISO image of the operating system, run it, make installation and all required adjustments and then pack everything into format suitable for consuming by Vagrant running with VirtualBox*
 ```
 packer template-nginx64.json
 ```

 In case of successful process completion you would see these lines :
 ```
 ==> Builds finished. The artifacts of successful builds are:
 --> nginx64-vbox: VM files in directory: output-nginx64-vbox
 --> nginx64-vbox: 'virtualbox' provider box: nginx64-vbox.box
 ```
 Now you should have file `ngxin64-vbox.box` in the current folder. This is you Vagrant box with Nginx installed in Ubuntu  Bionic Beaver 64Bit. Congratulations! 

 Further, we going to do some *complimentary steps* to test the box. 

 First we need  to initialize Vagrant with our fresh box, bring it up  , check and later destroy to free resources.

- We need to let know Vagrant about our new box - e.g. add it. 
 ```
 vagrant box add --name nginx64 nginx64-vbox.box
 ```

 Output should look like : 
 ```
    ==> box: Box file was not detected as metadata. Adding it directly...
    ==> box: Adding box 'nginx64' (v0) for provider: 
        box: Unpacking necessary files from: file:///Users/andrii/labs/skills/packer-nginx64/nginx64-vbox.box
    ==> box: Successfully added box 'nginx64' (v0) for 'virtualbox'! 
 ```
 
- Now we can initialize our Vagrant environment. This will create **Vagrantfile** in the current folder with all the required settings to run this base box. 
 ```
 vagrant init nginx64
 ```
 
- To create and provision virtual machine with Vagrant - execute from command line :
 ```
 vagrant up
 ```
 ( *This will utilize settings from previous step - from Vagrantfile* )

- At this point VM already up and running , so you can use SSH client to connect to it. For example for Linux and MacOS - execute from command-line : 
 ```
 vagrant ssh
 ```
 You should see Basic Ubuntu greeting at first line , something like this : 
 ```
 Welcome to Ubuntu 18.04.3 LTS (GNU/Linux 4.15.0-55-generic x86_64)
 ```

- Let's check that Nginx indeed running  - at first we can check with the systemd init system to make sure the service is  running by typing:
 ```
 systemctl status nginx
 ```
 Output :
 ```
 ● nginx.service - A high performance web server and a reverse proxy server
    Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
    Active: active (running) since Fri 2019-09-20 13:47:14 UTC; 5min ago
      Docs: man:nginx(8)
   Process: 404 ExecStart=/usr/sbin/nginx -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
   Process: 324 ExecStartPre=/usr/sbin/nginx -t -q -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
  Main PID: 413 (nginx)
     Tasks: 2 (limit: 525)
    CGroup: /system.slice/nginx.service
            ├─413 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
            └─419 nginx: worker proces
 ```
 As you can see above, the service appears to have started successfully. However, the real way to test is to actually request a page from Nginx.
 Let's do it by getting the actual page served by Nginx on localhost :
 ```
 curl http://localhost:80
 ```
 And the start of output will be :
 ```
 <!DOCTYPE html>
 <html>
 <head>
 <title>Welcome to nginx!</title>
 <style>
     body {
         width: 35em;
         margin: 0 auto;
         font-family: Tahoma, Verdana, Arial, sans-serif;
     }
 </style>
 </head>
 <body>
 <h1>Welcome to nginx!</h1>
 <p>If you see this page, the nginx web server is successfully installed and
 working. Further configuration is required.</p>
 ```
 So - Nginx is up, running and serving pages, in this case - Nginx default Welcome page

- When you've done with the tests and don't need VM anymore - you should exit the SSH session - by executing in command line :
  ```
  exit
  ```

- Now - to completely destroy the VM and free up all your system resource (CPU, memory)  - execute from command line :
  ```
  vagrant destroy
  ``` 
  Next you should see the question on a new line :
  ```
  default: Are you sure you want to destroy the 'default' VM? [y/N]
  ```
  Answer `y` from keyboard, and you are good to go

# Required tools

1. To download the content of this repository you will need **git command-line tools**(recommended) or **Git UI Client**. To install official command-line Git tools please [find here instructions](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) for various operation systems. 
2. This box for virtualizaion uses **VirtualBox**, download the binaries for your [platform here](https://www.virtualbox.org/wiki/Downloads) and then follow [instructions for installation](https://www.virtualbox.org/manual/ch02.html)
3. For managing of VM (virtual machines) we are going to use **Vagrant**. To install **Vagrant** , please follow instructions here : [official Vargant installation manual](https://www.vagrantup.com/docs/installation/)
4. For creating base box image from scratch we need **Packer** - an open source tool for creating identical machine images for multiple platforms from a single source configuration.  You can [download binaries for your platform here](https://www.packer.io/downloads.html)  and then [follow this installation instruction](https://www.packer.io/intro/getting-started/install.html#precompiled-binaries).  In our case Packer is going to take care of installing OS into VM, communicating with it, doing basic provision and preparing for us packed Vagrant box, ready to use.


# TODO


# DONE

- [X] create initial readme
- [x] get required ISO links and checksums
- [x] create Packer template
- [X] build first box
- [x] make separate install script for Nginx
- [x] create Vagrant template to run the box
- [x] test box
- [x] update readme with last-minute instructions
