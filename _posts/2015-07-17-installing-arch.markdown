---
layout: post
title: "Installing Arch"
date: "2015-07-17"
categories: linux recipie
---
# Installing Arch
Installing Arch linux might be very unintuitive the first few times, but after installing it several times you do get used to it. Although it becomes rutinary it's common to miss a step or forget a command; This are some *VERY* compact notes on how to install Arch linux. They're ment as a cookbook just to remind me of the steps needed when installing Arch.
```
cfdisk
mkfs.ext4
mkswapge
swapon /dev/sda3
mount /dev/sda1 /mnt
mkdir /mnt/home
mount /dev/sda2 /mnt/home
pacstrap -i /mnt base base-devel
gefstab -U -p /mnt  :  sed ’s/rw,realtime,data=ordered/defaults,realtime/‘ >> /mnt/etc/fstab
arch-chroot /mnt

nano /etc/hostname
-> arch

nano  /etc/locale.gen
- >   en_US

locale=gen
echo LANG=en_US.UTF-8 > /etc/locale.conf
export LANG=en_US.UTF-8
ln -s /usr/share/zoneinfo/Mexico/General /etc/localtime
hwclock —systohc —utc
systemclt enable dhcpcd.service
ip link
nano /etc/pacman.conf

-> uncomment multilib

mkinitcpio -p linux
passwd
useradd -m -g users -s /bin/bash abcsds
passwd abcsds
pacman -Syy
pacman -S grub-bios
pacman -S os-prober
grub-install /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg
exit
umount /mnt/(boot,home,)
reboot



FONT=Lat2-Terminus16 to /etc/vconsole.conf
```
