I use [Qtile](http://www.qtile.org/)
Recomiendan [Hacer esto](https://github.com/qtile/qtile/wiki/wallpapers)

---

Mi configuracion
Usar nitrogen
- Instalar
```
pacman -S nitrogen
```
- Hacer un archivo de autoarranque
``` micro ~/.config/qtile/autostart.sh``` y escribe en la primera linea ```#!/bin/sh``` y en la segunda ```nitrogen --restore &``` sal de editar, ejecuta ```chmod +x ~/.config/qtile/autostart.sh```

- Hacer que el archivo de autoarranque lo ejecute qtile
Modifica ``` Config File```
Y escribe
```
import os
import subprocess

from libqtile import hook

@hook.subscribe.startup_once
def autostart():
    home = os.path.expanduser('~/.config/qtile/autostart.sh')
    subprocess.Popen([home])
```
