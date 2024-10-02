sudo su

cfdisk /dev/sda

mkfs.fat -F 32 /dev/sda1

mkswap /dev/sda2

mkfs.ext4 /dev/sda3

mkdir /mnt/boot

mount /dev/sda1 /mnt/boot

swapon /dev/sda2

mount /dev/sda3 /mnt

connect to internet

dinitctl start ntpd

basestrap /mnt base base-devel dinit elogind-dinit linux-zen linux-zen-headers linux-firmware neovim networkmanager networkmanager-dinit ntfs-3g sudo 

fstabgen -U /mnt >> /mnt/etc/fstab

artix-chroot /mnt

nvim /etc/fstab

ln -sf /usr/share/zoneinfo/America/Argentina/Buenos_Aires /etc/localtime

hwclock --systohc

nvim /etc/locale.gen

locale-gen

echo LANG=en_US.UTF-8 >> /etc/locale.conf

pacman -S grub os-prober efibootmgr amd-ucode xf86-video-amdgpu

grub-install --target=x86_64-efi --bootloader-id=grub --efi-directory=/boot

nvim /etc/default/grub #grub timeout, enable os prober

grub-mkconfig -o /boot/grub/grub.cfg

passwd

useradd -m -G wheel mxsatworld

passwd mxsatworld

nvim /etc/hostname

nvim /etc/hosts

exit

sudo umount -a

sudo reboot

sudo dinitctl enable NetworkManager

sudo pacman -S broadcom-wl-dkms

sudo reboot

nmcli dev wifi list

sudo nmcli --ask dev wifi connect "$1"

sudo pacman -S xorg xorg-xinit i3 xfce4-terminal firefox dmenu keepassxc alsa-utils pulseaudio htop brightnessctl xclip maim libreoffice lxappearance arc-gtk-theme bluez bluez-utils pulseaudio-bluetooth cups cups-pdf usbutils openssh hplip xss-lock tmux git thunar gvfs vlc zvbi xdotool dunst bluez-dinit cups-dinit unrar unzip java-runtime-common jre-openjdk

nvim ~/.xinitrc #exec /usr/bin/i3

startx

ssh-keygen -t rsa -b 4096 -C "mcuadrado578@gmail.com"

alsamixer
    unmute channels

sudo nvim /etc/modules-load.d/snd-pcm-oss.conf

sudo nvim /etc/modules-load.d/btusb.conf

sudo dinitctl enable bluetoothd

sudo dinitctl enable cupsd

install yay

yay -S caffeine-ng

usermod -a -G video,dbus,cups mxsatworld
