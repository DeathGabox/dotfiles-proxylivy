> TTY
```
## STOP THEY CHANGED ##
cd /home/$USER/Documentos/git
https://github.com/catppuccin/tty.git && cd tty
chmod a+x *.sh
./generate.sh macchiato
reboot
```

Grub2
```
cd /home/$USER/Documentos/git
git clone https://github.com/catppuccin/grub.git && cd grub
sudo cp -r src/* /usr/share/grub/themes/
descomenta y edita /etc/default/grub
  GRUB_THEME="/usr/share/grub/themes/catppuccin-macchiato-grub-theme/theme.txt"
sudo grub-mkconfig -o /boot/grub/grub.cfg
```
