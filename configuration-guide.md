> Note: This is a forever work in progress

- [x] Read The Fabulous Manual ([RTFM](https://es.wikipedia.org/wiki/RTFM)) always, like [Archwiki](https://wiki.archlinux.org/) , [geento wiki](https://wiki.gentoo.org/wiki/Main_Page) or Self-doc written by project, this repo dotfile guide is considered out of date by design

## Mkinitcpio
- In `/etc/mkinitcpio.conf` at MODULES, add `i915`
- Edit `/etc/modprobe.d/i915.conf` add `options i915 enable_guc=2`
- `sudo mkinitcpio -p linux`
- `reboot`

> Update Grub and mkinitcpio
```
grub-mkconfig -o /boot/grub/grub.cfg
mkinitcpio --config /etc/mkinitcpio.conf --generate /boot/initramfs-custom.img
mkinitcpio -p linux
```

## Firefox Config 

- [SimpleFox CSS Repo](https://github.com/migueravila/SimpleFox), Read [This Guide](https://www.quippd.com/firefox/wiki/useful-customizations/) and This [Reddit Answer](https://www.reddit.com/r/firefox/comments/17hlkhp/comment/k6ogtuv/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button) and [Betterfox - Fastfox.js](https://github.com/yokoffing/Betterfox/blob/main/Fastfox.js)

Write in searchbar `about:config`
> Set to `True`
- `toolkit.legacyUserProfileCustomizations.stylesheets`
- `layers.acceleration.force-enabled`
- `gfx.webrender.all`
- `svg.context-properties.content.enabled`

> PDF Dark Mode (wow)
- `pdfjs.forcePageColors` to `true`
- `pdfjs.pageColorsBackground` to `#202020` | default `Canvas`
- `pdfjs.pageColorsForeground` to `#d1d1d1` | default `CanvasText`

> Vaapi Via FFMPEG Acceleration
- `media.ffmpeg.vaapi.enabled` to `true`

> Smaller Tabs Width
- `browser.tabs.tabMinWidth` to `50`

> Disable Firefox Screenshot
- `extensions.screenshots.disabled` to `true`

> Disable Autoplay
- `media.autoplay.blocking_policy` to `2`

> Set this to `0` to use your own fonts always ^^
- `browser.display.use_document_fonts`

> Disable Webrtc indicator (Set to `False`)
- `privacy.webrtc.legacyGlobalIndicator`

> Make Compact UI (Set to `True`)
- `uc.tweak.context-menu.hide-firefox-account`

> Disable Ugly Suggestion (Set to `False`)
- `browser.urlbar.autoFill`
- `browser.formfill.enable`
- `browser.search.suggest.enabled`
- `extensions.formautofill.addresses.enabled`
- `extensions.formautofill.creditCards.enabled`

> Use more Net cache :D
- `network.buffer.cache.size` to `524288` -> 512KB
- `network.buffer.cache.count` to `128`
- `network.http.max-connections` to `1800`
- `network.http.max-persistent-connections-per-server` to `12`
- `network.http.max-urgent-start-excessive-connections-per-host` to `8`
- `network.http.pacing.requests.burst` to `8`
- `network.http.pacing.requests.min-parallelism` to `8`
- `network.websocket.max-connections` to `400`
- `network.ssl_tokens_cache_capacity` to `32768`

> Fastest Full Screen, this can set to `0` but can generate some troubles :p
- `full-screen-api.warning.timeout` to `20`
- `full-screen-api.warning.delay` to `20`
- `full-screen-api.transition.timeout` to `0`

> Accept more images than webp (kinda deprecated)
- `image.http.accept` to `*/*`

> Warn when close firefox with tabs
- `browser.tabs.warnOnClose` to `true`

> Disable "Update Page" in firefox after an upgrade
- `browser.startup.upgradeDialog.enabled` to `false`

> Disable Automatic pop-up when download is finished
- `browser.download.alwaysOpenPanel` to `false`

> Faster Mouse Wheel
- `mousewheel.default.delta_multiplier_y` to `200`

> Smooth Mouse :D
- `general.smoothScroll.msdPhysics.enabled` to `true`

> Open Bookmark in new tab
- `browser.tabs.loadBookmarksInTabs` to `true`

> Enable More RAM consuming, less HDD (I dont use but help a lot in old machines)
- `browser.cache.disk.enable` to `false`
- `browser.cache.memory.capacity` to `-1` (Unlimited i guess)
- `media.memory_cache_max_size` to bigger number

> What is this ADs?? please disable
- `browser.vpn_promo.enabled` to `false`
- `browser.newtabpage.activity-stream.feeds.recommendationprovider` to `false`
- `extensions.htmlaboutaddons.recommendations.enabled` to `false`

> Disable telemetry
- `browser.discovery.enabled` to `false`
- `datareporting.healthreport.uploadEnabled` to `false`

> Force Secure HTTPS Conection (Break EA.com, well, who cares ;p)
- `security.ssl.require_safe_negotiation` to `true`

> Max GFX.accelerated
- `gfx.canvas.accelerated.cache-items` to `4096` | default `2048`
- `gfx.canvas.accelerated.cache-size` to `1024` | default `256`
- `gfx.content.skia-font-cache-size` to `20` | default `5`

> Note1: $Firefox-Channel is the firefox Channel you selected, examples `Nightly` `Beta` `Developer` `Normal` `ESR`, maybe it's just non-sense .default folder like: `Firefox -> u0kchxzv.default` `Firefox Developer Edition -> idknp77f.dev-edition-default` `Firefox-ESR -> rycwnmek.default-release`
```
cd ~/.mozilla/$Firefox-Channel/$Firefox-Default/
mkdir chrome
mv ~/Documents/git/dotfiles-gabo/.mozilla/$CSS-Folder/* chrome/
```

## Fish Config
> [!TIP]
> You need to redo all step in root mode to have fisher working well

> [!NOTE]
> Config File Default are
> `~/.config/fish/config.fish` & `~/.config/fish/conf.d/`

### Install Fisher
```
curl -sL https://raw.githubusercontent.com/jorgebucaran/fisher/main/functions/fisher.fish | source && fisher install jorgebucaran/fisher
```

### Plugins
> [!NOTE]
> see more plugins [here](https://github.com/jorgebucaran/awsm.fish)

### Install [Tide](https://github.com/IlanCosman/tide)
```
fisher install IlanCosman/tide@v6
```

### Install [Done](https://github.com/franciscolourenco/done)
```
fisher install franciscolourenco/done
```

### Fish Default Shell
```
chsh -s /bin/fish
```

---
> [!NOTE]
> Move .config with your configurations:
> - Kitty
> - Fastfetch
> - Hyprland
> - qt5ct
> - qt6ct

> [!IMPORTANT]
> To work, you need [Nerd Fonts](https://www.nerdfonts.com/), like HackNerdFont or JetBrains

```
mv ~/Documents/git/dotfiles-gabo/.config ~/.config
```

### THEME

My Favs <3
- Manage GTK Themes [nwg-look](https://github.com/nwg-piotr/nwg-look)
- Manage QT Themes [qt6ct](https://github.com/trialuser02/qt6ct) and [qt5ct](https://github.com/desktop-app/qt5ct) for failback
- Theme GTK [Nordic](https://github.com/EliverLara/Nordic)
- Theme QT [Catppucin](https://github.com/catppuccin/qt5ct)
- Icons [Papirus Icon Theme](https://archlinux.org/packages/extra/any/papirus-icon-theme/)
- Mouse [Volante Cursors](https://github.com/varlesh/volantes-cursors)
- Also this [reddit thread](https://www.reddit.com/r/kde/comments/urug5v/guide_to_a_consistent_application_style_in_plasma/) can help

```
cd /home/$USER/Documentos/github
git clone https://github.com/EliverLara/Nordic.git
sudo mv Nordic/ /usr/share/themes
```

> Cursors
```
cd /home/$USER/Documentos/github
wget https://github.com/ful1e5/BreezeX_Cursor/releases/download/v2.0.0/BreezeX-Black.tar.gz
tar xvf BreezeX-Black.tar.gz
rm -drf BreezeX-Black.tar.gz
sudo mv BreezeX-* /usr/share/icons/
```

> QT
> NOTE: add `QT_QPA_PLATFORMTHEME=qt6ct` to your env file and reboot

<details>
 <summary><b>Configure path to qt6ct User & Root</b></summary>
 <br>

User Files
```
- Configuration path: "/home/deathgabox/.config/qt6ct"
- Shared QSS paths:"/usr/share/qt6ct/qss")
- Shared color scheme paths: "/usr/share/qt6ct/colors")
```

Root Files
```
- Configuration path: "/root/.config/qt6ct"
- Shared QSS paths:"/usr/share/qt6ct/qss")
- Shared color scheme paths:"/usr/share/qt6ct/colors")
```

Colors
```
Catppuccin-Frappe.conf      (Light Mode)
Catppuccin-Latte.conf       (Dark Mode)
Catppuccin-Macchiato.conf   (Darker Mode)
Catppuccin-Mocha.conf       (Darkest Mode)
```

</details>

## TTY
> Clone and Copy Files
```
cd ~/Documents/git
git clone https://github.com/catppuccin/tty.git && cd tty
chmod a+x *.sh
./generate.sh mocha
```
> Edit `/etc/default/grub` and append the stdin of sh script to `GRUB_CMDLINE_LINUX`


## Grub2
> Clone and Copy Files
```
cd /home/$USER/Documentos/git
git clone https://github.com/catppuccin/grub.git && cd grub
sudo cp -r src/* /usr/share/grub/themes/
```
> Edit `/etc/default/grub` and add `GRUB_THEME="/usr/share/grub/themes/catppuccin-macchiato-grub-theme/theme.txt"`
> Next run:
```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

# Extra-Config
## SDDM
### Installation
> Theme [Aur](https://aur.archlinux.org/packages/sddm-theme-tokyo-night)
```
cd ~/Documents/git/dotfiles-gabo/etc/sddm.conf.d/
cat theme.conf > /usr/share/sddm/themes/tokyo-night-sddm/theme.conf
mkdir /etc/sddm.conf.d
cat sddm.conf > /etc/sddm.conf.d/sddm.conf
```

## Qemu
### User-Group
> Info about [Qemu](https://wiki.archlinux.org/title/QEMU)
- In `/etc/libvirt/qemu.conf` ~520-525 line, discomment, change user to $USER
```
user="$USER"
group="libvirt-qemu"
```
### Enable Systemctl
```
systemctl enable libvirtd virtqemud virtstoraged virtnodedevd virtnetworkd --now
```

## Steam
With Nouveau `commands` per game is:
```
DRI_PRIME=1 %command%
```

## Thunar
[Note](https://wiki.archlinux.org/title/Thunar)
You can navigate network with `smb://, ftp://, ssh://, sftp://, davs://`
