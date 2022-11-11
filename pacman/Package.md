```
pacman -S bpytop code discord fish lxappearance kitty libreoffice-fresh libreoffice-fresh-es micro nano mousepad mpv smplayer smplayer-skins smplayer-themes picard nomacs obsidian qt5ct lsd bat reflector rsync curl
```
```
yay -S deemix-gui lightscreen
```

- Modificar /etc/pacman/conf
- quitar "#" en ParallelDownload=5

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


Mas informacion sobre lo siguiente en https://www.youtube.com/watch?v=G6Onhz1lLA0
Automatizar este proceso (En el boot)

```
- sudo nano /etc/xdg/reflector/reflector.conf
- sudo sytemctl enable reflector.service
- sudo systemctl start reflector.service
```

Semanal
```
sudo systemctl enable reflector.timer
```
