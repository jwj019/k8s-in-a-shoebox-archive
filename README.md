# k8s-in-a-shoebox
Repo for my home network running openmediavault, Nexus, and Kubernetes on SBCs in a shoebox!

My uses 5 single board computers: 
- 1 Odroid XU4 (Ubuntu Minimal 18.04)
- 3 Odroid C2 (Ubuntu Minimal 18.04)
- 1 Raspberry Pi 3 B+ (Raspbian Stretch Lite 2018-11-13)

The scripts within this repo are written with these images in mind, but should in theory work with any Debian based distros.

QUICKSTART

1) Flash SD cards with the following images:
  - Odroid XU4 - http://east.us.odroid.in/ubuntu_18.04lts/ubuntu-18.04-4.14-minimal-odroid-xu4-20180531.img.xz
  - Odroid C2 - http://east.us.odroid.in/ubuntu_18.04lts/ubuntu-18.04-3.16-minimal-odroid-c2-20180626.img.xz
  - Raspberry Pi 3 B+ - https://downloads.raspberrypi.org/raspbian_lite_latest
  
2) Follow this guide to enable SSH on your Raspbian image: https://hackernoon.com/raspberry-pi-headless-install-462ccabd75d0
  
3) Install Ansible and other dependencies on your controller host (AKA your local desktop)
  - sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367 && \
    sudo apt-get update -y && \
    sudo apt-get install ansible python sshpass -y
    
4) cp /etc/ansible/ansible.cfg ~/.ansible.cfg

5) Edit ~/.ansible.cfg to redirect the inventory to the hosts file in this repo

6) Customize the hosts file to use the IPs of your machines

7) Python needs to be installed on each individual node in order to be orchestrated by Ansible.  Use this to install it:
  - ansible <host> -m raw -a "apt install -y python-minimal python-simplejson" --ask-pass
  
8) Execute the following commands to run the user playbook:
  - ansible-playbook users.yml --ask-pass --limit=odroid -K
  - ansible-playbook users.yml --ask-pass --limit=pi -K

9) 
