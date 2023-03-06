
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
pacman -S xorg xorg-server qtile git
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
