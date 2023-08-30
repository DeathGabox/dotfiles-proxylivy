[Inicio](/.github/README.md)

[Thankyou](/.github/THANKYOU.md#Install)

**Install ARCH LINUX**

> Cambiar layout a español
```
loadkeys es
```
> NOTE: Ethernet conecta automaticamente

<details>
   <summary><b>Conecta a internet</b></summary>

> Testear la conectividad de internet
```
ping -c 1 google.cl
``` 
> Conectar wifi
```
iwctl station "device" connect "Your\ SSID"
```

```
timedatectl set-ntp true
timedatectl status
```
  
</details>

--- 
  
> Elige tu modo de bios entre UEFI o Legacy Bios
> 
> `ls /sys/firmware/efi/efivars/`, si sale `no such file or directory` eligue Legacy BIOS, si salen varios archivos, Elige UEFI

<details>
   <summary><b>Legacy Bios (MBR)</b></summary>
   
> Particiones
```
cfdisk dev/sdx // (nvmexnx)
  dev/sda1 512M/Primary/Linux
  dev/sda2 dejando 4G/Primary/Linux
  dev/sda3 4G/Primary/Linux Swap
  "Write" y salir
```

> Revisar las particiones
```
lsblk
```

> Crear Sistema de ficheros
```
mkfs.vfat -F 32 /dev/sda1
mkfs.ext4 /dev/sda2
mkswap /dev/sda3
swapon
```

> Montar particiones e instalar paquetes
```
mount /dev/sda2 /mnt
mkdir /mnt/boot
mount /dev/sda1 /mnt/boot
```

</details>
   
<details>
   <summary><b>UEFI BIOS(GPT)</b></summary>
   
> Particiones
```
cfdisk
  dev/sda1 512M/EFI System
  dev/sda2 dejando 4G/Linux filesystem
  dev/sda3 4G/Primary/Linux Swap
  "Write" y salir
```

> Revisar las particiones
```
lsblk
```

> Crear Sistema de ficheros
```
mkfs.vfat -F 32 -S 4096 /dev/device1
mkfs.ext4 -b 4096 /dev/device2
mkswap /dev/device3
swapon /dev/device3
```

> Montar particiones e instalar paquetes
```
mount /dev/device2 /mnt
```
   
</details>
   
---
   
> instalar paquetes con pacstrap
>
> NOTE: en sistemas UEFI, instalar **efibootmgr os-prober ntfs-3g dosfstools mtools**
```
pacstrap /mnt linux linux-firmware networkmanager grub wpa_supplicant base base-devel gvfs gvfs-mtp xdg-user-dirs dialog xf86-input-synaptics fish bat micro
```
   
> Crear Fstab
```
genfstab -U -p /mnt >> /mnt/etc/fstab
cat /mnt/etc/fstab
```

<details>
   <summary><b>chroot</b></summary>

> Crear Usuarios
```
arch-chroot /mnt
passwd
useradd -m $USER -G audio,lp,optical,storage,video,wheel,games,power,scanner -s /bin/fish
passwd $USER
```

> Configurar la hora y zona horaria
```
ls /usr/share/zoneinfo
ln -s /usr/share/zoneinfo/"Area"/"Country" /etc/localtime
hwclock --systohc --utc
```

> Sudo Config
```
pacman -Sy sudo nano
nano /etc/sudoers
  descomentar %wheel ALL=(ALL:ALL) ALL
```

> Configurar idiomas
```
nano /etc/locale.gen
  descomentar en_US.UTF-8 UTF-8
              es_ES.UTF-8 UTF-8
locale-gen
```

> Keymap
```
nano /etc/vconsole.conf
  KEYMAP=es
```

---

> NOTA: RECUERDA SOLO MONTAR EL BOOTLOADER DEPENDIENDO DE LA CONFIGURACION DE BIOS

---

> Montar Bootloader LEGACY BIOS
```
grub-install /dev/sdx // (nvmexnxpx)
grub-mkconfig -o /boot/grub/grub.cfg
```

> Montar Bootloader UEFI
```
grub-install --efi-directory=/boot --bootloader-id=grub --target=x86_64-efi --removable
grub-mkconfig -o /boot/grub/grub.cfg
```
Nota: --efi-directory=/boot/efi podrias probar
   
      
> Hostname
```
echo $HOSTNAME > /etc/hostname
nano /etc/hosts
  Agregar la linea 127.0.0.1    $HOSTNAME.localhost $HOSTNAME
```




> Lujitos
```
pacman -S neofetch
neofetch
exit
```

</details>
   
---

> Desmontar Particiones
```
umount -R /mnt
```

---

> Reboot
```
reboot now
```
