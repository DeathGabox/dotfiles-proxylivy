> Note: This is a forever work in progress
- [x] Read The Fabulous Manual ([RTFM](https://es.wikipedia.org/wiki/RTFM)) always, like [Archwiki](https://wiki.archlinux.org/) or Self-doc written by project, this is considered out of date by design
- [ ] Make .assets Folder with images and gifs

# Installation

You need to download an archlinux iso, you can grab [here](https://archlinux.org/download/) and burn the iso into a bootable usb, i recomend Ventoy, grab [here](https://github.com/ventoy/Ventoy)

> Cambiar layout a español
```
loadkeys es
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
iwctl station "device" connect "Your\ SSID"
```
  
</details>

> Config Time
```
timedatectl set-ntp true
timedatectl status
```

--- 
  
> Choose your BIOS mode between UEFY or Legacy bios by
> 
> `ls /sys/firmware/efi/efivars/`, if shows `no such file or directory` you need to choose legacy BIOS, if show a lot of files, choose UEFI

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
```
   
</details>
   
---
   
> Install with pacstrap
>
> NOTE: in UEFI systems, you need to install **efibootmgr os-prober ntfs-3g dosfstools mtools**
```
pacstrap /mnt linux linux-firmware networkmanager grub wpa_supplicant base base-devel gvfs gvfs-mtp xdg-user-dirs dialog xf86-input-synaptics bat micro intel-ucode
```
   
> Crear Fstab
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

> Configure Local Time Zone
```
ls /usr/share/zoneinfo
ln -s /usr/share/zoneinfo/"Area"/"Country" /etc/localtime
timedatectl set-timezone "Area"/"Country"
sudo hwclock --systohc --utc
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
  discomment: en_US.UTF-8 UTF-8
              es_CL.UTF-8 UTF-8
locale-gen
echo LANG=es_CL.UTF-8 > /etc/locale.conf
export LANG=es_CL.UTF-8
```

> Keymap
```
localectl set-x11-keymap latam
localectl set-locale LANG=es_CL.UTF-8
nano /etc/vconsole.conf
  KEYMAP=latam
```

---

> NOTE: Remember only mount bootloader follow by BIOS configuration

---

> Mount Legacy BIOS
```
grub-install /dev/sdx // (nvmexnxpx)
grub-mkconfig -o /boot/grub/grub.cfg
```

> Mount Bootloader UEFI
```
mount /dev/device1 -t vfat /boot/
grub-install --bootloader-id=grub --target=x86_64-efi --removable --recheck
grub-mkconfig -o /boot/grub/grub.cfg
```
Nota: --efi-directory=/boot/ podrias probar
   
      
> Hostname
NOTE: Change $HOSTNAME by the name you choose, duh
```
echo $HOSTNAME > /etc/hostname
nano /etc/hosts
  Agregar la linea 127.0.0.1    $HOSTNAME.localhost $HOSTNAME
```

</details>
   
---

> Desmontar Particiones
```
umount -R /mnt
```

---

> Reboot
NOTE: Remember disconnect Bootable USB
NOTE2: Sometimes, you need to add .efi kernel files to your bios to recognize rigth in the boot
```
reboot now
```

---

Optimize Pacman modifing `etc/pacman/conf` and uncomment `ParallelDownload=5` and add 4-5, more [info](https://wiki.archlinux.org/title/Pacman#Enabling_parallel_downloads)

> Note: Need Enable [ChaoticAUR](https://github.com/chaotic-aur)

> Note2: pkglist is make with `pacman -Qqen > pkglist.txt` and aur package with `pacman -Qqem > aurpkglist.txt`

> install Package by backup text
```
sudo pacman -S --needed - < ~/Documents/git/dotfiles-deathgabox/.package-backup/pkglist.txt
```

Install Yay Package by backup text
```
yay -S --needed - < ~/Documents/git/dotfiles-deathgabox/.package-backup/aurpkglist.txt
```

> Install YAY
```
mkdir -p Documents/$USER/repos
cd !$ 
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```

> Install Audio Server [Pipewire](https://wiki.archlinux.org/title/PipeWire)
```
pacman -S pipewire lib32-pipewire pipewire-docs pipewire-audio pipewire-alsa pipewire-pulse alsa alsa-utils bluez bluez-utils blueman pavucontrol
systemctl restart pipewire-pulse.service
amixer sset Master unmute
amixer sset Speaker unmute
amixer sset Headphone unmute
alsamixer
```

## Graphics

Now, if you do correctly, you are in vanilla Archlinux, congratulations, now, configure Graphic Card, i have a `NVIDIA Geforce 940MX` Codename `NV118 (GM108) 	GeForce 830M, 840M, 930M, 940M[X]`

Useful Links
- [Archlinux Wiki NVIDIA](https://wiki.archlinux.org/title/NVIDIA)
- [Archlinux Official Repositories(To enable multilib)](https://wiki.archlinux.org/title/Official_repositories)
- [Hyprland Nvidia Section](https://wiki.hyprland.org/Nvidia/)

> Install Package
```
sudo pacman -Syu nvidia-dkms nvidia-utils opencl-nvidia libva libva-nvidia-driver libvdpau nvidia-prime nvtop nvidia-settings lib32-nvidia-utils lib32-libva lib32-libvdpau
```


> Config

> At the end of `GRUB_CMDLINE_LINUX_DEFAULT=""` you need to add
```
nvidia_drm.modeset=1 nvidia_drm.fbdev=1
```

> At `MODULES` section in `/etc/mkinitcpio.conf` add
NOTE: Also remove kms from `HOOKS` in `/etc/mkinitcpio.conf`
```
nvidia nvidia_modeset nvidia_uvm nvidia_drm
```

> Update Grub and mkinitcpio
```
grub-mkconfig -o /boot/grub/grub.cfg
mkinitcpio --config /etc/mkinitcpio.conf --generate /boot/initramfs-custom.img
```

> Write in `/etc/modprobe.d/nvidia.conf`
```
options nvidia-drm modeset=1
```

> Fix Suspend Wakeup issues
```
systemctl enable nvidia-suspend.service --now
systemctl enable nvidia-hibernate.service --now
systemctl enable nvidia-resume.service --now
```

> Install Intel Driver
```
intel-gmmlib intel-media-driver
```

> Install Vulkan
```
vulkan-icd-loader lib32-vulkan-icd-loader
```

> Mod Permissions
```
usermod $USER -aG mpd games scanner vboxusers usbmux wireshark cups docker saned adbusers libvirt-qemu libvirt video uucp storage render optical lp kvm input audio wheel
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

> Install Simple Desktop Package
```
pacman -S wayland weston hyprland
```

## Config

### Firefox Config with [SimpleFox CSS Repo](https://github.com/migueravila/SimpleFox)

> Write in searchbar `about:config` and turn "True" to next params :
```
- toolkit.legacyUserProfileCustomizations.stylesheets
- layers.acceleration.force-enabled
- gfx.webrender.all
- svg.context-properties.content.enabled
```

> Note: Mozilla create weird names to the $Firefox-Default-Folder, for me, `Firefox -> u0kchxzv.default` `Firefox Developer Edition -> idknp77f.dev-edition-default` `Firefox-ESR -> rycwnmek.default-release`
```
cd ~/.mozilla/$Firefox-Branch/$Firefox-Default/
mkdir chrome
mv ~/Documents/git/dotfiles-gabo/.mozilla/$CSS-Folder/* chrome/
```

### Fish Config
NOTE: You need to redo all step in root mode to have fisher working well

> Install necessary package
```
sudo pacman -Syu fish fisher
fish
```


> Install Fisher
```
curl -sL https://raw.githubusercontent.com/jorgebucaran/fisher/main/functions/fisher.fish | source && fisher install jorgebucaran/fisher
```

> Fisher Plugins
> Install [Tide](https://github.com/IlanCosman/tide)
```
fisher install IlanCosman/tide@v6
```
Install [Done](https://github.com/franciscolourenco/done)
```
fisher install franciscolourenco/done
```

Install [Alias Assisntant](https://github.com/paysonwallach/fish-you-should-use/)
```
fisher install paysonwallach/fish-you-should-use
```

Install [Alias Ideas](https://github.com/gazorby/fish-abbreviation-tips)
```
fisher install gazorby/fish-abbreviation-tips
```

Dejar a fish como predeterminado
```
chsh -s /bin/fish
```

Config File Default
```
~/.config/fish/config.fish
~/.config/fish/conf.d/
```

Kitty Config
NOTE: To work, you need [Nerd Fonts](https://www.nerdfonts.com/), like HackNerdFont, or JetBrains, its on 
```
mv ~/Documents/git/dotfiles-gabo/.config/kitty/* ./config/kitty/
```

Fastfetch.conf file(WIP)

Wine package
```
sudo pacman -S --needed giflib lib32-giflib libpng lib32-libpng libldap lib32-libldap gnutls lib32-gnutls mpg123 lib32-mpg123 openal lib32-openal v4l-utils lib32-v4l-utils libpulse lib32-libpulse libgpg-error lib32-libgpg-error alsa-plugins lib32-alsa-plugins alsa-lib lib32-alsa-lib libjpeg-turbo lib32-libjpeg-turbo sqlite lib32-sqlite libxcomposite lib32-libxcomposite libxinerama lib32-libgcrypt libgcrypt lib32-libxinerama ncurses lib32-ncurses opencl-icd-loader lib32-opencl-icd-loader libxslt lib32-libxslt libva lib32-libva gtk3 lib32-gtk3 gst-plugins-base-libs lib32-gst-plugins-base-libs vulkan-icd-loader lib32-vulkan-icd-loader
```
