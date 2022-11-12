# Dotfiles
Config Files :D


---
Install
```
sudo su
setxkbmap es
mkdir -p /home/deathgabox/Documentos/github
cd $!
git clone https://aur.archlinux.org/yay.git
cd yay
exit
makepkg -si
sudo su
cd ..
mkdir blackarch
cd blackarch/
curl -0 https://blackarch.org/strap.sh
chmod +x strap.sh
sudo ./strap.sh
cd /usr/share/fonts

```
```
sudo su
- /etc/sudoers
- - Modifica TANTO
- /etc/vconsole.conf
- - Modifica TANTO
```
