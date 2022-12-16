# NVIDIA 
## Geforce 940MX

[AL NVIDIA](https://wiki.archlinux.org/title/NVIDIA)

Habilita el repositorio ```Multilib```

Codename ``` NV118 (GM108) 	GeForce 830M, 840M, 930M, 940M[X] ```

- Descargar dependencias para que el video funcione
```
sudo pacman -S nvidia dkms nvidia-utils opencl-nvidia libvdpau
```
- Descargar dependencias lib32
```
sudo pacman -S lib32-libvdpau lib32-nvidia-utils lib32-opencl-nvidia
```

- Instalar apoyo
```
sudo pacman -S egl-wayland gwe libxnvctrl mhwd-nvidia nvidia-dkms nvidia-prime nvidia-settings nvtop mhwd
```
## Nvidia Config

---

## Intel
Install
```
sudo pacman -S intel-gmmlib intel-media-driver intel-ucode libmfx libva-intel-driver libva-utils
```
Dependencias Lib32
```
lib32-libva-intel-driver
```

---
## Mesa/Vulkan
Install
```
sudo pacman -S vulkan-intel
```

Dependencias Lib32
```
lib32-vulkan-intel
```

