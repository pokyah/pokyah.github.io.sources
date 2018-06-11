---
title: 'Installing Ubuntu gnome 16.04 on a windows machine'
author: Thomas Goossens
date: '2018-02-28'
categories:
  - R
  - how-to
tags:
  - statistics
---

## Download the .iso file 

Head at https://wiki.ubuntu.com/UbuntuGNOME/GetUbuntuGNOME and select the proper version (64bit)

## Create a booting USB drive

* If you have access to a Linux computer, launch [startup disk creator](https://en.wikipedia.org/wiki/Startup_Disk_Creator)

* Once launched, select the USB drive on which you want to install Linux and select the iso file you have just downloaded

* Click make Startup Disk

* Once you get notified that the installation is finished, eject the USB drive

## Enter the BIOS config to setup USB boot

* plug the USB drive in the computer

* boot your computer and press either f2, f10 or even enter to enter in the BIOS config

* once in the BIOS, find the menu called boot/startup or something similar. If you cannot change boot order from BIOS, restart and press another key like f12 to access the Boot menu configuration and choose boot from USB drive of flash drive disk

* The PC should now boot from the linux USB drive

## Linux configuration

* Choose install Linux
* Do not connect to internet -> sometimes it crashes the installation
* Thick Install third-party software
* Do not thick Encrypt
* Thick choose LVM
* Choose something else to manually edit the partition table

### partition table edition

* delete all the paritions with the minus sign
* create a new __swap__ partition of 4000MB using the plus sign and choose SWAP
* on free space add a new partition for the root : 80000MB thick logical and choose ext4 at mount point choose "/". Do not change beginning of this space
* on free space add a new partition for the home : remaining space thick logical and choose ext4 at mount point choose "/home". Do not change beginning of this space
* sometimes, you need to also create a boot partition (Ubuntu does it automatically)
* click install now and validate erase

### user config
* choose your timezone
* edit your username and password
* click install and wait for the instalaltion to be completed.

### install all softwares

* go to the [craw-ansible rpo](https://framagit.org/agromet-apps/craw-ansible) and follow the instructions in the README.md file



