# Dotfiles
![GitHub](https://img.shields.io/github/license/DeathGabox/DotFiles?color=green&logo=GitBook&logoColor=red&style=for-the-badge)
![GitHub Repo stars](https://img.shields.io/github/stars/DeathGabox/DotFiles?color=9cf&label=Stars%20%3C3&logo=github&logoColor=black&style=for-the-badge)
![GitHub commit activity (branch)](https://img.shields.io/github/commit-activity/m/DeathGabox/DotFiles/main?color=blueviolet&label=Commit&logo=github&logoColor=black&style=for-the-badge)


First of all, thanks to all the wikis, for example [Official Wiki Arch](https://wiki.archlinux.org/), each one is worth reading and helping, this is just a help for me, if it helps you in something, that's great, but don't blindly trust every command, okay?

Take note i use Wayland instead of Xorg, this make different design perpectives and software, examples are [gammastep](https://gitlab.com/chinstrap/gammastep) instead of [Redshift](https://github.com/jonls/redshift) because [issues with wayland](https://github.com/jonls/redshift/issues/55)

The [Install Guide](/installation-guide.md) gives:
- Installation and first reboot
- All necesary package

The [Config Guide](/configuration-guide.md) gives:
- .config and extra configuration

Created to be used in real env, because Hyprland can't work with good performance without GPU passthru | [Info](https://wiki.hyprland.org/Getting-Started/Master-Tutorial/#vm)

---

I love [Hyprland](https://hyprland.org/), and for more scalability, i made [hyprland.conf](/.config/hypr/hyprland.conf) with only include routes to the other .conf files, monitors.conf is managed by [nwg-displays](https://github.com/nwg-piotr/nwg-displays)

```
.config
├── fastfetch
│   └── config.conf
├── hypr
│   ├── bind.conf
│   ├── env.conf
│   ├── exec.conf
│   ├── hyprland.conf
│   ├── monitors.conf
│   ├── variable.conf
│   ├── windowrulev2.conf
│   └── workspaces.conf
├── kitty
│   ├── color.ini
│   └── kitty.conf
├── fastfetch
│   └── config.conf
├── lf
│   └── lfrc
├── qt5ct
│   ├── colors
│   │   └── Catppuccin-Mocha.conf
│   ├── qss
│   └── qt5ct.conf
├── qt6ct
│   ├── colors
│   │   └── Catppuccin-Mocha.conf
│   ├── qss
│   └── qt5ct.conf
└── tofi
    ├── config
    ├── dmenu
    └── soy-milk
```

Mozilla CSS is a bit tricky, see [Configuration Guide](/configuration-guide.md#firefox-config) for more info

```
.mozilla
└── firefox-esr
    └── rycwnmek.default-release
        └── chrome
            ├── userChrome.css
            └── userContent.css

```


FINAL NOTE WIP: When i can finally learn how to make a vertical bar with EWWW, i gonna add screenshot :D

But this is how Terminal look like, Kitty + Hack [Nerd Font](https://www.nerdfonts.com/)
![Fastfetch Screenshot](/.github/assets/Fastfetch-Github.png)
