## Index

- [Configure Pacman](#configure-pacman)
    - [Basic Tweaks](#basic-tweaks)
    - [Chaotic AUR](#chaotic-aur)
- [Install Packages](#install-packages)
    - [Necessary Packages](#necessary-packages)
    - [Applications](#applications)
        - [General](#general)
        - [Audio](#audio)
        - [Game](#game)
        - [Other](#other)
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
    - [Install driver](#install-driver)
        - [Intel](#intel)
        - [AMD](#amd)
        - [Bluetooth](#bluetooth)
        - [Printers](#printers)
    - [Apply themes](#apply-themes)
        - [GTK](#gtk)
        - [QT](#qt)
    - [Backup files](#backup-files)
    - [DPI bypass](#dpi-bypass)
    - [Adblock](#adblock)
    - [Dictionary](#dictionary)
    - [Show stars on sudo password](#show-stars-on-sudo-password)
    - [Change keyboard layout on X11](#change-keyboard-layout-on-x11)
    - [Prism Launcher offline bypass](#prism-launcher-offline-bypass)
    - [Tuxi config fix](#tuxi-config-fix)
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

enable multilib and make pacman colorful

    sudo sed -i "/#Color/s/^#//g" /etc/pacman.conf; sudo sed -i "/#ParallelDownloads = 5/s/^#//g" /etc/pacman.conf; sudo sed -i "88,89s/#//" /etc/pacman.conf; echo "ILoveCandy" | sudo sed -i "33i\ILoveCandy" /etc/pacman.conf

then update pacman

    sudo pacman -Syu

### Chaotic AUR

firstly, downloading required packages

    sudo pacman-key --recv-key 3056513887B78AEB --keyserver keyserver.ubuntu.com && sudo pacman-key --lsign-key 3056513887B78AEB && sudo pacman -U 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-keyring.pkg.tar.zst' 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-mirrorlist.pkg.tar.zst' --noconfirm

enable chaotic aur

    echo -e "\n[chaotic-aur]\nInclude = /etc/pacman.d/chaotic-mirrorlist" | sudo tee -a /etc/pacman.conf

## Install Packages

### Necessary Packages:

    sudo pacman -S inxi linux-headers man-db tldr git base-devel yay fast scrcpy yt-dlp fzf ytfzf \
                   netctl dialog bind net-tools pup recode jq curl wget locate htop btop android-tools \
                   neofetch fastfetch pfetch zip unzip p7zip unrar make libva xsensors cmatrix \
                   rsync vi vim neovim starship tlp qt5ct qt6ct gnome-keyring translate-shell \
                   ttf-hack ttf-hack-nerd otf-font-awesome ttf-jetbrains-mono-nerd noto-fonts-emoji \
                   lsb-release network-manager-applet ffmpegthumbnailer tumbler wine-stable \
                   pavucontrol pipewire pipewire-pulse protonvpn-cli python-requests \
                   kvantum kvantum-qt5 mpv mpv-mpris gvfs gvfs-mtp mtpfs pacman-contrib thefuck cava \
                   redshift tty-clock rate-mirrors --needed

> [!WARNING]
> Install xdg-desktop-portal also if you use flatpak

> [!NOTE]
> Don't forget the enable tlp
>
>     sudo systemctl enable --now tlp.service

### Applications

#### General:

    yay -S firefox alacritty thunar syncthing anki \
           kdeconnect kdiskmark thunderbird obs-studio piper qbittorrent \
           vscodium discord ventoy thunar-volman thunar-archive-plugin \
           kweather gnome-system-monitor viewnior gimp steam upscayl \
           ungoogled-chromium youtube-music-git metadata-cleaner \
           dialect okular obsidian marker xarchiver jre-openjdk --needed

#### Audio:

    yay -S easyeffects audacity lsp-plugins-lv2 --needed

#### Game:

    yay -S 0ad osu mindustry wesnoth openttd openrct2 openra openloco openage granatier dol-git --needed

#### Other:

    yay -S kdenlive krita antimicrox bitwarden goverlay qdirstat celluloid epiphany \
           signal-desktop nuclear-player-bin lutris heroic-games-launcher-bin \
           tor-browser-bin librewolf epiphany octopi prismlauncher video-downloader \
           duckstation-git hypnotix ruffle-git lightspark notesnook-bin logseq-desktop-bin \
           stremio discover-overlay mousai songrec soundux tokodon kdevelop davinci-resolve \
           handbrake ppsspp rustdesk parsec calibre dino wike dissent amberol cpu-x \
           github-desktop harmonoid protonlaunch minecraft-launcher mcpelauncher-linux-git \
           waypaper-git shotcut flowblade olive vidcutter neovide edex-ui wireshark \
           hardinfo pamac-aur ksysguard gnome-dictionary waydroid --needed

### Flatpak:

    yay -S flatpak && flatpak install com.github.tchx84.Flatseal io.gitlab.jstest_gtk.jstest_gtk com.github.k4zmu2a.spacecadetpinball

### AUR:

    yay -S tgpt-bin localsend-bin sklauncher-bin fluent-reader-electron-bin tuxi-git urn-git sherlock-git lyrebird hydroxide --needed

### Window Manager

#### i3

    yay -S i3 polybar rofi picom dunst scrot xsel xcolor xwallpaper clipmenu redshift lxappearance polkit-gnome --needed

#### Hyprland

    yay -S hyprland hyprpaper hyprlock hyprpicker waybar dunst \
           grim slurp nwg-look wl-clipboard cliphist qt5-wayland qt6-wayland \
           rofi-lbonn-wayland tesseract tesseract-data-eng tesseract-data-tur \
           tesseract-data-rus tesseract-data-deu wlrobs-hg wlogout gtk-layer-shell \
           brightnessctl playerctl wireplumber pamixer polkit-gnome --needed

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
- `plugins=(git zsh-autosuggestions zsh-syntax-highlighting)`

/ZSH_THEME
- `ZSH_THEME="powerlevel10k/powerlevel10k"`

      source .zshrc

## System Modules

### Zen Kernel

first downloading the packages

    sudo pacman -S linux-zen linux-zen-headers

then adjust grub for zen kernel

    sudo sed -i "s/GRUB_DEFAULT=0/GRUB_DEFAULT=saved/g" /etc/default/grub; sudo sed -i "/#GRUB_SAVEDEFAULT=true/s/^#//g" /etc/default/grub

update grub

    sudo grub-mkconfig -o /boot/grub/grub.cfg

reboot to grub and select the linux-zen kernel. on the next time will automatically select the zen kernel

### Changing GRUB time

    sudo sed -i "s/GRUB_TIMEOUT=5/GRUB_TIMEOUT=0/g" /etc/default/grub

update grub and reboot

    sudo grub-mkconfig -o /boot/grub/grub.cfg

### Changing Limine time

    sudo sed -i "s/TIMEOUT=5/TIMEOUT=0/g" /boot/limine.cfg

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

### Adding Swap

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

### Install driver

#### Intel:

    yay -S mesa lib32-mesa libva-mesa-driver lib32-libva-mesa-driver libva-intel-driver lib32-libva-intel-driver xf86-video-intel vulkan-intel lib32-vulkan-intel vulkan-icd-loader lib32-vulkan-icd-loader --needed

#### AMD:

    yay -S mesa lib32-mesa libva-mesa-driver lib32-libva-mesa-driver xf86-video-amdgpu vulkan-radeon lib32-vulkan-radeon vulkan-icd-loader lib32-vulkan-icd-loader --needed

#### Bluetooth:

    yay -S bluez bluez-utils blueman

#### Printers:

    yay -S cups

### Apply themes

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

### Backup files

backup the files using rsync

    rsync -a --delete ~/.config/ ~/Backup/Configs/.config/ && rsync -a --delete ~/.mozilla/ ~/Backup/Configs/.mozilla/ && rsync -a --delete ~/.thunderbird/ ~/Backup/Configs/.thunderbird/ && rsync -a --delete ~/.themes/ ~/Backup/Configs/.themes/ && rsync -a --delete ~/.icons/ ~/Backup/Configs/.icons/ && rsync -a --delete ~/.aliases ~/Backup/Configs/ && rsync -a --delete ~/.bashrc ~/Backup/Configs/ && rsync -a --delete ~/.zshrc ~/Backup/Configs/ && rsync -a --delete ~/.xprofile ~/Backup/Configs/ ; echo 'All config files backed up successfully.'

    rsync -a --delete ~/Backup2lte/ ~/Backup/Backup2lte/ && rsync -a --delete ~/DCIM/ ~/Backup/DCIM/ && rsync -a --delete ~/Music/ ~/Backup/Music/ && rsync -a --delete ~/Notes/ ~/Backup/Notes/ && rsync -a --delete ~/Pictures/ ~/Backup/Pictures/ && rsync -a --delete ~/Videos/ ~/Backup/Videos/ ; echo 'All sync files backed up successfully.'

### DPI bypass

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

### Show stars on sudo password

    echo "Defaults pwfeedback" | sudo tee -a /etc/sudoers

### Change keyboard layout on X11

    /etc/X11/xorg.conf.d/00-keyboard.conf

change lines to this

        Option "XkbLayout" "tr,us"
        Option "XkbOptions" "grp:alt_shift_toggle"

### Prism Launcher offline bypass

    echo '{"accounts": [{"entitlement": {"canPlayMinecraft": true,"ownsMinecraft": true},"type": "Offline"}],"formatVersion": 3}' > ~/.local/share/PrismLauncher/accounts.json

### Tuxi config fix

> ready binary here: <https://gist.github.com/waztedll/0d3856ca7e583949ace73245a234f5d4>

    sudo sed -i '18c\[ -n "$TUXI_LANG" \] && LANGUAGE="$TUXI_LANG" || LANGUAGE="tr"' /usr/bin/tuxi && sudo sed -i '886c\user_agent="Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) QtWebEngine/5.15.2 Chrome/87.0.4280.144 Safari/537.36"' /usr/bin/tuxi

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

    echo -e "[General]\nClassicBondedOnly=false" | sudo tee -a /etc/bluetooth/input.conf

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
