[Inicio](https://github.com/DeathGabox/Dotfiles#dotfiles)
   
**Install ARCH LINUX**

> Cambiar layout a español
```
loadkeys es
```
> Ethernet conecta automaticamente
   <details>
   <summary><b>Conecta a internet</b></summary>
   <br>
   
  > Testear la conectividad de internet
```
ping -c 1 google.cl
``` 
> Conectar wifi
```
nmcli r wifi on
nmcli d wifi list
nmcli d wifi "Your\ Hostname" password "Your\ Password"
```
  
  </details>
 
--- 
  
> Elige tu modo de bios entre UEFI o Legacy Bios
> 
> `ls /sys/firmware/efi/efivar`, si sale `no such file or directory` eligue Legacy BIOS, si salen varios archivos, Elige UEFI

   <details>
   <summary><b>Legacy Bios (MBR)</b></summary>
   <br>
  
- Particiones
```
cfdisk
  dev/sda1 512M/Primary/Linux
  dev/sda2 dejando 4G/Primary/Linux
  dev/sda3 4G/Primary/Linux Swap
  "Write" y salir
```

> Revisar las particiones
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
```
     
  </details>
   
   <details>
   <summary><b>UEFI BIOS(GPT)</b></summary>
   <br>
   
  - Particiones
```
cfdisk
  dev/sda1 512M/EFI System
  dev/sda2 dejando 4G/Linux x86_64 root
  dev/sda3 4G/Primary/Linux Swap
  "Write" y salir
```

> Revisar las particiones
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
mkdir /mnt/efi
mount /dev/sda1 /mnt/efi
```
   </details>
   
---
   
> instalar paquetes con pacstrap
>
> NOTE: en sistemas UEFI, instalar efibootmgr os-probes ntfs-3g
```
pacstrap /mnt linux linux-firmware networkmanager grub wpa_supplicant base base-devel gvfs gvfs-mtp xdg-user-dirs dialog xf86-input-synaptics fish bat micro 
```
   
- Crear Fstab
```
genfstab -U /mnt >> /mnt/etc/fstab
cat /mnt/etc/fstab
```

   <details>
   <summary><b>chroot</b></summary>
   <br>


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
pacman -Sy sudo nano
nano /etc/sudoers
  descomentar %wheel ALL=(ALL:ALL) ALL
              root ALL=(ALL:ALL) ALL
```

- Configurar idiomas
```
nano /etc/locale.gen
  descomentar en_US.UTF-8 UTF-8
              es_ES.UTF-8 UTF-8
locale-gen
```

- Keymap
```
nano /etc/vconsole.conf
  KEYMAP=es
```

- Montar Bootloader
```
grub-install /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg
```

- Montar Bootloader UEFI
```
grub-install --efi-directory=/boot/efi --bootloader-id='Arch Linux' --target=x86_64-efi
grub-mkconfig -o /boot/grub/grub.cfg
```
      
- Hostname
```
echo $HOSTNAME > /etc/hostname
nano /etc/hosts
  Agregar la linea 127.0.0.1    $HOSTNAME.localhost $HOSTNAME
```

- Lujitos
```
pacman -S neofetch
neofetch
exit
```

   </details>
   
---
> Reboot
```
reboot now
```

- Configurar teclado en español
```
localectl set-x11-keymap es
```

- Activar Servicios
```
sudo su
ping -c 1 google.cl
systemctl start NetworkManager.service
systemctl enable NetwokManager
systemctl start wpa_supplicant.service
systemctl enable wpa_supplicant.service
ping -c 1 google.cl
```

- Instalar Paquetes
```
pacman -S xorg xorg-server qtile
```

- Instalar Git, yay, Blackarch, emptty
```
pacman -S git
mkdir -p Desktop/$USER/repos
cd !$ 
git clone https://aur.archlinux.org/yay.git
cd yay
exit
makepkg -si
sudo su
cd ../..
mkdir blackarch
cd !$
curl -0 https://blackarch.org/strap.sh
chmod +x strap.sh
./strap.sh
cd ..
yay -S emptty (Si no funciona, probar con emptty-git)
systemctl enable emptty
pacman -Sy
```

- Activar sonido
```
pacman -S pavucontrol alsa alsa-utils alsa-firmware
amixer sset Master unmute
amixer sset Speaker unmute
amixer sset Headphone unmute
alsamixer
``` 

- Timedate
```
timedatectl set-ntp true
timedatectl set-timezone America/Santiago
localectl set-locale LANG=es_CL.utf8
```


   <details>
   <summary><b>Fuentes adicionales</b></summary>
   <br>
   
> Fuentes Asiaticas
```
pacman -S asian-fonts wqy-zenhei ttf-hanazono ttf-baekmuk
```

> Fuentes
```
pacman -S ttf-jetbrains-mono ttf-hack-nerd cantarell ttf-dejavu
```

> Fuentes lib32
```
pacman -S lib32-fontconfig
```
> Emojis
```
pacman -S ttf-joypixels
```
</details>
