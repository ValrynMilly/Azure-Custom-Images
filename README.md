# Azure Custom Images
## Create an Ubuntu VM

az group create -n CIRG -l location 

az vm create -g CIRG -n CustomVM -l location --Image UbuntuLTS --ssh-key-values .ssh/id_rsa.pub

ssh User@IP

For Windows VM follow this link here https://docs.microsoft.com/en-us/azure/virtual-machines/windows/quick-create-cli

## Setup Image

sudo apt update 

sudo apt install python3-pip cd Azure-Custom-Image 

sudo pip3 -r requirements.txt vim /tmp/app.service [Unit] Description=App start up

    [Service]
    ExecStart=/usr/bin/python3 /home/user/Azure-Custom-Image/app.py

    [Install]
    WantedBy=multi-user.target
    
## Create Image
az vm deallocate -g CIRG -n VMname

az vm generalize -g CIRG -n VMname

az image create -g CIRG -n Imagename --source VMname

## Finally create new VM
az vm create -g CIRG -n VMname -l location --image Imagename --ssh-key-values .ssh/id_rsa.pub