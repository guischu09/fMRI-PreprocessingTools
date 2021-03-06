# README #

### Repository Description ###

This repository contains an implementation of a high level pipeline for fMRI preprocessing.

### Setup ###

The pipeline runs on Python, but depends on many dependencies. Here they are:



A.1) Install docker:


- sudo apt-get update
- sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common

- curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

- sudo apt-key fingerprint 0EBFCD88

- sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/	linux/ubuntu \
   $(lsb_release -cs) \
   stable"

- sudo apt-get update

- sudo apt-get install docker-ce docker-ce-cli containerd.io

- sudo docker run hello-world


A.1.1) Post Installation - run docker without sudo


- sudo groupadd docker

- sudo usermod -aG docker $USER

- newgrp docker 

- docker run hello-world



A.2) Install fmriprep image


- docker pull nipreps/fmriprep:20.1.1



B) Prepare the python enviroment:


1) Install miniconda. Installation details can be found at: https://docs.conda.io/en/latest/miniconda.html

2) Create enviroment, activate it and install dependencies. Open a new terminal and type the following:

- conda create --name fmriprep_aroma python=3.8 -y

- source activate fmriprep_aroma

- conda install -c anaconda numpy -y; conda install --channel conda-forge nipype==1.5.1 -y; pip install nibabel==3.2.0; pip install niworkflows==1.3.2; pip install nilearn==0.7.0; pip install fmriprep-docker==20.1.1;

3) Test if python wrapper is working:
- fmriprep-docker --help 

and say Yes to install what is missing


C) Mount device (e.g. External drive) in docker

Instructions: https://docs.cancergenomicscloud.org/docs/mount-a-usb-drive-in-a-docker-container#stepthree

0) Open a new terminal and type
- newgrp docker 

1) Find the name of your device. Name should be something like /dev/sdb

- sudo fdisk -l

alternatively, you can identify the name of your device at Disks. Search for Disks, select your device and check its path under the label "device".

2) create the /mnt/usb folder

- sudo mkdir /mnt/usb

3)Mount the device in /mnt/usb folder

- sudo mount /dev/device_name_from_step1/ /mnt/usb

4) Restart docker
- systemctl restart docker

5) Launch docker and mount the device 

- docker run -i -t -v /mnt/usb:/opt/usb ubuntu /bin/bash

6) Check if docker recognizes the device (you are now inside the container)

- ls /opt/usb

7) When finished, you can unmount the device as

sudo umount /mnt/usb


### Credits ###

-  Esteban O, Markiewicz CJ, Blair RW, Moodie CA, Isik AI, Erramuzpe A, Kent JD, Goncalves M, DuPre E, Snyder M, Oya H, Ghosh SS, Wright J, Durnez J, Poldrack RA, Gorgolewski KJ. fMRIPrep: a robust preprocessing pipeline for functional MRI. Nat Meth. 2018; doi:10.1038/s41592-018-0235-4

### Contact ###
guischu09@gmail.com - Guilherme Schu


