
> Configurar teclado en español
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

- Instalar WM
```
pacman -S xorg xorg-server xorg-xinit qtile git
```

- Instalar yay (Gestor AUR)
```
mkdir -p Desktop/$USER/repos
cd !$ 
git clone https://aur.archlinux.org/yay.git
cd yay
exit
makepkg -si
```



```
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





---

---


---

---


[Pacman Arch](https://wiki.archlinux.org/title/Pacman)
[Repositorios](https://wiki.archlinux.org/title/Official_repositories)

Usar repositorios
```
core
extra
community
multilib
```

Optimizar Pacman

- Modificar ``` /etc/pacman/conf ```
- quitar "#" en ``` ParallelDownload=5 ```

---
Instalar Paquetes Principales que uso
```
pacman -S sudo wget ranger htop bpytop kitty python-pygments atool elinks git ffmpegthumbnailer highlight libcaca lynx mediainfo bpytop code discord fish lxappearance-gtk3 libreoffice-fresh libreoffice-fresh-es micro nano mousepad mpv smplayer smplayer-skins smplayer-themes picard nomacs obsidian qt5ct lsd bat reflector rsync curl papirus-icon-theme gtk3 gtk4 firefox-developer-edition firefox-developer-edition-i18n-es-cl pulseaudio zip unzip tar p7zip unrar thunar gvfs tumbler thunar-volman thunar-archive-plugin obsidian discord font-manager gcolor3 cool-retro-term speedtest-cli picard python-dbus android-tools android-udev neovim emacs pkgfile telegram-desktop arandr neofetch catimg chafa nomacs xdotool qtile tldr inkscape noisetorch
```

Instalar Grupos de paquetes
```
pacman -S xorg xorg-server xorg-apps xorg-drivers 
```

Instalar paquetes Necesitados ¿?
``` 
pacman -S --needed base-devel git
```

Instalar Paquetes YAY
```
yay -S deemix-gui-appimage lightscreen mkinitcpio-firmware emptty clight clightd clight-gui-git 
```

Acelerar Pacman con deflector (Elige solo 1)
TOP 10 Velocidad
```
sudo reflector --latest 10 --protocol https --sort rate --save /etc/pacman.d/mirrorlist
```
TOP 10 Actualizado
```
sudo reflector --latest 10 --protocol https --sort age --save /etc/pacman.d/mirrorlist
``` 
TOP 10 Velocidad USA
```
sudo reflector --fastest 10 --country US --protocol https --sort rate --save /etc/pacman.d/mirrorlist
```

[Mas Informacion(Youtube)](https://www.youtube.com/watch?v=G6Onhz1lLA0)
:sparkles: :sparkles: Automatizar este proceso (En el boot) :sparkles: :sparkles:
```
- sudo nano /etc/xdg/reflector/reflector.conf
- sudo sytemctl enable reflector.service
- sudo systemctl start reflector.service
```
Semanal
```
sudo systemctl enable reflector.timer
```
