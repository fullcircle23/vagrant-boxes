Basic Vagrant box for running and testing Catapult Service Bootstrap on VirtualBox VM

Pre-requisites:
- Vagrant
- VirtualBox (preferably 5.2.22)
- VirtualBox Extension Pack (must be the same version)

Additionally, for Windows:
- PuTTY and PuTTYGen (SSH client and a generator for security keys)

This vagrant box includes the following:
- Ubuntu 18.04
- Docker
- Docker Compose
- Git
- catapult-service-bootstrap

Installation Steps:

$ cd {your gitlab root directory}
		
e.g. cd ~/GitLab

$ git clone git@172.16.18.111:nemmy/vagrant-boxes.git

$ cd ./vagrant-boxes/catapult-ubuntu

$ vagrant box add catapult-ubuntu catapult-ubuntu.box

$ vagrant box list
catapult-ubuntu     (virtualbox, 0)

$ cd {your virtual machines directory}

e.g. cd ~/vms

$ mkdir catapult-ubuntu-001

$ cd catapult-ubuntu-001

Copy the Vagrantfile from your local repo to here
$ cp {your gitlab root directory}/vagrant-boxes/catapult-ubuntu/Vagrantfile .

e.g. cp ~/GitLab/vagrant-boxes/catapult-ubuntu/Vagrantfile .

You may need to update the following variables if you're on Windows host machine
 MAC_USER - use your Host username
 HOST_PATH - ensure folder path is valid on the Host OS
 GUEST_PATH - this path is on the Guest OS, you need not change it

Power up the vm
$ vagrant up

Login to the vm (for non Windows host)
$ vagrant ssh

Login to the vm (for Windows host)
The problem we face now is that Windows doesn’t come with an SSH command line client. 
This means the built-in SSH functions of Vagrant won’t necessarily work for us Windows users. 
But that’s why we have PuTTY. Type this to get your SSH info whenever you need it:

$ vagrant ssh-config

It will tell you the IP and SSH port to use and a few other bits of info in case you forget.
Open PuTTY, enter the IP and port, give the connection a name, and save it. 
You can now connect to the new server over SSH with PuTTY. 
The username is “vagrant” and the password should be “vagrant” as well.

$ ls -l
total 4
drwxrwxr-x 9 vagrant vagrant 4096 Jan  9 11:12 catapult-service-bootstrap
drwxr-xr-x 1 vagrant vagrant  160 Jan 10 07:32 catapult-ubuntu-001

After ls command, you should see 2 directories:
	(i) catapult-service-bootstrap (already cloned from GitHub)
	(ii) catapult-ubuntu-001 (synced to same directory on your host machine)

You can now run the Catapult Service Bootstrap as per the steps in 
NEM Developer Center - Setting up your workstation
https://nemtech.github.io/getting-started/setup-workstation.html

$ cd catapult-service-bootstrap
$ docker-compose up

Check first block
$ curl localhost:3000/block/1

docker-compose up had already been executed once during this vm creation hence this vm comes with some blocks already added.
However, you may reset this doing ./clean-data
You may proceed with the rest of the steps starting from 
Creating a test account to complete 'Setting up your workstation'

Please log issues in this project for any problems. 
Thank you.






