I USE https://github.com/catppuccin/qt5ct

### Tutorial
Edita con `sudo micro /etc/environment` & add the line `QT_QPA_PLATFORMTHEME=qt5ct` and save. After `reboot`

Install
```
sudo su
cd /home/deathgabox/Documentos/Git
git clone https://github.com/catppuccin/qt5ct.git
cd qt5ct/themes/
mkdir -p ~/.config/qt6ct/colors/
cp Catppuccin-Mocha.conf /usr/share/qt6ct/colors/
cp Catppuccin-Mocha.conf ~/.config/qt6ct/colors/
**Configure qt6ct user & root**
```

Colors
```
Catppuccin-Frappe.conf      (Light Mode)
Catppuccin-Latte.conf       (Dark Mode)
Catppuccin-Macchiato.conf   (Darker Mode)
Catppuccin-Mocha.conf       (Darkest Mode)
```

---
USER
Configuration path: "/home/deathgabox/.config/qt6ct"
Shared QSS paths:"/usr/share/qt6ct/qss")
Shared color scheme paths: "/usr/share/qt6ct/colors")

---
ROOT
Configuration path: "/root/.config/qt6ct"
Shared QSS paths:"/usr/share/qt6ct/qss")
Shared color scheme paths:"/usr/share/qt6ct/colors")
