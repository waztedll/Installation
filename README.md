## Index

- [Configure Pacman](#configure-pacman)
    - [Basic Tweaks](#basic-tweaks)
    - [Chaotic-AUR](#chaotic-aur)
- [Install Packages](#install-packages)
    - [Base Packages](#base-packages)
    - [Environment](#environment)
        - [GNOME](#gnome)
        - [KDE](#kde)
        - [i3](#i3)
        - [Hyprland](#hyprland)
    - [Drivers](#drivers)
        - [Intel](#intel)
        - [AMD](#amd)
        - [Bluetooth](#bluetooth)
        - [Printers](#printers)
    - [Applications](#applications)
        - [General](#general)
        - [Audio](#audio)
        - [Game](#game)
        - [Other](#other)
    - [Flatpak](#flatpak)
    - [AUR](#aur)
    - [Shell](#shell)
        - [Fish](#fish)
        - [Zsh](#zsh)
- [System Modules](#system-modules)
    - [Bootsplash](#bootsplash)
    - [Enable VA-API](#enable-va-api)
        - [Intel graphics](#intel-graphics)
        - [AMD graphics](#amd-graphics)
        - [NVIDIA graphics](#nvidia-graphics)
    - [Zen Kernel](#zen-kernel)
    - [Change GRUB time](#change-grub-time)
    - [Mount Disks](#mount-disks)
    - [Create Swap](#create-swap)
- [Useful Utilities](#useful-utilities)
    - [Ad Block](#ad-block)
    - [Apply Themes](#apply-themes)
        - [GTK](#gtk)
        - [QT](#qt)
    - [Backup Files](#backup-files)
    - [Change Keyboard Layout on X11](#change-keyboard-layout-on-x11)
    - [Configure Touchpad on X11](#configure-touchpad-on-x11)
    - [Connect to Wi-Fi](#connect-to-wi-fi)
    - [Dictionary](#dictionary)
    - [Disable Wayland in GDM](#disable-wayland-in-gdm)
    - [DPI Bypass](#dpi-bypass)
    - [Prism Launcher Offline Bypass](#prism-launcher-offline-bypass)
    - [Remove the Wrong Password Delay](#remove-the-wrong-password-delay)
    - [Setup Gaming Environment](#setup-gaming-environment)
    - [Show the Stars on sudo Password](#show-the-stars-on-sudo-password)
    - [Tuxi Config Fix](#tuxi-config-fix)
- [Error Solutions](#error-solutions)
    - [Pacman gives PGP error](#pacman-pgp-error)
    - [Bluetooth not working](#bluetooth-not-working)
    - [Controller doesn't connect to the PC](#controller-not-connecting)
    - [Controller asks for a PIN code](#controller-asks-pin)
    - [Notifications not working correctly on KDE](#notification-issue-kde)
    - [Clipboard not working correctly on KDE](#clipboard-issue-kde)
- [Firefox Tweaks](#firefox-tweaks)
    - [about:config](#firefox-config)

## Configure Pacman

### Basic Tweaks

enable multilib, detailed process, parallel downloads, and make pacman more colorful

    sudo sed -i "/#Color/s/^#//g" /etc/pacman.conf; sudo sed -i "/#VerbosePkgLists/s/^#//g" /etc/pacman.conf; sudo sed -i "/#ParallelDownloads = 5/s/^#//g" /etc/pacman.conf; sudo sed -i "90,91s/#//" /etc/pacman.conf; echo "ILoveCandy" | sudo sed -i "34i\ILoveCandy" /etc/pacman.conf

update pacman to see the effects

    sudo pacman -Syu

### Chaotic-AUR

download required packages

    sudo pacman-key --recv-key 3056513887B78AEB --keyserver keyserver.ubuntu.com && sudo pacman-key --lsign-key 3056513887B78AEB && sudo pacman -U --noconfirm 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-keyring.pkg.tar.zst' 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-mirrorlist.pkg.tar.zst'

enable repo

    echo -e "\n[chaotic-aur]\nInclude = /etc/pacman.d/chaotic-mirrorlist" | sudo tee -a /etc/pacman.conf; sudo pacman -Syu --noconfirm

## Install Packages

### Base Packages

    sudo pacman -S --needed \
            inxi linux-headers man-db systemd-resolvconf tldr git base-devel yay scrcpy yt-dlp fzf ytfzf ani-cli \
            iwd xorg xorg-server xorg-xauth xf86-input-libinput netctl dialog bind net-tools wget curl ncdu xdg-utils \
            android-tools neofetch fastfetch pfetch zip unzip 7zip unrar make libva libva-utils lm_sensors ffmpeg \
            cmatrix rsync vi vim neovim starship tlp qt5ct qt6ct gnome-keyring translate-shell glfw openal \
            ttf-hack ttf-hack-nerd otf-font-awesome ttf-jetbrains-mono-nerd noto-fonts-emoji lsb-release inetutils \
            network-manager-applet ffmpegthumbnailer tumbler tgpt acpi tree joyutils fdupes recode jq pup \
            python-pip python-requests kvantum kvantum-qt5 redshift imagemagick htop btop gvfs gvfs-mtp gvfs-gphoto2 gvfs-afc mtpfs \
            pacman-contrib thefuck cava mat2 libnotify zenity rate-mirrors heimdall-grimler-git libimobiledevice ifuse

> Enable `tlp` if it's not enabled.
>
>     sudo systemctl enable --now tlp.service

### Environment

<details id="gnome">
    <summary><strong>GNOME</strong></summary>

    yay -S --needed \
            gnome-shell gnome-control-center gnome-tweaks gnome-browser-connector gnome-menus \
            gnome-weather gnome-bluetooth-3.0 power-profiles-daemon switcheroo-control dconf-editor \
            gnome-calculator polkit-gnome extension-manager gdm gdm-settings

> Enable `switcheroo-control` if it's not enabled.
>
>     sudo systemctl enable --now switcheroo-control.service

</details>

<details id="kde">
    <summary><strong>KDE</strong></summary>

    yay -S --needed plasma-desktop

</details>

<details id="i3">
    <summary><strong>i3</strong></summary>

    yay -S --needed \
            i3 polybar rofi picom dunst scrot slop xsel xcolor xwallpaper \
            xorg-xbacklight clipmenu redshift playerctl lxappearance polkit-gnome \
            tesseract tesseract-data-eng tesseract-data-tur tesseract-data-rus tesseract-data-deu

</details>

<details id="hyprland">
    <summary><strong>Hyprland</strong></summary>

    yay -S --needed \
            hyprland hyprpaper hyprlock hyprpicker waybar dunst grim slurp \
            nwg-look wl-clipboard cliphist qt5-wayland qt6-wayland rofi-wayland \
            tesseract tesseract-data-eng tesseract-data-tur tesseract-data-rus \
            tesseract-data-deu wlrobs-hg wlogout gtk-layer-shell brightnessctl \
            playerctl wireplumber pamixer polkit-gnome 

</details>

### Drivers

<details id="intel">
    <summary><strong>Intel</strong></summary>

    yay -S --needed \
            mesa-amber lib32-mesa-amber libva-intel-driver lib32-libva-intel-driver intel-media-driver \
            xf86-video-intel vulkan-intel lib32-vulkan-intel vulkan-icd-loader lib32-vulkan-icd-loader intel-gpu-tools

</details>

<details id="amd">
    <summary><strong>AMD</strong></summary>

    yay -S --needed \
            mesa lib32-mesa xf86-video-amdgpu vulkan-radeon lib32-vulkan-radeon vulkan-icd-loader lib32-vulkan-icd-loader hsa-rocr

</details>

<details id="bluetooth">
    <summary><strong>Bluetooth</strong></summary>

    yay -S --needed bluez bluez-utils blueman && systemctl enable --now bluetooth

</details>

<details id="printers">
    <summary><strong>Printers</strong></summary>

    yay -S --needed cups cups-pdf system-config-printer && systemctl enable --now cups

</details>

### Applications

<details id="general">
    <summary><strong>General</strong></summary>

    yay -S --needed \
            firefox epiphany ungoogled-chromium-bin alacritty thunar obsidian syncthing \
            anki localsend pavucontrol discord thunderbird obs-studio piper qbittorrent \
            xsensors xarchiver thunar-volman thunar-archive-plugin thunar-media-tags-plugin \
            gtkhash-thunar gnome-system-monitor viewnior gimp steam lutris umu-launcher \
            heroic-games-launcher-git mpv mpv-mpris upscayl youtube-music-git evince marker \
            keepassxc ventoy lact wine-stable

</details>

<details id="audio">
    <summary><strong>Audio</strong></summary>

    yay -S --needed easyeffects audacity lsp-plugins-lv2 calf; curl -LO https://github.com/Rikorose/DeepFilterNet/releases/download/v0.5.6/libdeep_filter_ladspa-0.5.6-x86_64-unknown-linux-gnu.so; sudo mv -v libdeep_filter_ladspa-0.5.6-x86_64-unknown-linux-gnu.so /usr/lib64/ladspa/libdeep_filter_ladspa.so

</details>

<details id="game">
    <summary><strong>Game</strong></summary>

    yay -S --needed 0ad osu mindustry wesnoth openttd openrct2 openra openloco openage granatier dol-git

</details>

<details id="other">
    <summary><strong>Other</strong></summary>

    yay -S --needed \
            kdenlive krita antimicrox bitwarden goverlay qdirstat celluloid epiphany \
            signal-desktop element-desktop zathura zathur-pdf-poppler vscodium kdeconnect gallery-dl kdiskmark kweather \
            tor-browser-bin librewolf octopi ferium prismlauncher modrinth-app pinta \
            duckstation-git hypnotix ruffle-git lightspark notesnook-bin logseq-desktop-bin \
            stremio discover-overlay mousai songrec soundux tokodon kdevelop davinci-resolve \
            handbrake ppsspp rustdesk parsec calibre dino wike dissent amberol harmonoid cpu-x \
            github-desktop protonlaunch minecraft-launcher mcpelauncher-linux-git video-downloader \
            waypaper-git vlc shotcut flowblade olive vidcutter neovide edex-ui wireshark hardinfo \
            pamac-aur ksysguard gnome-dictionary dialect waydroid zed screenkey veracrypt lmms ardour \
            authenticator xdman-beta-bin john tradingview solaar logiops

</details>

### Flatpak

    yay -S --needed flatpak && flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo && flatpak install com.github.tchx84.Flatseal io.gitlab.jstest_gtk.jstest_gtk com.github.k4zmu2a.spacecadetpinball

### AUR

    yay -S --needed \
            sklauncher-bin fluent-reader-electron-bin kando-bin nuclear-player-bin bifrost-bin hydra-launcher-bin \
            tuxi-git urn-git sherlock-git protonvpn-cli-community lyrebird fast hydroxide varia tty-clock odin4-cli xclicker \
            mangayomi-linux

### Shell

<details id="fish">
    <summary><strong>Fish</strong></summary>

run each one respectively

    sudo pacman -S fish fisher
    fisher install IlanCosman/tide@v6
    chsh -s /usr/bin/fish

</details>

<details id="zsh">
    <summary><strong>Zsh</strong></summary>

first, install zsh and change default shell to zsh

    sudo pacman -S zsh zsh-completions
    chsh -s /usr/bin/zsh

then clone required pluginsㅤ

    git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions && git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting && git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k

ㅤlastly edit zsh config and include the plugins

    nvim ~/.zshrc

/plugins
- `plugins=(git zsh-autosuggestions zsh-syntax-highlighting)`

/ZSH_THEME
- `ZSH_THEME="powerlevel10k/powerlevel10k"`

      source .zshrc

</details>

## System Modules

### Bootsplash

- start by installing `plymouth` package

      sudo pacman -S --needed plymouth

- edit `/etc/mkinitcpio.conf` and add `plymouth` to your hooks after `udev`
- regenerate the images by running

      sudo mkinitcpio -P

- now edit your bootloader config and append `quiet splash loglevel=0 udev.log_level=3` to your cmdline. the result should look like this in limine

      cmdline: cryptdevice=PARTUUID=d5dd7183-f8df-4b85-9b39-a634174f56ce:root root=/dev/mapper/root rw quiet splash loglevel=0 udev.log_level=3 rootfstype=ext4

now it is time to select your plymouth theme

- list themes by running

      plymouth-set-default-theme -l

- optional: remove unnecessary stuff to make it more cleaner

      sudo rm -f /usr/share/plymouth/themes/spinner/animation-*.png
      sudo rm -f /usr/share/plymouth/themes/spinner/throbber-*.png

- set default theme & regenerate kernel images

      sudo plymouth-set-default-theme -R spinner

now you can reboot and see if plymouth has successfully installed and our configurations applied

### Enable VA-API

> override the gpu driver for VA-API via `/etc/environment`

<details id="intel-graphics">
    <summary><strong>Intel graphics</strong></summary>

    LIBVA_DRIVER_NAME=i965 # for libva-intel-driver
    LIBVA_DRIVER_NAME=iHD # for intel-media-driver

</details>

<details id="amd-graphics">
    <summary><strong>AMD graphics</strong></summary>

    LIBVA_DRIVER_NAME=radeonsi # for AMDGPU driver

</details>

<details id="nvidia-graphics">
    <summary><strong>NVIDIA graphics</strong></summary>

    LIBVA_DRIVER_NAME=nouveau # for Nouveau
    LIBVA_DRIVER_NAME=vdpau # for NVIDIA VDPAU
    LIBVA_DRIVER_NAME=nvidia # for NVIDIA NVDEC

</details>

### Zen Kernel

download required packages

    sudo pacman -S --needed linux-zen linux-zen-headers

then adjust GRUB for the zen kernel

    sudo sed -i "s/GRUB_DEFAULT=0/GRUB_DEFAULT=saved/g" /etc/default/grub; sudo sed -i "/#GRUB_SAVEDEFAULT=true/s/^#//g" /etc/default/grub

update GRUB

    sudo grub-mkconfig -o /boot/grub/grub.cfg

reboot to bootloader and select the `linux-zen` kernel. on the next, time it will automatically select the zen kernel

### Change GRUB time

> to skip the 5 second hold

    sudo sed -i "s/GRUB_TIMEOUT=5/GRUB_TIMEOUT=0/g" /etc/default/grub

update GRUB and reboot

    sudo grub-mkconfig -o /boot/grub/grub.cfg; reboot

### Mount Disks

first, creating the mount folder
> replace `Storage` with whatever you want

    sudo mkdir -p /mnt/Storage

copy the UUID by listing disks

    lsblk -f
    
write UUID to the appropriate place
> in this example, the ntfs used for the disk used by Windows

<pre style="margin-bottom: 0px; border-bottom: medium; padding-bottom: 0.8em; --darkreader-inline-border-bottom: currentcolor;" data-darkreader-inline-border-bottom="">/etc/fstab</pre>
<pre style="margin-top: 0; border-top-style:dashed; padding-top: 0.8em;">UUID=paste_uuid_here              /mnt/Storage     ntfs     defaults      0 0</pre>

make the system recognize the new disk

    sudo systemctl daemon-reload; sudo mount -a

### Create Swap

create a swap file

    sudo dd if=/dev/zero of=/swapfile bs=1M count=4096

change the permissions

    sudo chmod 600 /swapfile

make swap

    sudo mkswap /swapfile

enable the swap

    sudo swapon /swapfile

verify the process

    swapon --show

paste swap to end of the file

<pre style="margin-bottom: 0px; border-bottom: medium; padding-bottom: 0.8em; --darkreader-inline-border-bottom: currentcolor;" data-darkreader-inline-border-bottom="">/etc/fstab</pre>
<pre style="margin-top: 0; border-top-style:dashed; padding-top: 0.8em;">/swapfile                                 none           swap    defaults         0 0</pre>

reboot to see changes

> if you want to delete the swap, just type

    sudo swapoff -v /swapfile && sudo rm /swapfile

## Useful Utilities

### Ad Block

    sudo curl -o /etc/hosts https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts

### Apply Themes

<details id="gtk">
    <summary><strong>GTK</strong></summary>

> Dracula GTK: <https://github.com/dracula/gtk/archive/master.zip>

- download the $THEME and extract the .zip file to the `~/.themes`
- open up the `lxappearance` and select the $THEME in widgets.

</details>

<details id="qt">
    <summary><strong>QT</strong></summary>

> Dracula QT: <https://github.com/dracula/qt5/archive/master.zip>

- download the $THEME and extract the anywhere
- open up the `kvantum` and select the folder that includes $THEME and install it
- click the change theme and select the $THEME
- open up the `qt5ct` and `qt6ct` and select the `kvantum`

</details>

### Backup Files

backup the files using rsync

    rynsc -av --delete /path/to/files/ /path/to/backup/

### Change Keyboard Layout on X11

<pre style="margin-bottom: 0px; border-bottom: medium; padding-bottom: 0.8em; --darkreader-inline-border-bottom: currentcolor;" data-darkreader-inline-border-bottom="">/etc/X11/xorg.conf.d/00-keyboard.conf</pre>
<pre style="margin-top: 0; border-top-style:dashed; padding-top: 0.8em;">
Section "InputClass"
    Option "XkbLayout" "tr,us"
    Option "XkbOptions" "grp:alt_shift_toggle"
    ...
EndSection
</pre>

### Configure Touchpad on X11

<pre style="margin-bottom: 0px; border-bottom: medium; padding-bottom: 0.8em; --darkreader-inline-border-bottom: currentcolor;" data-darkreader-inline-border-bottom="">/etc/X11/xorg.conf.d/30-touchpad.conf</pre>
<pre style="margin-top: 0; border-top-style:dashed; padding-top: 0.8em;">
Section "InputClass"
    Identifier "touchpad"
    Driver "libinput"
    MatchIsTouchpad "on"
    Option "Tapping" "on"
    Option "NaturalScrolling" "on"
    Option "ScrollMethod" "edge"
    ...
EndSection
</pre>

see more [here](https://man.archlinux.org/man/libinput.4.en.txt)

### Connect to Wi-Fi

via `NetworkManager`

    $ nmcli device status
    $ nmcli device wifi list
    $ nmcli device wifi connect <SSID> password <password>
    $ nmcli general status

via `iwctl`

    [iwd]# device list
    [iwd]# adapter phy0 set-property Powered on
    [iwd]# device wlan0 set-property Powered on
    [iwd]# station wlan0 scan
    [iwd]# station wlan0 get-networks
    [iwd]# station wlan0 connect <network>
    [iwd]# station wlan0 show

### Dictionary

download the database

    wget https://github.com/metwse/rofi-tdk.sh/releases/download/v1/rofi-tdk.tar.gz

then move it into the required directory

    sudo mv ~/rofi-tdk.tar.gz /var/

### Disable Wayland in GDM

> [!NOTE]
> This will disable all wayland sessions in GDM

    sudo sed -i "/#WaylandEnable=false/s/^#//g" /etc/gdm/custom.conf

### DPI Bypass

    git clone https://github.com/bol-van/zapret
    cd zapret

check and install

    sudo ./install_bin.sh
    sudo ./blockcheck.sh
    sudo ./install_easy.sh

### Prism Launcher Offline Bypass

    echo '{"accounts": [{"entitlement": {"canPlayMinecraft": true,"ownsMinecraft": true},"type": "Offline"}],"formatVersion": 3}' > ~/.local/share/PrismLauncher/accounts.json

### Remove the Wrong Password Delay

to remove the boring delay after entering wrong password, edit `/etc/pam.d/system-auth` and add `nodelay` at end of the every line that starts with `auth` and includes `pam_faillock.so` or `pam_unix.so`

<pre style="margin-bottom: 0px; border-bottom: medium; padding-bottom: 0.8em; --darkreader-inline-border-bottom: currentcolor;" data-darkreader-inline-border-bottom="">/etc/pam.d/system-auth</pre>
<pre style="margin-top: 0; border-top-style:dashed; padding-top: 0.8em;">
auth       required                    pam_faillock.so      preauth nodelay                                                
auth       [success=2 default=ignore]  pam_unix.so          try_first_pass nullok nodelay                                  
-auth      [success=1 default=ignore]  pam_systemd_home.so                                                                 
auth       [default=die]               pam_faillock.so      authfail nodelay
...
</pre>

### Setup Gaming Environment

### Show the Stars on sudo Password

    echo "Defaults pwfeedback" | sudo tee -a /etc/sudoers

### Tuxi Config Fix

> ready binary here: <https://gist.github.com/waztedll/0d3856ca7e583949ace73245a234f5d4>

    sudo sed -i '18c\[ -n "$TUXI_LANG" \] && LANGUAGE="$TUXI_LANG" || LANGUAGE="tr"' /usr/bin/tuxi && sudo sed -i '886c\user_agent="Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) QtWebEngine/5.15.2 Chrome/87.0.4280.144 Safari/537.36"' /usr/bin/tuxi

## Error Solutions

<details id="pacman-pgp-error">
    <summary><strong>Pacman gives PGP error</strong></summary>

    sudo pacman -S --noconfirm --needed archlinux-keyring && sudo pacman-key --refresh-keys

</details>

<details id="bluetooth-not-working">
    <summary><strong>Bluetooth not working</strong></summary>

    rfkill list
    rfkill unblock bluetooth
    systemctl status bluetooth
    sudo systemctl start bluetooth
    systemctl status bluetooth

</details>

<details id="controller-not-connecting">
    <summary><strong>Controller doesn't connect to the PC</strong></summary>

    $ bluetoothctl
    [bluetoothctl#] power on
    [bluetoothctl#] agent on
    [bluetoothctl#] default-agent
    [bluetoothctl#] scan on
    [bluetoothctl#] devices
    [bluetoothctl#] pair <gamepad>
    [bluetoothctl#] connect <gamepad>
    [bluetoothctl#] trust <gamepad>
    [bluetoothctl#] scan off
    [bluetoothctl#] exit

</details>

<details id="controller-asks-pin">
    <summary><strong>Controller asks for a PIN code</strong></summary>

    echo -e "[General]\nClassicBondedOnly=false\nUserspaceHID=false" | sudo tee /etc/bluetooth/input.conf

</details>

<details id="notification-issue-kde">
    <summary><strong>Notifications not working correctly on KDE</strong></summary>

    sudo pacman -S knotifications5 knotifyconfig5
  
go to settings -> notifications then enable all authentication pushs

</details>

<details id="clipboard-issue-kde">
    <summary><strong>Clipboard not working correctly on KDE</strong></summary>

go to clipboard setings and set keyboard shortcut "Show Items at Mouse Posittion"

</details>

## Firefox Tweaks

<details id="firefox-config">
    <summary><strong>about:config</strong></summary>

```
### Necessary

beacon.enabled = false
browser.cache.offline.enable = false
browser.send_pings = false
browser.urlbar.speculativeConnect.enabled = false
dom.battery.enabled = false
dom.event.contextmenu.enabled = false
dom.event.clipboardevents.enabled = false
dom.private-attribution.submission.enabled = false
extensions.pocket.enabled = false
media.eme.enabled = false
media.navigator.enabled = false
network.IDN_show_punycode = true
privacy.firstparty.isolate = true
privacy.resistFingerprinting = true
toolkit.telemetry.cachedClientID = blank

### For Google tracking

geo.enabled = false
geo.wifi.uri = blank
browser.search.geoip.url = blank

### For escaping from FBI

browser.safebrowsing.enabled = false
browser.safebrowsing.phishing.enabled = false
browser.safebrowsing.malware.enabled = false
browser.safebrowsing.downloads.enabled = false
browser.safebrowsing.downloads.remote.enabled = false
browser.safebrowsing.provider.google4.dataSharing.enabled = false
browser.safebrowsing.provider.google4.updateURL = blank
browser.safebrowsing.provider.google4.reportURL = blank
browser.safebrowsing.provider.google4.reportPhishMistakeURL = blank
browser.safebrowsing.provider.google4.reportMalwareMistakeURL = blank
browser.safebrowsing.provider.google4.lists = blank
browser.safebrowsing.provider.google4.gethashURL = blank
browser.safebrowsing.provider.google4.dataSharingURL = blank
browser.safebrowsing.provider.google4.dataSharing.enabled = false
browser.safebrowsing.provider.google4.advisoryURL = blank
browser.safebrowsing.provider.google4.advisoryName = blank
browser.safebrowsing.provider.google.updateURL = blank
browser.safebrowsing.provider.google.reportURL = blank
browser.safebrowsing.provider.google.reportPhishMistakeURL = blank
browser.safebrowsing.provider.google.reportMalwareMistakeURL = blank
browser.safebrowsing.provider.google.pver = blank
browser.safebrowsing.provider.google.lists = blank
browser.safebrowsing.provider.google.gethashURL = blank
browser.safebrowsing.provider.google.advisoryURL = blank
browser.safebrowsing.downloads.remote.url = blank
```

</details>

<a href="#top">Back to top</a>
