> Note: This is a forever work in progress

[Notes to read about acceleration](https://www.linuxquestions.org/questions/slackware-14/enabling-intel-video-hardware-acceleration-4175721864/)

- [x] Read The Fabulous Manual ([RTFM](https://es.wikipedia.org/wiki/RTFM)) always, like [Archwiki](https://wiki.archlinux.org/) or Self-doc written by project, this is considered out of date by design

# Info
## Intel
- Model: `Intel i5-6200U`
- Graphics: `GPU HD Graphics 520`
- Graphics-Gen: `Gen9`

## Nvidia
- Model: `Nvidia Geforce 940MX`
- Codename Family: `NV110(Maxwell)`
- Codename: `NV118 (GM108) GeForce 830M, 840M, 930M, 940MX`
- Review: [TechPowerUp Specs](https://www.techpowerup.com/gpu-specs/geforce-940mx.c2845)

# Configuration
## Useful Links
- READ THE WIKI AND FORUM AFTER INSTALL ANYTHING
- LIBVDPAU IS BROKEN; DON'T INSTALL IT
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

## Mkinitcpio
- In `/etc/mkinitcpio.conf` at MODULES, add `i915`
- Edit `/etc/modprobe.d/i915.conf` add `options i915 enable_guc=2`
- `sudo mkinitcpio -p linux`
- `reboot`

> Update Grub and mkinitcpio
```
grub-mkconfig -o /boot/grub/grub.cfg
mkinitcpio --config /etc/mkinitcpio.conf --generate /boot/initramfs-custom.img
mkinitcpio -p linux
```

## Firefox Config 

- [SimpleFox CSS Repo](https://github.com/migueravila/SimpleFox)

> Write in searchbar `about:config` and turn "True" to next params
- `toolkit.legacyUserProfileCustomizations.stylesheets`
- `layers.acceleration.force-enabled`
- `gfx.webrender.all`
- `svg.context-properties.content.enabled`

> Note1: $Firefox-Channel is the firefox Channel you selected, examples `Nightly` `Beta` `Developer` `Normal` `ESR`, maybe it's just non-sense .default folder like: `Firefox -> u0kchxzv.default` `Firefox Developer Edition -> idknp77f.dev-edition-default` `Firefox-ESR -> rycwnmek.default-release`
```
cd ~/.mozilla/$Firefox-Channel/$Firefox-Default/
mkdir chrome
mv ~/Documents/git/dotfiles-gabo/.mozilla/$CSS-Folder/* chrome/
```

## Fish Config
> [!TIP]
> You need to redo all step in root mode to have fisher working well

> [!NOTE]
> Config File Default are
> `~/.config/fish/config.fish` & `~/.config/fish/conf.d/`

### Install Fisher
```
curl -sL https://raw.githubusercontent.com/jorgebucaran/fisher/main/functions/fisher.fish | source && fisher install jorgebucaran/fisher
```

### Plugins
> [!NOTE]
> see more plugins [here](https://github.com/jorgebucaran/awsm.fish)

### Install [Tide](https://github.com/IlanCosman/tide)
```
fisher install IlanCosman/tide@v6
```

### Install [Done](https://github.com/franciscolourenco/done)
```
fisher install franciscolourenco/done
```

### Fish Default Shell
```
chsh -s /bin/fish
```

---
> [!NOTE]
> Move .config with your configurations:
> - Kitty
> - Fastfetch
> - Hyprland
> - qt5ct
> - qt6ct

> [!IMPORTANT]
> To work, you need [Nerd Fonts](https://www.nerdfonts.com/), like HackNerdFont or JetBrains

```
mv ~/Documents/git/dotfiles-gabo/.config ~/.config
```

### THEME

My Favs <3
- Manage GTK Themes [nwg-look](https://github.com/nwg-piotr/nwg-look)
- Manage QT Themes [qt6ct](https://github.com/trialuser02/qt6ct) and [qt5ct](https://github.com/desktop-app/qt5ct) for failback
- Theme GTK [Nordic](https://github.com/EliverLara/Nordic)
- Theme QT [Catppucin](https://github.com/catppuccin/qt5ct)
- Icons [Papirus Icon Theme](https://archlinux.org/packages/extra/any/papirus-icon-theme/)
- Mouse [Volante Cursors](https://github.com/varlesh/volantes-cursors)
- Also this [reddit thread](https://www.reddit.com/r/kde/comments/urug5v/guide_to_a_consistent_application_style_in_plasma/) can help

```
cd /home/$USER/Documentos/github
git clone https://github.com/EliverLara/Nordic.git
sudo mv Nordic/ /usr/share/themes
```

> Cursors
```
cd /home/$USER/Documentos/github
wget https://github.com/ful1e5/BreezeX_Cursor/releases/download/v2.0.0/BreezeX-Black.tar.gz
tar xvf BreezeX-Black.tar.gz
rm -drf BreezeX-Black.tar.gz
sudo mv BreezeX-* /usr/share/icons/
```

> QT
> NOTE: add `QT_QPA_PLATFORMTHEME=qt6ct` to your env file and reboot

<details>
 <summary><b>Configure path to qt6ct User & Root</b></summary>
 <br>

User Files
```
- Configuration path: "/home/deathgabox/.config/qt6ct"
- Shared QSS paths:"/usr/share/qt6ct/qss")
- Shared color scheme paths: "/usr/share/qt6ct/colors")
```

Root Files
```
- Configuration path: "/root/.config/qt6ct"
- Shared QSS paths:"/usr/share/qt6ct/qss")
- Shared color scheme paths:"/usr/share/qt6ct/colors")
```

Colors
```
Catppuccin-Frappe.conf      (Light Mode)
Catppuccin-Latte.conf       (Dark Mode)
Catppuccin-Macchiato.conf   (Darker Mode)
Catppuccin-Mocha.conf       (Darkest Mode)
```

</details>

## TTY
> Clone and Copy Files
```
cd ~/Documents/git
git clone https://github.com/catppuccin/tty.git && cd tty
chmod a+x *.sh
./generate.sh mocha
```
> Edit `/etc/default/grub` and append the stdin of sh script to `GRUB_CMDLINE_LINUX`


## Grub2
> Clone and Copy Files
```
cd /home/$USER/Documentos/git
git clone https://github.com/catppuccin/grub.git && cd grub
sudo cp -r src/* /usr/share/grub/themes/
```
> Edit `/etc/default/grub` and add `GRUB_THEME="/usr/share/grub/themes/catppuccin-macchiato-grub-theme/theme.txt"`
> Next run:
```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

# Extra-Config
## SDDM
### Installation
> Theme [Aur](https://aur.archlinux.org/packages/sddm-theme-tokyo-night)
```
cd ~/Documents/git/dotfiles-gabo/etc/sddm.conf.d/
cat theme.conf > /usr/share/sddm/themes/tokyo-night-sddm/theme.conf
mkdir /etc/sddm.conf.d
cat sddm.conf > /etc/sddm.conf.d/sddm.conf
```

## Qemu
### User-Group
> Info about [Qemu](https://wiki.archlinux.org/title/QEMU)
- In `/etc/libvirt/qemu.conf` ~520-525 line, discomment, change user to $USER
```
user="$USER"
group="libvirt-qemu"
```
### Enable Systemctl
```
systemctl enable libvirtd virtqemud virtstoraged virtnodedevd virtnetworkd --now
```

## Steam
In `commands` per game add:
```
__NV_PRIME_RENDER_OFFLOAD=1 __GLX_VENDOR_LIBRARY_NAME=nvidia %command%
```

## Thunar
[Note](https://wiki.archlinux.org/title/Thunar)
You can navigate network with `smb://, ftp://, ssh://, sftp://, davs://`


# OLD
<details>
 <summary><b>Propietary NVIDIA (I dont use)</b></summary>
 <br>

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
