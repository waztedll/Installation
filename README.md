## Contents

- [Configure Pacman](#configure-pacman)
    - [Basic Tweaks](#basic-tweaks)
    - [Chaotic AUR](#chaotic-aur)
- [Packages to Install](#packages-to-install)
    - [Necessary Packages](#necessary-packages)
    - [Applications](#applications)
        - [General](#general)
        - [Audio](#audio)
        - [Other](#other)
        - [Game](#game)
    - [Flatpak](#flatpak)
    - [AUR](#aur)
    - [Window Manager](#window-manager)
        - [i3](#i3)
        - [Hyprland](#hyprland)
    - [Shell](#shell)
        - [Fish](#fish)
        - [Zsh](#zsh)
- [System Modules](#system-modules)
    - [Zen Kernel](#zen-kernel)
    - [Changing GRUB time](#changing-grub-time)
    - [Changing Limine time](#changing-limine-time)
    - [Mounting Disk](#mounting-disk)
    - [Adding SWAP](#adding-swap)
- [Useful Things](#useful-things)
    - [Connect to Wi-Fi](#connect-to-wi-fi)
    - [Install Driver](#install-driver)
        - [Intel](#intel)
        - [AMD](#amd)
        - [Bluetooth](#bluetooth)
        - [Printers](#printers)
    - [Apply Themes](#apply-themes)
        - [GTK](#gtk)
        - [QT](#qt)
    - [Backup Files](#backup-files)
    - [DPI Bypass](#dpi-bypass)
    - [Adblock](#adblock)
    - [Dictionary](#dictionary)
    - [Show Stars on Sudo Password](#show-stars-on-sudo-password)
    - [Tuxi Config Fix](#tuxi-config-fix)
    - [Prism Launcher Offline Bypass](#prism-launcher-offline-bypass)
- [Error Solutions](#error-solutions)
    - [If pacman gives PGP error](#if-pacman-gives-pgp-error)
    - [If bluetooth not working](#if-bluetooth-not-working)
    - [If controller doesn't connect to PC](#if-controller-doesnt-connect-to-pc)
    - [If controller asks for PIN code](#if-controller-asks-for-pin-code)
    - [If notifications not work correctly on KDE](#if-notifications-not-work-correctly-on-kde)
    - [If clipboard not work correctly](#if-clipboard-not-work-correctly)
- [Firefox Config](#firefox-config)

## Configure Pacman

### Basic Tweaks

Install vim and start

    sudo pacman -S vim --noconfirm && sudo vim /etc/pacman.conf

Remove # on

`Color`  
`Parallel Downloads = 5`
    
`[multilib]`  
`Include = /etc/pacman.d/mirrorlist`

add  

    ILoveCandy

then update pacman

    sudo pacman -Syu

### Chaotic AUR

firstly, downloading required packages

    sudo pacman-key --recv-key 3056513887B78AEB --keyserver keyserver.ubuntu.com && sudo pacman-key --lsign-key 3056513887B78AEB && sudo pacman -U 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-keyring.pkg.tar.zst' 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-mirrorlist.pkg.tar.zst' --noconfirm

then editing the pacman config

    sudo vim /etc/pacman.conf

include this codes

    [chaotic-aur]  
    Include = /etc/pacman.d/chaotic-mirrorlist

## Packages to Install

### Necessary Packages:

    sudo pacman -S inxi linux-headers man-db git base-devel yay fast pup scrcpy yt-dlp ytfzf \
                   netctl dialog bind recode net-tools jq wget locate htop btop android-tools \
                   fastfetch pfetch zip unzip p7zip unrar make gvfs libva xsensors cmatrix \
                   rsync vi vim neovim starship tlp qt5ct qt6ct gnome-keyring firefox-pwa fzf \
                   ttf-hack ttf-hack-nerd otf-font-awesome ttf-jetbrains-mono-nerd noto-fonts-emoji neofetch \
                   translate-shell lsb-release network-manager-applet wine-stable kdialog \
                   ffmpegthumbnailer tumbler brightnessctl playerctl pipewire pipewire-pulse \
                   python-requests wireplumber pamixer pavucontrol kvantum kvantum-qt5 mpv mpv-mpris mtpfs \
                   gvfs-mtp pacman-contrib thefuck cava tty-clock xdg-desktop-portal xdg-desktop-portal-gtk \
                   rate-mirrors --needed

> don't forget the enable tlp
>
>     sudo systemctl enable --now tlp.service

### Applications

#### General:

    yay -S firefox alacritty pamac-nosnap bitwarden thunar anki syncthing \
           kdeconnect kdiskmark thunderbird obs-studio piper qbittorrent cpu-x \
           vscodium discord ventoy thunar-volman thunar-archive-plugin \
           kweather ksysguard gnome-system-monitor viewnior krita steam upscayl \
           ungoogled-chromium youtube-music-git metadata-cleaner gnome-dictionary \
           dialect okular obsidian marker qmmp protonvpn-cli \
           xarchiver neovide jre-openjdk --needed

#### Audio:

    yay -S easyeffects audacity lsp-plugins-lv2

#### Other:

    yay -S gimp kdenlive antimicrox goverlay qdirstat celluloid kitty epiphany \
           signal-desktop nuclear-player-bin xdman lutris heroic-games-launcher-bin \
           tor-browser-bin librewolf epiphany octopi prismlauncher video-downloader \
           duckstation-git hypnotix ruffle-git lightspark notesnook-bin logseq-desktop-bin \
           stremio armcord discover-overlay mousai songrec soundux tokodon kdevelop \
           handbrake 0ad osu ppsspp rustdesk parsec calibre dino wike gtkcord4 cpu-x \
           github-desktop harmonoid davinci-resolve protonlaunch mcpelauncher-ui \
           waypaper-git shotcut flowblade olive vidcutter neovide edex-ui wireshark \
           hardinfo tgpt

#### Game:

    yay -S mindustry wesnoth granatier dol-git

### Flatpak:

    yay -S flatpak && flatpak --user remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo && flatpak install com.github.tchx84.Flatseal com.github.k4zmu2a.spacecadetpinball io.gitlab.jstest_gtk.jstest_gtk

### AUR:

    yay -S tuxi-git urn-git lyrebird sklauncher-bin localsend-bin fluent-reader-electron-bin sherlock-git

### Window Manager

#### i3

    yay -S i3 polybar rofi picom dunst scrot xclip xorg-xclipboard xcolor xwallpaper lxappearance polkit-kde-agent --needed

#### Hyprland

    yay -S hyprland waybar xdg-desktop-portal-hyprland qt5-wayland qt6-wayland \
           hyprpaper hyprpicker grim slurp nwg-look wl-clipboard cliphist dunst \
           hyprlock rofi-lbonn-wayland tesseract tesseract-data-eng \
           tesseract-data-tur tesseract-data-rus tesseract-data-deu wlrobs-hg wlogout \
           gtk-layer-shell polkit-kde-agent --needed

### Shell

#### Fish

    sudo pacman -S fish fisher  
    fisher install IlanCosman/tide@v6  
    chsh -s /usr/bin/fish

#### Zsh

first, installing zsh and changing default shell to zsh

    sudo pacman -S zsh zsh-completions && chsh -s /usr/bin/zsh

then cloning required pluginsㅤ

    git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions && git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting && git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k

ㅤlast one, editing zsh config and including plugins

    nvim ~/.zshrc

/plugins
- `plugins=( git zsh-autosuggestions zsh-syntax-highlighting )`

/ZSH_THEME
- `ZSH_THEME="powerlevel10k/powerlevel10k"`

      source .zshrc

## System Modules

### Zen Kernel

first downloading the packages

    sudo pacman -S linux-zen linux-zen-headers
    
then editing the grub

    sudo nvim /etc/default/grub

> GRUB_SAVEDEFAULT="true"  
> remove # (uncomment)  
> make GRUB_DEFAULT=saved

    sudo grub-mkconfig -o /boot/grub/grub.cfg

on the grub menu, select the linux-zen kernel. on the next time will automatically select the zen kernel

reboot

### Changing GRUB time

    sudo nvim /etc/default/grub

> make GRUB_TIMEOUT=0

    sudo grub-mkconfig -o /boot/grub/grub.cfg

reboot

### Changing Limine time

    sudo nvim /boot/limine.cfg

> make TIMEOUT=0

### Mounting Disk

first, creating mount folder
- `cd /mnt`
- `sudo mkdir Depo`

list disks uuid
- type `lsblk -f` and copy the uuid

then
- `sudo nvim /etc/fstab`

      UUID=paste_uuid_here              /mnt/Depo     ntfs     defaults      0 0
  
- `systemctl daemon-reload`
- `sudo mount -a`

reboot

### Adding SWAP

create a swap file

    sudo dd if=/dev/zero of=/swapfile bs=1M count=4096

set to file permission 600

    sudo chmod 600 /swapfile

make swap

    sudo mkswap /swapfile

turn the swap on

    sudo swapon /swapfile

verify process

    swapon --show

add swap file to fstab

    sudo nvim /etc/fstab

paste this into last line

    /swapfile                                 none           swap    defaults         0 0

reboot

if you want to delete swap

    sudo swapoff -v /swapfile && sudo rm /swapfile

reboot

## Useful things

### Connect to Wi-Fi

with network manager

    nmtui

with iwctl

    [iwd]# device list
    [iwd]# station wlan0 scan
    [iwd]# station wlan0 get-networks
    [iwd]# station wlan0 connect <network>
    [iwd]# station wlan0 show

change dns by edit the connections and on ipv4 settings select the addresses only n enter the following ip addresses;

    9.9.9.9, 149.112.112.112

### Install Driver

#### Intel:

    yay -S mesa lib32-mesa libva-mesa-driver lib32-libva-mesa-driver libva-intel-driver lib32-libva-intel-driver xf86-video-intel vulkan-intel lib32-vulkan-intel vulkan-icd-loader lib32-vulkan-icd-loader --needed

#### AMD:

    yay -S mesa lib32-mesa libva-mesa-driver lib32-libva-mesa-driver xf86-video-amdgpu vulkan-radeon lib32-vulkan-radeon vulkan-icd-loader lib32-vulkan-icd-loader --needed

#### Bluetooth:

    yay -S bluez bluez-utils blueman

#### Printers:

    yay -S cups

### Apply Themes

#### GTK

Dracula GTK: <https://github.com/dracula/gtk/archive/master.zip>

- download the $theme and extract the .zip file to the `~/.themes`
- open up `lxappearance` and then select the $theme into widgets.

#### QT

Dracula QT: <https://github.com/dracula/qt5/archive/master.zip>

- download the $theme and extract the anywhere
- open up `kvantum` and select the folder that includes $theme and install it
- then click the change theme and select the $theme
- open up qt5ct and qt6ct and select the kvantum

### Backup Files

create folders for backup

    mkdir ~/dotbak && mkdir ~/dotbak/.config && mkdir ~/dotbak/.mozilla && mkdir ~/dotbak/.thunderbird && mkdir ~/dotbak/.themes && mkdir ~/dotbak/.icons

backup the config files

    rsync -a --delete ~/.config/ ~/dotbak/.config/
    rsync -a --delete ~/.mozilla/ ~/dotbak/.mozilla/
    rsync -a --delete ~/.thunderbird/ ~/dotbak/.thunderbird/
    rsync -a --delete ~/.themes/ ~/dotbak/.themes/
    rsync -a --delete ~/.icons/ ~/dotbak/.icons/
    rsync -a --delete ~/.aliases ~/dotbak/
    rsync -a --delete ~/.bashrc ~/dotbak/
    rsync -a --delete ~/.zshrc ~/dotbak/

### DPI Bypass

    git clone https://github.com/bol-van/zapret
    cd zapret

check and install

    sudo ./install_bin.sh
    sudo ./blockcheck.sh
    sudo ./install_easy.sh

### Adblock

    sudo curl -o /etc/hosts https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts

### Dictionary

- Download database via: <https://github.com/metwse/rofi-tdk.sh/releases/>

      sudo mv ~/Downloads/rofi-tdk.tar.gz /var/

### Show Stars on Sudo Password

    sudo nvim /etc/sudoers

add

    Defaults pwfeedback

### Tuxi Config Fix

`sudo nvim /usr/bin/tuxi`

line 18:

    [ -n "$TUXI_LANG" ] && LANGUAGE="$TUXI_LANG" || LANGUAGE="tr"

line 886:
      
    user_agent="Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) QtWebEngine/5.15.2 Chrome/87.0.4280.144 Safari/537.36"

### Prism Launcher Offline Bypass

    echo '{"accounts": [{"entitlement": {"canPlayMinecraft": true,"ownsMinecraft": true},"type": "Offline"}],"formatVersion": 3}' > ~/.local/share/PrismLauncher/accounts.json

## Error Solutions

### If pacman gives PGP error

    sudo pacman -S archlinux-keyring && sudo pacman-key --refresh && sudo pacman-key --list-keys brett@i--b.com

---
### If bluetooth not working

    rfkill list
    rfkill unblock bluetooth
    systemctl status bluetooth
    sudo systemctl start bluetooth
    systemctl status bluetooth

---
### If controller doesn't connect to PC

    [bluetoothctl#] scan on
    [bluetoothctl#] devices
    [bluetoothctl#] pair <gamepad>
    [bluetoothctl#] connect <gamepad>
    [bluetoothctl#] trust <gamepad>

---
### If controller asks for PIN code

add this lines into /etc/bluetooth/input.conf

    [General]
    ClassicBondedOnly=false

---
### If notifications not work correctly on KDE

    sudo pacman -S knotifications5 knotifyconfig5
  
- go to settings and notifications then enable all authentication pushs

---
### If clipboard not work correctly

- go to clipboard setings and set keyboard shortcut "Show Items at Mouse Posittion"

## Firefox Config

```
### Needed

extensions.pocket.enabled = false
browser.send_pings = false
dom.event.clipboardevents.enabled = false
media.eme.enabled = false
media.navigator.enabled = false
beacon.enabled = false
browser.safebrowsing.downloads.remote.enabled = false
network.IDN_show_punycode = true
    
### For Google IP
    
geo.enabled = false
geo.wifi.uri = blank
browser.search.geoip.url = blank
    
### For ultra super privacy
    
browser.safebrowsing.enabled = false
browser.safebrowsing.phishing.enabled = false
browser.safebrowsing.malware.enabled = false
browser.safebrowsing.downloads.enabled = false
browser.safebrowsing.provider.google4.dataSharing.enabled = blank
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

<a href="#top">Back to top</a>
