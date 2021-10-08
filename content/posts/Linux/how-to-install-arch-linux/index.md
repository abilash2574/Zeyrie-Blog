---
title: "How to Install Arch Linux"
subtitle: ""
date: 2021-10-08T23:23:00+05:30
lastmod: 2021-09-22T23:01:27+05:30
draft: false
author: "Abilash S"
authorLink: "https://www.zeryie.in/"
description:
tags: ["arch_linux", "tutorial", "linux"]
categories: ["Linux", ]

resources:
- name: featured-image
  src: "pics/featured-image.png"
- name: featured-image-preview
  src: featured-image-preview.jpg

toc:
  enable: true
math:
  enable: false
lightgallery: true
license: ""

hiddenFromHomePage: false
hiddenFromSearch: false
---

In this tutorial, we will learn how to install arch linux. This can be used as a reference for installing vanilla arch linux. This tutorial will be a step by step guide and it will be install linux to a stage, where we can boot into the installed system. No further builds of environments, other packages will not be covered in this turorial

<!--more-->


# Getting Started

So, lets first head to the official {{< link href="https://archlinux.org/download/" content="Arch linux" title="Visit Arch linux download page" >}} website's download page to download the iso file for installation.

In this page, you have different options to download the image file for different purposes. Choose the one that suits your case. 

This tutorial will complete until we install all the necessary packages and tools for our arch system to boot.

<!-- # Creating a Bootable installation media -->

<!-- # Booting into the installation media -->

# Installation

## Setup the keyboard layout

{{< admonition info "" >}}
By default the keyboard layout is set to en-us!
{{< /admonition >}}

To list all the availabe keyboard layouts:

```sh
ls /usr/share/kbd/keymaps/**/*.map.gz | less
```

Then to load the layout:

```sh
loadkeys de-latin1
```


## Connet to Internet

To verify if you have an active connection, you can use ping 

{{< admonition tip "To check if you have internet connection" >}}
You can use `ping`, as follows:
```sh
ping www.google.com
```
{{< /admonition >}}

<!-- Write here how to connect to a wifi network -->


## Update the system clock

To update the system clock run:

```sh
timedatectl set-ntp true
```

To verify if the above command worked current:

```sh 
timedatectl status
```

## Partitioning the disk

To partition our disk we are using fdisk, there are many other ways as well. But I am using the one recommended by arch wiki.

<div>
<span style="color: red">Step 1 ->  </span> To list all the disks available, run `fdisk -l`.

<!-- add the image  -->
{{< image src="pics/list_disk.png" caption="List of disks">}}

Now select the disk you want to work with, run 

```sh
fdisk /dev/the_disk_to_be_partitioned
```

{{< admonition tip "" >}}
If you need help using fdisk always remeber to check the help prompt by typing `m`
{{< /admonition >}}

After selecting a disk to work with, you will be taken to another prompt.
</div>

<div>
<span style="color: red">Step 2 ->  </span> Select a label for the disk

To do this, type `g` in the prompt. This will create a GPT partition table, which is required for linux.

We can do that as follows:

{{< image src="pics/create_label.png" caption="Creating GPT label">}}

</div>

{{< admonition note "" >}}
* A minimum of <span style="color: red">550 MB</span> is recommended for the boot partition.
* Do enter the default value in the prompts just press enter.
* A easy way to type the partition size in the prompt, use `+` follwed by the `desired size` and `M` for mebabytes, `G` for gigabytes, and so on. <span>Eg. +550M</span> represents 550 MB
{{< /admonition >}}

<div>
<span style="color: red">Step 3 ->  </span> Creating a EFI boot partition

Since I am using a UEFI based system, I am creating a `/boot` partition right away.

So we will create a new partition as follows:

<!-- Added the image of first partition  -->
{{< image src="pics/boot_partition.png" caption="Creating Boot partition">}}


Now we much note that, the type of this partition is linux filesystems, but we need this to be a `FAT32` file system, so to convert the file system we use the `t` command in the prompt, as follows:

{{< image src="pics/change_filesystem.png" caption="Changing file system">}}


{{< admonition tip  "" >}}
To know all the filesystems available in fdisk, type `L` in the prompt asking for selecting a filesystem type
{{< /admonition >}}


<!-- add the image for changing file type of boot partition -->
{{< image src="pics/efi_file.png" caption="Changed file system to EFI">}}


<div>
<span style="color: red">Step 4 ->  </span> Creating a swap partition

Next we want a swap partition for our system, and it is recommended to have a swap partition even if you have more than enough RAM, but in end its upto you to create this partition.

Create another partition with size of your choice, I have created a swap of size `2 GB`.

<!-- Add a image for swap partition -->
{{< image src="pics/swap_partition.png" caption="Creating a swap partition">}}


To change the filesystem type for this parition do as follows:

<!-- add image for chaning filetype -->
{{< image src="pics/swap_file.png" caption="Changing file system to swap">}}

</div>

<div>
<span style="color: red">Step 5 ->  </span> Creating a Root Partition

Next we will create a `root` partition of our choice:

<!-- add image for root partition. -->
{{< image src="pics/root_partition.png" caption="Creating root partition">}}


Since the file type for the root parition is to be linux filetype, we leave it unchanged
</div>

<div>
<span style="color: red">Step 6 -> </span> Create a Home partition

Finally create a `home` parition:

<!-- add image for home partition. -->
{{< image src="pics/home_partition.png" caption="Creating home partition">}}


The file type of this partition is to be linux filesystem, so we leave it unchanged.
</div>

<div>
<span style="color: red">Step 7 -> </span> Finally to write all the changes

To write all the changes and quit fdisk press `w`, which will write our changes.

{{< image src="pics/write_partition.png" caption="Write all changes to disk">}}


</div>

## Defining File Systems

After creating all the partitions, we must format it to the appropriate file systems 

Run the following commands to create appropriate file systems:

```sh
mkfs.fat -F32 /dev/sda1   # This is for boot partition
mkswap /dev/sda2          # this is for swap 
swapon /dev/sda2          # turning on swap
mkfs.ext4 /dev/sda3       # for root partition
mkfs.ext4 /dev/sda4       # for home partition
```

## Mounting Partitions

To mount all the partitions we have created till now, run the following:

```sh 
mount /dev/sda3 /mnt          # this will mount the root partition
mkdir -p /mnt/boot/EFI        # this creates the boot and EFI dir
mount /dev/sda1 /mnt/boot/EFI # this will mount the boot parition
mkdir /mnt/home               # we create the home dir
mount /dev/sda4 /mnt/home     # and we mount the home partiton
```

To check if you have everything setup correctly, run `fdisk -l` or `lsblk`.

## Installing Linux

To installing the base installation packages, run the follwoing:

```sh 
pacstrap /mnt base linux linux-firmware
```


After installing the packages, we are going to generate the `fstab` for our system as follows:

```sh 
genfstab -U /mnt >> /mnt/etc/fstab
```

We can verify if the partitions we have created by running:

```sh
cat /mnt/etc/fstab
```

Now we will move to the installation drive or our system by running the following:

```sh 
arch-chroot /mnt
```

### Setting Time zone

We can set the time zone to our system by running the following command:

```sh 
# ln -sf /usr/share/zoneinfo/REGION/CITY /etc/localtime
# e.g
ln -sf /usr/share/zoneinfo/Asia/Kolkata /etc/localtime
```

To actually fine the region and city we can `ls` to the `zoneinfo` dir as follows:

```sh
ls /usr/share/zoneinfo          # this will list all the zones
ls /usr/share/zoneinfo/REGION   # this will list all the cities in that region (Change region with actual folder from the above list )
``` 
### Setting Hardware clock

To set the hardware clock run the following:

```sh
hwclock --systohc
```

### Setting Locale

Now we must set the locale file, but before this, we must install a editor of our choice to open the `loacle.gen` file. To do so:

```sh
pacman -S nano # or vim
```

Next we must open the `locale.gen` file as follows

```sh
nano /etc/locale.gen
```

In this file, find the layout of your keyboard or the locale and uncomment it.
Usually its `en_US.UTF-8 UTF-8` for English US.
After uncommenting, save the file.

{{< admonition tip "" false>}}
We can have more than one locale, its your choice, so uncomment the locale that you wanted
{{< /admonition >}}

Now we must generate the locale, we do that by running:

```sh
locale-gen
```

### Adding host
Now we can set the host name as follows:

```sh
nano /etc/hostname
```

Enter the hostname of the system, (which will be your system name). Now save the file after entering the name

Next we will create a hostfile as follows:

```sh 
nano /etc/hosts
```

This file will note be empty and we must add the following lines

{{< highlight code >}}
127.0.0.1	localhost
::1		    localhost
127.0.1.1	host_name.localdomain  host_name  # Replace host_name with your hostname
{{< /highlight >}}

### Creating Root and User

Now we will create a password for out root user, we do that as follows:

```sh
passwd
```

This will prompt you to enter the password for root user, enter the password and confirm it.

Now we will add a normal user, as we don't want to login as root all the time.

```sh
adduser -m user_name
passwd user_name 
```

Enter the password for the new user and confirm it.

Now, we have to give user privileges to the newly created user, we can do that as follows:

```sh 
usermod -aG wheel,audio,video,optical,storage user_name   # we can add more privileges as well
```

Now we must install sudo to give sudo privileges to the user

```sh 
pacman -S sudo
```

To give the sudo privileges to user, we will edit the `visudo` file:

```sh
EDITOR=nano visudo          # to use vim EDITOR=vim visudo
```

Now we must find the line about wheel group.

{{< highlight code >}}
%wheel ALL=(ALL) ALL
{{< /highlight >}}

Just uncomment the above line and save it.

## Installing GRUB

Now we must install grub, so firstly we must download grub installer, and along side, we need efi installers as well for the system so,

```sh 
pacman -S grub efibootmgr dosfstools or-prober mtools
```

Now we will run the grub install command as follows:

```sh 
grub-install --target=x86_64-efi --bootloader-id=grub_uefi --recheck 
```

We get a message saying no error reported, which means we have successfully installed grub. 

Next we must make a grub configuration file as follows:

```sh 
grub-mkconfig -o /boot/grub/grub.cfg
```

Now we have generated grub config files, from this point we can reboot the system and use it further.

{{< admonition tip "Bonus Tips" >}}

It is a good choice to install some packages for new system such as network manger, and more.

So, 

```sh 
pacman -S networkmanager nvim git 
```

We should also enable the network manager, so:

```sh 
systemctl enable NetworkManager
```


{{< /admonition >}}


Now we can exit from the chroot, as follows:

```sh 
umount -l /mnt
```

This will force umount and now we can reboot the system by running:

```sh 
reboot
```



{{< admonition success  "Thank You for Reading" >}}
If you like this post, bookmark it for future references, share it with friends and peoples who might need it.
{{< /admonition >}}

