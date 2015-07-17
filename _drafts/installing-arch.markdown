---
layout: post
title: "Installing Arch"
date: "2015-07-17"
---
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
