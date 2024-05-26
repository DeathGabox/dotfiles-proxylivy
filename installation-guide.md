> Note: This is a forever work in progress

- Read The Fabulous Manual ([RTFM](https://es.wikipedia.org/wiki/RTFM)) always, like [Archwiki](https://wiki.archlinux.org/) , [geento wiki](https://wiki.gentoo.org/wiki/Main_Page) or Self-doc written by project, this repo dotfile guide is considered out of date by design

- Read [dualboot.md](/dualboot.md) if you want to install windows(WinterOS) :P

Take This notes, to read path
- Root Path: "/"
- User Path: "~/"
- Github Path: "~/dotfiles/"

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
with `ip a` you can view `station`, usually is `wlan0` in my device
```
ip a
iwctl station "station" scan
iwctl station "station" get-networks
iwctl station "station" connect "Your\ SSID"
```
  
</details>

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
mount /dev/device1 -t vfat /mnt/boot/
```
   
</details>
   
---

> Install with pacstrap
```
pacstrap /mnt linux linux-firmware linux-headers networkmanager grub wpa_supplicant base base-devel intel-ucode efibootmgr os-prober ntfs-3g dosfstools mtools sbsigntools sbctl efitools fish micro git
```

> Create Fstab
```
genfstab -U -p /mnt >> /mnt/etc/fstab
cat /mnt/etc/fstab
```

## Create Users
```
arch-chroot /mnt
passwd
useradd -m $USER -G wheel -s /bin/fish
passwd $USER
```

## Sudo Config
- Edit /etc/sudoers and discomment
```
%wheel ALL=(ALL:ALL) ALL
```

## Configure Language
- In `/etc/locale.gen` discomment `en_US.UTF-8 UTF-8` and `es_CL.UTF-8 UTF-8`

## Configure locale
```
locale-gen
echo LANG=es_CL.UTF-8 > /etc/locale.conf
```

## Hostname
- In `/etc/hostname` write your $HOSTNAME

## Hosts
In `/etc/hosts` add your $HOSTNAME
```
127.0.0.1      $HOSTNAME.localhost $HOSTNAME
```

---
## Bootloader
> NOTE: Remember only mount bootloader follow by BIOS configuration, and read [Grub](https://wiki.archlinux.org/title/GRUB) Documentation
### Bootloader Legacy BIOS
```
grub-install /dev/sdx // (nvmexnxpx)
```

### Bootloader UEFI
> Note: See [Grub#Shrim-Lock Wiki](https://wiki.archlinux.org/title/GRUB#Shim-lock)
```
grub-install --target=x86_64-efi --efi-directory=/boot/ --bootloader-id=GRUB --modules="tpm" --disable-shim-lock --removable --recheck
```

### Update Grub
```
grub-mkconfig -o /boot/grub/grub.cfg
```

### Create keys with sbctl
> enroll-keys dont work because [Acer Bios](https://wiki.archlinux.org/title/Acer_Aspire_E5-575) is weird, i still dont know how to make work right, but its worth it
```
sudo sbctl status
sudo sbctl create-keys
sudo sbctl enroll-keys -m
```

### Signing
> Note: Can be automaticed with `sbctl verify | sed 's/✗ /sbctl sign -s /e'`
```
sudo sbctl verify
sudo sbctl sign -s /boot/EFI/BOOT/BOOTX64.EFI
sudo sbctl sign -s /boot/grub/x86_64-efi/grub.efi
sudo sbctl sign -s /boot/grub/x86_64-efi/core.efi
sudo sbctl sign -s /boot/vmlinuz-linux
sudo sbctl status
```

> Umount Partitions
Note: Before reboot, disconnect Any USB Device, some bios get ultra slow down in init for some reason
```
exit
umount -R /mnt
reboot
```

# First Startup
Quick Note: Congrats!!, now with the fun part, customization.

## Make Internet Works
Note: Next you need to connect to wifi with `nmtui`, ethernet just work
```
sudo systemctl enable NetworkManager.service bluetooth.service --now
```

## Spanish Mode
```
localectl set-x11-keymap latam
localectl set-locale LANG=es_CL.UTF-8
```

## Configure Local Time Zone 
> see System Time in Archwiki for more [info](https://wiki.archlinux.org/title/System_time)
```
timedatectl list-timezones
ln -sf /usr/share/zoneinfo/"Zone"/"Sub-Zone" /etc/localtime
timedatectl set-timezone "Zone"/"Sub-Zone"
timedatectl set-ntp true
sudo hwclock --systohc --utc
timedatectl status
```

## Repo Config
- Need Enable [ChaoticAUR](https://github.com/chaotic-aur) and [multilib](https://wiki.archlinux.org/title/Official_repositories) repo
- Optimize Pacman modifing `etc/pacman/conf` and uncomment `ParallelDownload=5` -> [more info](https://wiki.archlinux.org/title/Pacman#Enabling_parallel_downloads)

> Note: pkglist list is make with `pacman -Qqen > pkglist.txt` and aur package list with `pacman -Qqem > aurpkglist.txt`

Pacman Package
```
sudo pacman -S --needed - < .package-backup/pkglist.txt
```

Intall yay from chaotic-aur
```
sudo pacman -Syu yay
```

AUR package
```
yay -S --needed - < .package-backup/aurpkglist.txt
```

<details>
   <summary><b>Manual install by package</b></summary>

## Font
```
sudo pacman -S wqy-zenhei ttf-hanazono ttf-baekmuk ttf-jetbrains-mono ttf-hack-nerd ttf-dejavu lib32-fontconfig ttf-joypixels
```

## All Package
> Note: recomend to open weston to copy and paste 
```
sudo pacman -S virt-manager qemu virtualbox docker docker-compose wireshark-cli wireshark-qt adbmanager sane sane-airscan avahi cups usbmuxd mpd mpv wf-recorder gvfs gvfs-mtp xdg-user-dirs dialog xf86-input-libinput bat micro kitty nwg-look nwg-displays imagemagick python-pygments ghostscript libheif libraw libwmf dvjulibre qt5-base qt6-base qt5-svg qt5-wayland qt6-wayland catfish tumbler thunar-volman thunar-archive-plugin xarchiver thunar-media-tags-plugin ffmpegthumbnailer libgsf libgepub libopenraw lha lrzip lzip lzop p7zip unarj unrar unzip zip tool colordiff diff-so-fancy git-delta glow highlight jq mdcat perl-image-exiftool source-highlight cdrtools html2text antiword odt2txt catdoc cliphist wl-clipboard wlogout grim slurp swappy wf-recorder hyprpicker brightnessctl playerctl kitty thunar
```

## Package env
```
sudo pacman -S clutter libdecor glfw glew
```

## Wine package
```
sudo pacman -S --needed giflib lib32-giflib libpng lib32-libpng libldap lib32-libldap gnutls lib32-gnutls mpg123 lib32-mpg123 openal lib32-openal v4l-utils lib32-v4l-utils libpulse lib32-libpulse libgpg-error lib32-libgpg-error alsa-plugins lib32-alsa-plugins alsa-lib lib32-alsa-lib libjpeg-turbo lib32-libjpeg-turbo sqlite lib32-sqlite libxcomposite lib32-libxcomposite libxinerama lib32-libgcrypt libgcrypt lib32-libxinerama ncurses lib32-ncurses opencl-icd-loader lib32-opencl-icd-loader libxslt lib32-libxslt libva lib32-libva gtk3 lib32-gtk3 gst-plugins-base-libs lib32-gst-plugins-base-libs vulkan-icd-loader lib32-vulkan-icd-loader lib32-acl lib32-libpcap lib32-libnl lib32-gettext dosbox lib32-gst-plugins-base lib32-gst-plugins-good lib32-pcsclite lib32-sdl2 unixodbc lib32-libwebp lib32-libid3tag
```

## Yay Package
```
yay -S tofi ctpv
```

### Install Audio Server [Pipewire](https://wiki.archlinux.org/title/PipeWire)
```
sudo pacman -S pipewire lib32-pipewire pipewire-docs pipewire-audio pipewire-alsa pipewire-jack pipewire-v4l2 pipewire-pulse alsa-utils bluez bluez-utils blueman pavucontrol gst-plugin-pipewire libpipewire lib32-libpipewire libwireplumber qpwgraph wireplumber
```

## Intel CPU/iGPU Model
> [Notes to read about acceleration](https://www.linuxquestions.org/questions/slackware-14/enabling-intel-video-hardware-acceleration-4175721864/)
- Model: `Intel i5-6200U`
- Graphics: `GPU HD Graphics 520`
- Graphics-Gen: `Gen9`

## Nvidia dGPU Model
- Model: `Nvidia Geforce 940MX`
- Codename Family: `NV110(Maxwell)`
- Codename: `NV118 (GM108) GeForce 830M, 840M, 930M, 940MX`
- Review: [TechPowerUp Specs](https://www.techpowerup.com/gpu-specs/geforce-940mx.c2845)

# Configuration
## Useful Links
- [Archlinux Wiki NVIDIA](https://wiki.archlinux.org/title/NVIDIA)
- [Hyprland Nvidia Section](https://wiki.hyprland.org/Nvidia/)

## Install Package
### Intel
>Note: For Nouveau, you only need to see if [Loading](https://wiki.archlinux.org/title/Nouveau#Loading) is correct
```
sudo pacman -S mesa lib32-mesa mesa-utils intel-gmmlib intel-media-driver libva lib32-libva libva-utils libva-mesa-driver lib32-libva-mesa-driver libvpl
```
### Vulkan
```
sudo pacman -S vulkan-intel lib32-vulkan-intel vulkan-icd-loader lib32-vulkan-icd-loader vulkan-mesa-layers lib32-vulkan-mesa-layers vulkan-tools
```

### All GST-Driver
```
sudo pacman -S gst-plugins-ugly gst-plugins-good gst-plugins-base gst-plugins-bad gst-libav libde265 gst-plugin-pipewire gst-plugin-va
```

</details>


## Permissions
```
sudo usermod $USER -aG games,wheel,audio,kvm,optical,storage,uucp,video,wireshark,libvirt,audio,video,adbusers,saned,cups,lp,scanner,usbmux,mpd,input,libvirt-qemu,vboxusers,docker,render
```

## Start Services
```
systemctl enable docker sshd avahi-daemon cups virtqemud libvirtd --now
```

## Audio Server
### Start Pipewire with pulseaudio
```
systemctl enable pipewire-pulse.service --user --now
```

### Unmute from alsa-utils
```
amixer sset Master unmute
amixer sset Speaker unmute
amixer sset Headphone unmute
alsamixer
```

## mkinitcpio
In `/etc/mkinitcpio.conf` copy this [Mkinitcpio](https://wiki.archlinux.org/title/Mkinitcpio#MODULES) Modules
```
i915 kvm kvm_intel virtio-net virtio-blk virtio-scsi virtio-balloon virtio_pci vboxdrv
```

### Remake Mkinitcpio and Grub Config
```
mkinitcpio -p linux
grub-mkconfig -o /boot/grub/grub.cfg
```

## Final Step: REBOOT
```
reboot
```

Now you can go to the [Configuration Guide](/configuration-guide.md) :D

---
# OLD

<details>
 <summary><b>!!! IGNORE THIS !!! Propietary NVIDIA (I dont use it anymore) !!! IGNORE THIS !!!</b></summary>
 <br>

- Now i am using [Nouveau](https://nouveau.freedesktop.org/) because have a good compatibility with my card, work right
- READ THE WIKI AND FORUM AFTER INSTALL ANYTHING
- LIBVDPAU IS BROKEN; DON'T INSTALL IT


> Install Nvidia Package
```
sudo pacman -S dkms nvidia-dkms nvidia-utils lib32-nvidia-utils nvidia-prime nvidia-settings
```

> Install Nvidia Acceleration Layer
> 
> NOTE: Follow [ElFarto nvidia-vaapi-driver config](https://github.com/elFarto/nvidia-vaapi-driver/)
```
sudo pacman -S libva-mesa-driver lib32-libva-mesa-driver mesa-vdpau lib32-mesa-vdpau nvtop meson ffnvcodec-headers
```

> In `/etc/default/grub` at the end of `GRUB_CMDLINE_LINUX_DEFAULT=""` add
> 
> NOTE: i dont know if `nvidia_drm.fbdev=1` works fine
```
nvidia_drm.modeset=1
```

> In `/etc/mkinitcpio.conf` at the `MODULES` section add
>
> NOTE: Also remove `kms` from `HOOKS`
>
> NOTE2: This also dont work good
>
> NOTE3: Without nvidia_modeset seem to work good
```
nvidia nvidia_uvm nvidia_drm
```

> In `/etc/modprobe.d/nvidia.conf` add
```
options nvidia-drm modeset=1
```
> Fix Suspend Wakeup issues
```
sudo systemctl enable nvidia-suspend.service nvidia-hibernate.service nvidia-resume.service
```

</details>

