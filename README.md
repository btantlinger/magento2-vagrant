# Vagrant for Magento2

Vagrant Setup for Magento 2 install.  All prerequisites setup and running. 

Installs all requisites for Magento 2.1.x  Utilizes Ubuntu 14.04. 

You can reference the Magento2 installation guide [here.](http://devdocs.magento.com/guides/v2.1/install-gde/bk-install-guide.html)

## Prerequisites
### Virtualbox
[VirtualBox](https://www.virtualbox.org/) is an open source virtualizer, an application that can run an entire operating system within its own virtual machine. 

1. Download the installer for your laptop operating system using the links below.
    * [VirtualBox for Windows Hosts](http://download.virtualbox.org/virtualbox/4.3.18/VirtualBox-4.3.18-96516-Win.exe)
    * [VirtualBox for OS X hosts](http://download.virtualbox.org/virtualbox/4.3.18/VirtualBox-4.3.18-96516-OSX.dmg)
    * [VirtualBox for Linux hosts](https://www.virtualbox.org/wiki/Linux_Downloads) (requires that you pick your distro)
1. Run the installer, choosing all of the default options.
    * Windows: Grant the installer access every time you receive a security prompt.
    * Mac: Enter your admin password.
    * Linux: Enter your root password if prompted.
1. Reboot your laptop if prompted to do so when installation completes.
1. Close the VirtualBox window if it pops up at the end of the install.

### Vagrant
[Vagrant](https://www.vagrantup.com/) is an open source command line utility for managing reproducible developer environments. 

1. Download the installer for your laptop operating system using the links below.
    * [Vagrant for Windows hosts](https://dl.bintray.com/mitchellh/vagrant/vagrant_1.6.5.msi)
    * [Vagrant for OS X hosts](https://dl.bintray.com/mitchellh/vagrant/vagrant_1.6.5.dmg)
    * [Vagrant for Linux hosts](https://www.vagrantup.com/downloads.html) (requires that you pick your distro)
1. Run the installer, choosing all defaults.
1. Reboot your laptop if prompted to do so when installation completes.

## Usage
After Vagrant and Virtualbox are setup, run the following commands to install the Dev Box. 

**Clone the Repository**

    git clone https://github.com/btantlinger/magento2-vagrant.git
**Navigate to the folder**

    cd /path/to/magento2-vagrant/

**(Optional) Add Magento Market Place access keys**


Magento 2.1 can be installed using Composer. However, the Magento Composer repo requires authentication.  To access the magento repo via Composer, you must create authentication keys on the Magento Marketplace.

Read [this](http://devdocs.magento.com/guides/v2.1/install-gde/prereq/connect-auth.html) guide on how to create your authentication keys.  Once you have created the keys, open up the `Vagrantfile` and place them here:

    publicKey = ""
    privateKey = ""
    
_Note: If you did not enter any authentication keys, Composer will not run automatically.  You will have to run it yourself to finish installation._

**Run Vagrant Command**

    vagrant up

The configuration process will take a while, especially if it is the first time you use a vagrant box with this virtual machine, because this one had to be completely downloaded at the first utilization.

Once completed, you can connect via SSH to you virtual machine, with putty for example. The adress and the port are usually
127.0.0.1 and 2222 respectively, but it can change if you have many VMs running at the same time.

If you added your autentication keys to the `VagrantFile`, Magento 2.1 should be fully deployed to your VM.  If you did not add your authentication keys, you will need to manually run the composer command on your VM via the commands below:

    vagrant ssh
    cd /var/www/html/magento2
    create-project --repository-url=https://repo.magento.com/ magento/project-community-edition .
    
**Sample Data**

Magento's sample data package can be installed by running the following command from the Magento root directory:

    bin/magento sampledata:deploy


**Other Info**

    Database Username: root
    Database Password: (none)
    SSH Login : vagrant
    SSH Password : vagrant
    root user password: vagrant
    Database Name: magento
    URL of Instance: http://192.168.33.10/magento2/
    Host File Configuration: 192.168.33.10 www.magento2.dev magento2.dev


## Issue Reporting
Any and all feedback is welcome.  Please let me know of any issues you may find in the bug tracker on github. You can find it [here. ](https://github.com/ryanstreet/magento2-vagrant/issues)
