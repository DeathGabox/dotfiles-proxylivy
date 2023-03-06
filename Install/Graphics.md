# NVIDIA 
## Geforce 940MX
[Gracias](Lista de Links :P)
[AL NVIDIA](https://wiki.archlinux.org/title/NVIDIA)

[Help](https://nvidia.custhelp.com/app/answers/detail/a_id/137/~/linux---editing-your-x-config-file)

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

Aqui iria todo para que funcione, desde initcpio y lo demas


---

## Intel
Install
```
sudo pacman -S intel-gmmlib intel-media-driver intel-ucode libmfx libva-intel-driver libva-utils xf86-video-intel
```
Dependencias Lib32
```
sudo pacman -S lib32-libva-intel-driver
```

---
## Mesa/Vulkan
Install
```
sudo pacman -S vulkan-intel glu libva-mesa-driver mesa mesa-demos mesa-vdpau vulkan-mesa-layers vulkan-radeon vulkan-icd-loader vulkan-devel vulkan-swrast
```

Dependencias Lib32
```
lib32-vulkan-intel lib32-glu lib32-libva-mesa-driver lib32-mesa lib32-mesa-demos lib32-mesa-vdpau lib32-vulkan-mesa-layers lib32-vulkan-radeon lib32-vulkan-icd-loader 
```

