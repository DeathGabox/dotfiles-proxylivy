[Pacman Arch](https://wiki.archlinux.org/title/Pacman)
[Repositorios](https://wiki.archlinux.org/title/Official_repositories)

Optimizar Pacman
```
- Modificar /etc/pacman/conf
- quitar "#" en ParallelDownload=5
```
---
```
pacman -S atool elinks git ffmpegthumbnailer highlight libcaca lynx mediainfo bpytop code discord fish lxappearance-gtk3 kitty libreoffice-fresh libreoffice-fresh-es micro nano mousepad mpv smplayer smplayer-skins smplayer-themes picard nomacs obsidian qt5ct lsd bat reflector rsync curl
```
``` 
pacman -S --needed base-devel git
```
```
yay -S deemix-gui lightscreen
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
