# Dotfiles
Config Files :D
$USER == Usuario

---
Install
```
sudo su
setxkbmap es
useradd -m $USER
passwd $USER
passwd root
usermod -aG wheel $USER
grub-install /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg
echo "Hostname" > /etc/hostname
systemctl start NetworkManager.service
systemctl enable NetwokManager
systemctl start wpa_supplicant.service
systemctl enable wpa_supplicant.service
fc-cache -f -v
timedatectl set-ntp true
timedatectl set-timezone America/Santiago
amixer sset Master unmute
amixer sset Speaker unmute
amixer sset Headphone unmute
alsamixer
mkdir -p /home/$USER/Documentos/github
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
```
```
sudo su
- /etc/sudoers
- - Modifica TANTO
- /etc/vconsole.conf
- - Modifica TANTO
- /etc/hosts
- - Modifica TANTO
- /etc/locale.gen
- - modifica TANTO
- - - locale-gen
```
PONER LOS WGET de los archivos
