# Dotfiles
Config Files :D
$USER == Usuario

---
Install ARCH LINUX

- Testear la conectividad de internet
```
ping -c 1 google.cl
``` 

- Cambiar layout a español
```
loadkeys es
```

- Particiones
```
cfdisk
  dev/sda1 512M/Primary/Linux
  dev/sda2 dejando 4G/Primary/Linux
  dev/sda3 4G/Primary/Linux Swap
  "Write" y salir
```

- Revisar las particiones
```
lsblk
```

- Crear Sistema de ficheros
```
mkfs.vfat -F 32 /dev/sda1
mkfs.ext4 /dev/sda2
mkswap /dev/sda3
swapon
```

- Montar particiones e instalar paquetes
```
mount /dev/sda2 /mnt
mkdir /mnt/boot
mount /dev/sda1 /mnt/boot
pacstrap /mnt linux linux-firmware networkmanager grub wpa_supplicant base base-devel
```

- Crear Fstab
```
genfstab -U /mnt >> /mnt/etc/fstab
cat /mnt/etc/fstab
```

- Crear Usuarios
```
arch-chroot /mnt
passwd
useradd -m $USER
passwd $USER
usermod -aG wheel $USER
```

- Sudo Config
```


















```
Post Install :D
```

sudo su
setxkbmap es
useradd -m $USER
passwd $USER
passwd root
usermod -aG wheel $USER
grub-install /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg
echo "Hostname" > /etc/hostname
systemctl start NetworkManager.service
systemctl enable NetwokManager
systemctl start wpa_supplicant.service
systemctl enable wpa_supplicant.service
fc-cache -f -v
timedatectl set-ntp true
timedatectl set-timezone America/Santiago
localectl set-locale LANG=es_CL.utf8
amixer sset Master unmute
amixer sset Speaker unmute
amixer sset Headphone unmute
alsamixer
mkdir -p /home/$USER/Documentos/github
cd $!
git clone https://aur.archlinux.org/yay.git
cd yay
exit
makepkg -si
sudo su
cd ..
mkdir blackarch
cd blackarch/
curl -0 https://blackarch.org/strap.sh
chmod +x strap.sh
sudo ./strap.sh
sudo systemctl enable emptty
```
```
sudo su
```
- /etc/sudoers (Descomenta)
- - %wheel ALL=(ALL:ALL) ALL
- /etc/vconsole.conf (Agrega)
- - KEYMAP=es
- /etc/hosts
- - 127.0.0.1 localhost
- - ::1 localhost
- /etc/locale.gen (Descomenta)
- - en_US.UTF-8 UTF8
- - es_CL.UTF-8 UTF8
- - - locale-gen
