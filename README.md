# ArchBook
Arch Linux on MacBook Pro (Retina, 13-inch, Early 2015)

MacBook Pro 

ip link

ip link set WLAN up # Si no funciona

iwctl --passphrase PASS station WLAN connect RED

loadkeys es

timedatectl set-ntp true

pacman -Syy reflector

reflector -c Chile -a 6 --sort rate --save /etc/pacman.d/mirrorlist

pacman -Syy

reflector --country Chile --age 12 --protocol https --sort rate --save /etc/pacman.d/mirrorlist

reflector --latest 20 --age 1 --country 'Chile' --protocol https --sort rate --save /etc/pacman.d/mirrorlist

lsblk

fdisk -l

gdisk /dev/sda3
	n
	enter
	enter
	enter
	enter
	w
	Y

lsblk

mkfs.ext4 /dev/sda3
y
enter

mount /dev/sda3 /mnt
mkdir /mnt/boot
mount /dev/sda1 /mnt/boot

lsblk

pacstrap /mnt base base-devel linux-zen linux-zen-headers linux-firmware nano vim intel-ucode 

genfstab -U /mnt >> /mnt/etc/fstab 

cat /mnt/etc/fstab

arch-chroot /mnt

dd if=/dev/zero of=/swapfile bs=1G count=8 status=progress

chmod 600 /swapfile

mkswap /swapfile
swapon /swapfile

nano /etc/fstab
			(ver video 9:40)
			
ln -sf /usr/share/zoneinfo/America/Santiago /etc/localtime

hwclock --systohc

echo LANG=es_CL.UTF-8 >> /etc/locale.conf

echo KEYMAP=es >> /etc/vconsole.conf

nano /etc/locale.gen (es_CL.UTF-8)

locale-gen

echo zen >> /etc/hostname

nano /etc/hosts

127.0.0.1	localhost
::1		localhost
127.0.0.1  	zen.localdomain zen

passwd

pacman -S efibootmgr networkmanager network-manager-applet dialog wpa_supplicant mtools dosfstools base-devel linux-headers git reflector bluez bluez-utils pulseaudio pulseaudio-bluetooth alsa-utils cups xdg-utils xdg-user-dirs

bootctl --path=/boot install

cd /boot/
ls
cd loader/
ls
nano loader.conf
			(ver video 15:30)

cd entries/
ls
nano arch.conf
			(ver video 17:00)

systemctl enable NetworkManager
systemctl enable bluetooth
sudo systemctl enable --now cups

useradd -mG wheel nelson
passwd nelson

EDIT=nano visudo (descomentar %wheel ALL=(ALL) ALL)

exit
exit

umount -a

REBOOT

nmtui > activate a conection 

sudo pacman -S xf86-video-intel xorg sddm plasma kde-applications packagekit-qt5 chromium

sudo pacman -S materia-gtk-theme materia-kde papirus-icon-theme

sudo pacman -S plasma-wayland-session

sudo systemctl enable sddm

exit

REBOOT



kill -9 -1

sudo pacman -S xorg xterm xorg-xinit
