- [x] Read The Fabulous Manual ([RTFM](https://es.wikipedia.org/wiki/RTFM)) always, like [Archwiki](https://wiki.archlinux.org/) or Self-doc written by project, this is considered out of date by design

# Installation

You need to download an archlinux [iso](https://archlinux.org/download/) and burn the iso into a bootable usb, i recomend [Ventoy](https://github.com/ventoy/Ventoy), plug the usb in the pc, then start the installation commands, also read Official Guide Installation by [Archwiki](https://wiki.archlinux.org/title/Installation_guide)


> Change Layout to Latam
```
loadkeys la-latin1
```
> NOTE: Ethernet automatically work

<details>
   <summary><b>Connect to internet via Wi-Fi</b></summary>

> Test internet connectivity
```
ping -c 1 google.cl
```
> Connect Wifi
```
ip a
iwctl station "device" connect "Your\ SSID"
```
  
</details>

> Configure Local Time Zone [info](https://wiki.archlinux.org/title/System_time)
```
timedatectl list-timezones
ln -sf /usr/share/zoneinfo/"Zone"/"Sub-Zone" /etc/localtime
timedatectl set-timezone "Zone"/"Sub-Zone"
timedatectl set-ntp true
sudo hwclock --systohc --utc
timedatectl status
```

--- 
  
> Choose your BIOS mode between UEFY or Legacy bios by
> `ls /sys/firmware/efi/efivars/`, if shows `no such file or directory` you need to choose legacy BIOS, if show files, choose UEFI

<details>
   <summary><b>Legacy Bios (MBR)</b></summary>
   
> Partitions
```
cfdisk dev/sdx // (nvmexnx)
  dev/sda1 512M/Primary/Linux
  dev/sda2 dejando 4G/Primary/Linux
  dev/sda3 4G/Primary/Linux Swap
  "Write" y salir
```

> Look at Partitions
```
lsblk
```

> Create File System
```
mkfs.vfat -F 32 /dev/sda1
mkfs.ext4 /dev/sda2
mkswap /dev/sda3
swapon /dev/sda3
```

> Mount File System
```
mount /dev/sda2 /mnt
mkdir /mnt/boot
mount /dev/sda1 /mnt/boot
```

</details>
   
<details>
   <summary><b>UEFI BIOS(GPT)</b></summary>
   
> Partitions
```
cfdisk /dev/device
  dev/device1 512M/EFI System
  dev/devive2 dejando 4G/Linux filesystem
  dev/device3 4G/Primary/Linux Swap
  "Write" y salir
```

> Look at Partitions
```
lsblk
```

> Create File Systems
```
mkfs.vfat -F 32 -S 4096 /dev/device1
mkfs.ext4 -b 4096 /dev/device2
mkswap /dev/device3
swapon /dev/device3
```

> Mount Partitions
NOTE: Boot is mounted next
```
mount /dev/device2 /mnt
mkdir /mnt/boot/
mount /dev/device1 -t vfat /boot/
```
   
</details>
   
---

> Install with pacstrap
```
pacstrap /mnt linux linux-firmware linux-headers networkmanager grub wpa_supplicant base base-devel intel-ucode efibootmgr os-prober ntfs-3g dosfstools mtools sbsigntools sbctl sbsigntools efitools
```

> Create Fstab
```
genfstab -U -p /mnt >> /mnt/etc/fstab
cat /mnt/etc/fstab
```

<details>
   <summary><b>chroot</b></summary>

> Create Users
```
arch-chroot /mnt
passwd
useradd -m $USER -g users -G audio,lp,optical,storage,video,wheel,games,power,scanner -s /bin/fish
passwd $USER
```

> Sudo Config
- Edit /etc/sudoers and discomment
```
%wheel ALL=(ALL:ALL) ALL
```

> Configure Language
- In `/etc/locale.gen` discomment `en_US.UTF-8 UTF-8` and `es_CL.UTF-8 UTF-8`, then
```
locale-gen
echo LANG=es_CL.UTF-8 > /etc/locale.conf
```

---
## Bootloader
> NOTE: Remember only mount bootloader follow by BIOS configuration, and read [Grub](https://wiki.archlinux.org/title/GRUB) Documentation
> Note: See [Grub#Shrim-Lock Wiki](https://wiki.archlinux.org/title/GRUB#Shim-lock)

> Mount Bootloader Legacy BIOS
```
grub-install /dev/sdx // (nvmexnxpx)
```

> Mount Bootloader UEFI
```
grub-install --target=x86_64-efi --efi-directory=/boot/ --bootloader-id=GRUB --removable --recheck
```

### USE CA
- Note: Test this -> `grub-install --target=x86_64-efi --efi-directory=/boot/ --bootloader-id=GRUB --removable --recheck --modules="tpm" --disable-shim-lock`

### Create keys with sbctl
NOTE: See this message (Your system is not in Setup Mode! Please reboot your machine and reset secure boot keys before attempting to enroll the keys.)
NOTE2: You need to delete all keys, and tpm keys, to enter in setup mode [Youtube Help](https://www.youtube.com/watch?v=yU-SE7QX6WQ)
```
sudo sbctl status
sudo sbctl create-keys
sudo sbctl enroll-keys -m
```

### Signing
Note: i think only need to sign `bootx64` and `grub`
Note2: Can be automaticed with `sbctl verify | sed 's/✗ /sbctl sign -s /e'`
```
sudo sbctl verify
sudo sbctl sign -s /boot/EFI/BOOT/BOOTX64.EFI
sudo sbctl sign -s /boot/grub/x86_64-efi/grub.efi
sudo sbctl sign -s /boot/grub/x86_64-efi/core.efi
sudo sbctl sign -s /boot/vmlinuz-linux
```

### After Sign
NOTE: You need to reboot and check
```
reboot
sbctl status
```

## USE MOK MANAGER
Note: Where is sbsign??
```
grub-install --target=x86_64-efi --efi-directory=/boot/ --modules="tpm" --sbat /usr/share/grub/sbat.csv
sbsign --key MOK.key --cert MOK.crt --output /boot/EFI/GRUB/grubx64.efi /boot/EFI/GRUB/grubx64.efi
cp esp/EFI/GRUB/grubx64.efi esp/EFI/BOOT/grubx64.efi
```

---

> Update Grub
```
grub-mkconfig -o /boot/grub/grub.cfg
```

> Hostname
- Edit `/etc/hosts`
> Note: Change $HOSTNAME
```
echo $HOSTNAME > /etc/hostname
nano /etc/hosts
  Agregar la linea 127.0.0.1    $HOSTNAME.localhost $HOSTNAME
```

</details>


> Umount Partitions
Note: Before reboot, disconnect Any USB Device, some bios get blocked for some reason, and need to add .efi files to get secure boot
```
exit
umount -R /mnt
reboot
```

Quick Note: Congrats!!, now with the fun part, customization.

# First Startup
## Internet
```
sudo systemctl enable NetworkManager.service --now
```

## Spanish Mode
```
localectl set-x11-keymap latam
localectl set-locale LANG=es_CL.UTF-8
```

## Repo Config
- Need Enable [ChaoticAUR](https://github.com/chaotic-aur) and [multilib](https://wiki.archlinux.org/title/Official_repositories) repo
- Optimize Pacman modifing `etc/pacman/conf` and uncomment `ParallelDownload=5` -> [more info](https://wiki.archlinux.org/title/Pacman#Enabling_parallel_downloads)

<details>
   <summary><b>Install from backup(~2000Package)</b></summary>

> Note: 
> Note2: pkglist is make with `pacman -Qqen > pkglist.txt` and aur package with `pacman -Qqem > aurpkglist.txt`
```
sudo pacman -S --needed - < ~/Documents/git/dotfiles-deathgabox/.package-backup/pkglist.txt
```
```
yay -S --needed - < ~/Documents/git/dotfiles-deathgabox/.package-backup/aurpkglist.txt
```

</details>

### Install Package
```
gvfs gvfs-mtp xdg-user-dirs dialog xf86-input-libinput bat micro
```

## Wine package
```
sudo pacman -S --needed giflib lib32-giflib libpng lib32-libpng libldap lib32-libldap gnutls lib32-gnutls mpg123 lib32-mpg123 openal lib32-openal v4l-utils lib32-v4l-utils libpulse lib32-libpulse libgpg-error lib32-libgpg-error alsa-plugins lib32-alsa-plugins alsa-lib lib32-alsa-lib libjpeg-turbo lib32-libjpeg-turbo sqlite lib32-sqlite libxcomposite lib32-libxcomposite libxinerama lib32-libgcrypt libgcrypt lib32-libxinerama ncurses lib32-ncurses opencl-icd-loader lib32-opencl-icd-loader libxslt lib32-libxslt libva lib32-libva gtk3 lib32-gtk3 gst-plugins-base-libs lib32-gst-plugins-base-libs vulkan-icd-loader lib32-vulkan-icd-loader
```

## Audio Server
> Install Audio Server [Pipewire](https://wiki.archlinux.org/title/PipeWire)
```
sudo pacman -S pipewire lib32-pipewire pipewire-docs pipewire-audio pipewire-alsa pipewire-jack pipewire-v4l2 pipewire-pulse alsa-utils bluez bluez-utils blueman pavucontrol gst-plugin-pipewire libpipewire lib32-libpipewire libwireplumber qpwgraph wireplumber
```

> Start Pipewire with pulseaudio
```
systemctl enable pipewire-pulse.service --user --now
```

> Unmute from alsa-utils
```
amixer sset Master unmute
amixer sset Speaker unmute
amixer sset Headphone unmute
alsamixer
```

> Need to Reboot
```
reboot
```

## Desktop
> Install Simple Desktop Package
```
pacman -S wayland weston hyprland
```

 <details>
   <summary><b>Fuentes adicionales</b></summary>
   <br>

> Fuentes Asiaticas
```
pacman -S wqy-zenhei ttf-hanazono ttf-baekmuk
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

## Final Extra Package
```
sudo pacman -S virt-manager qemu virtualbox docker docker-compose wireshark-cli wireshark-qt adbmanager sane sane-airscan avahi cups usbmuxd mpd mpv
```

> Final Mod Permissions
```
sudo usermod $USER -aG games,wheel,audio,kvm,optical,storage,uucp,video,wireshark,libvirt,audio,video,adbusers,saned,cups,lp,scanner,usbmux,mpd,input,libvirt-qemu,vboxusers,docker,render
```

> Start Services
```
systemctl enable docker sshd avahi-daemon cups virtqemud libvirtd --now
```

## Final WIP TESTING (Modprobe Kernel things) please ignore
NOTE: Add this on MODULES?? [mkinitcpio](https://wiki.archlinux.org/title/Mkinitcpio#MODULES)
> Modprobe
```
sudo modprobe -a vboxdrv
```
