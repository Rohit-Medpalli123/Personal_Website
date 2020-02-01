---
layout: post
section-type: post
title: How to Install Vagrant on Windows
category: Installation
tags: [ 'Vagrant', 'Ubuntu' ]
---

Vagrant is a command-line tool for building and managing virtual machine environments. By default, Vagrant can provision machines on top of VirtualBox, Hyper-V, and Docker. Other providers such as Libvirt (KVM), VMware and AWS can be installed via the Vagrant plugin system.

Vagrant is typically used by developers to set up a development environment that matches the production environment.

### What does Vagrant do?
– Create and destroy VMs

– Starts, stops, restarts VMs

– Access to VMs

– Networking and WM settings

– Orchestrates “provisioning” for on-demand setup

### Windows, VirtualBox, and Hyper-V

If you wish to use VirtualBox on Windows, you must ensure that Hyper-V is not enabled on Windows. You can turn off the feature by running this Powershell command:

Disable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V-All
You can also disable it by going through the Windows system settings:

Right click on the Windows button and select ‘Apps and Features’.
Select Turn Windows Features on or off.
Unselect Hyper-V and click OK.
You might have to reboot your machine for the changes to take effect.

### Installing Vagrant
Installing Vagrant is extremely easy. Head over to the Vagrant downloads page and get the appropriate installer or package for your platform. Install the package using standard procedures for your operating system.

The installer will automatically add vagrant to your system path so that it is available in terminals. If it is not found, please try logging out and logging back in to your system (this is particularly necessary sometimes for Windows).

### Required Tools
1.Git

2.Virtualbox

3.Vagrant

### Step 1: Installing Git for windows 10
[Downnload latest version of GIT and install](https://git-scm.com/downloads )

### Step 2: Downloading and Installing VirtualBox on Windows 10
[Downnload latest version of Virtualbox and install](https://www.virtualbox.org/)

### Step 3: Installing Vagrant on windows 10

[Downnload latest version of Virtualbox and install](https://www.vagrantup.com/downloads.html)

### Most Common Vagrant Commands
vagrant init: initialize

vagrant up: Download image and do rest of the 
settings and power-up the box

vagrant status: Shows status

vagrant suspend: Saves the box’s current state

vagrant halt: shutdown the box (Power-off)

vagrant destroy: shutdown and delete the box



### References:
[Steps:Medium article](https://medium.com/@botdotcom/installing-virtualbox-and-vagrant-on-windows-10-2e5cbc6bd6ad)

[Vagrant box for ubuntu](https://app.vagrantup.com/ubuntu/boxes/xenial64)