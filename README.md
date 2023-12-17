FThe system has been installed, run:

    sudo pacman -Syu

## If you need refresh to keys:

    sudo pacman -S archlinux-keyring pacman-contrib vim && sudo pacman-key --refresh && sudo pacman-key --list-keys brett@i--b.com

create mirrorlists

    sudo touch /etc/pacman.d/mirrorlist && sudo touch /etc/pacman.d/chaotic-mirrorlist

# Beginning install

## Configure & Speed Up Pacman

    sudo vim /etc/pacman.conf

Remove # on

`Color`  
`Parallel Downloads = 5`
    
`[multilib]`  
`Include = /etc/pacman.d/mirrorlist`

Add  

    ILoveCandy

Update pacman

    sudo pacman -Syu

# Chaotic AUR

first, downloading required packages

    sudo pacman-key --recv-key 3056513887B78AEB --keyserver keyserver.ubuntu.com && sudo pacman-key --lsign-key 3056513887B78AEB && sudo pacman -U 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-keyring.pkg.tar.zst' 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-mirrorlist.pkg.tar.zst'

then editing the pacman config

    sudo vim /etc/pacman.conf

include this codes

    [chaotic-aur]  
    Include = /etc/pacman.d/chaotic-mirrorlist

# Packages to Install

## requirements:

    sudo pacman -S inxi linux-headers git base-devel yay ksh tcsh fast pup scrcpy yt-dlp rofi npm \
                   netctl dialog bind recode net-tools jq wget cargo locate htop btop android-tools \
                   fastfetch pfetch rufetch ufetch-git corectrl zip unzip p7zip unrar nodejs make  \
                   podman gvfs libva xsensors cmatrix vi vim neovim starship iotop ufw tlp tlp-rdw \
                   qt5ct qt6ct gnome-keyring otf-font-awesome ttf-jetbrains-mono-nerd noto-fonts-emoji \
                   speech-dispatcher translate-shell lsb-release network-manager-applet wine-stable \
                   firefox-pwa python ffmpegthumbnailer tumbler brightnessctl playerctl pipewire \
                   pipewire-pulse python-requests wireplumber pamixer pavucontrol kvantum mpv \
                   neofetch dracula-gtk-theme-git gtk-layer-shell gvfs gvfs-mtp hardinfo
                   cava tty-clock xdg-desktop-portal rate-mirrors --needed

#### tlp

    sudo systemctl enable --now tlp.service

## applications:

    sudo pacman -S firefox pamac-nosnap bitwarden easyeffects thunar audacity syncthing \
                   alacritty kdenlive kdeconnect thunderbird obs-studio piper qbittorrent \
                   qdirstat kdiskmark spotify vscodium discord gtkcord4 ventoy okular \
                   kweather ksysguard kwrite viewnior lsp-plugins-lv2 \
                   krita steam upscayl ungoogled-chromium youtube-music metadata-cleaner \
                   mangohud goverlay gnome-dictionary dialect wike thunar-archive-plugin \
                   obsidian marker harmonoid protonvpn-cli jre-openjdk jdk-openjdk --needed
                   
optional: `antimicrox celluloid kitty epiphany signal-desktop nuclear-player-bin xdman lutris heroic-games-launcher-bin tor-browser-bin librewolf epiphany octopi prismlauncher video-downloader duckstation-git hypnotix ruffle lightspark notesnook-bin logseq-desktop-bin stremio armcord discover-overlay mousai songrec soundux tokodon kdevelop handbrake 0ad osu ppsspp rustdesk parsec calibre dino`

game: `mindustry wesnoth granatier`

## flatpak:

    flatpak install com.github.tchx84.Flatseal com.github.k4zmu2a.spacecadetpinball io.gitlab.jstest_gtk.jstest_gtk

## AUR:

    yay -S tuxi-git devour urn-git lyrebird spotube-bin waypaper-git sklauncher-bin localsend-bin fluent-reader-bin

game: `dol-git`

# Hyprland

    yay -S --needed hyprland xdg-desktop-portal-hyprland qt5-wayland qt6-wayland \
                    waybar hyprpaper hyprpicker grimblast nwg-look wl-clipboard cliphist dunst swaybg \
                    swaylock-effects slurp grim rofi-lbonn-wayland tesseract tesseract-data-eng \
                    tesseract-data-tur tesseract-data-rus tesseract-data-deu wlrobs-hg wlogout \
                    wine-wl-git webcord polkit-kde-agent

### for weather

    curl -s https://raw.githubusercontent.com/yusufipk/hyprconf/master/waybar/modules/weather.sh | sh

# Installing Shells

## Install ZSH

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

## Installing fish

    sudo pacman -S fish fisher && fish && fisher install IlanCosman/tide@v6 && chsh -s /usr/bin/fish

# System Modules

## Installing Zen kernel

first downloading the packages

    sudo pacman -S linux-zen linux-zen-headers
    
then editing the grub

    sudo nvim /etc/default/grub

/GRUB_SAVEDEFAULT="true"  
remove # (uncomment)

/GRUB_DEFAULT=0  
make GRUB_DEFAULT=saved

    sudo grub-mkconfig -o /boot/grub/grub.cfg

on the grub menu, select the linux-zen kernel. on the next time will automatically select the zen kernel

reboot

## Changing GRUB time

    sudo nvim /etc/default/grub

/GRUB_TIMEOUT=5  
make GRUB_TIMEOUT=0

    sudo grub-mkconfig -o /boot/grub/grub.cfg

reboot

## Mounting Disk

first, creating mount folder
- `cd /mnt`
- `sudo mkdir Depo`

list disks uuid
- `lsblk -f` or `ls -l /dev/disk/by-uuid`              

then
- `sudo nvim /etc/fstab`

      UUID=uuid_paste_here              /mnt/Depo     ntfs     defaults      0 0
  
- `systemctl daemon-reload`
- `sudo mount -a`

reboot

## Adding SWAP (4GiB)

- sudo dd if=/dev/zero of=/swapfile bs=1M count=4096
- sudo chmod 600 /swapfile
- sudo mkswap /swapfile
- sudo swapon /swapfile
- swapon --show
- sudo nvim /etc/fstab

      /swapfile                                 none           swap    defaults         0 0

reboot

**Deleting Swap file**

    sudo swapoff -v /swapfile && sudo rm /swapfile

reboot

# Useful utilities

## Connecting to Wi-Fi

    nmtui

## Driver

for dual gpus:

    yay -S optimus-manager

for open source amd & intel drivers:

    yay -S mesa lib32-mesa vulkan-radeon vulkan-intel lib32-vulkan-radeon lib32-vulkan-intel libva-mesa-driver lib32-libva-mesa-driver xf86-video-intel xf86-video-amdgpu vulkan-icd-loader lib32-vulkan-icd-loader --needed

for printers:

    yay -S cups

for bluetooth:

    yay -S bluez bluez-utils bluez-plugins bluez-qt5 blueman

## Applying GTK & QT themes

IMPORTANT: before the beginning be sure you have loaded ~/.themes and ~/.icons folders

### GTK

first download the dracula kvantum and tokyonight-se icons [here](https://rentry.org/x9tsn)

- firstly, extract the `TokyoNight-SE.tar.bz2` into `/usr/share/icons`
- secondly, open the `nwg-look` on wayland then select the `Dracula` into widgets, in icons select the `Tokyo Night-SE`

### QT

- firstly, extract the `Dracula.tar.xz`
- secondly, open the `kvantum` and select the Dracula folder and install it
- then click the change theme and select the Dracula

## Applying GTK & icon themes on flatpak applications

    sudo flatpak override --filesystem=$HOME/.themes && sudo flatpak override --filesystem=$HOME/.icons

then choosing the right theme & icons

    sudo flatpak override --env=GTK_THEME=Dracula && sudo flatpak override --env=ICON_THEME=TokyoNight-SE

## Backup your config files

    mkdir ~/backup && mkdir ~/backup/.config && mkdir ~/backup/.mozilla && mkdir ~/backup/.thunderbird && mkdir ~/backup/.themes && mkdir ~/backup/.icons

    rsync -a --delete ~/.config/ ~/backup/.config/
    rsync -a --delete ~/.mozilla/ ~/backup/.mozilla/
    rsync -a --delete ~/.thunderbird/ ~/backup/.thunderbird/
    rsync -a --delete ~/.themes/ ~/backup/.themes/
    rsync -a --delete ~/.icons/ ~/backup/.icons/
    rsync -a --delete ~/.aliases ~/backup/
    rsync -a --delete ~/.bashrc ~/backup/
    rsync -a --delete ~/.zshrc ~/backup/

## Zapret

    git clone https://github.com/bol-van/zapret
    cd zapret

checking and installing

    sudo ./install_bin.sh
    sudo ./blockcheck.sh
    sudo ./install_easy.sh

## Rofi

### Theme

- Download theme via: <https://github.com/newmanls/rofi-themes-collection/blob/master/themes/rounded-pink-dark.rasi>

         sudo mv ~/Downloads/rounded-pink-dark.rasi /usr/share/rofi/themes/

### Dictionary

- Download database via: <https://github.com/metwse/rofi-tdk.sh/releases/>

        sudo mv ~/Downloads/rofi-tdk.tar.gz /var/

## Showing stars on sudo password

    sudo nvim /etc/sudoers

add

    Defaults pwfeedback

## Editing tuxi config

`nvim /usr/bin/tuxi`

line 18:

    [ -n "$TUXI_LANG" ] && LANGUAGE="$TUXI_LANG" || LANGUAGE="tr"

line 886:
      
    user_agent="Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) QtWebEngine/5.15.2 Chrome/87.0.4280.144 Safari/537.36"

## Removing color on noefetch

    sudo nvim /home/taha/.config/neofetch/config.conf

- Add # on **info cols**



## Prism Launcher offline fix

    echo '{"accounts": [{"entitlement": {"canPlayMinecraft": true,"ownsMinecraft": true},"type": "Offline"}],"formatVersion": 3}' > ~/.local/share/PrismLauncher/accounts.json

# Error Solutions

--------------------------------------------------
## If bluetooth not working, run this commands

    rfkill list
    rfkill unblock bluetooth
    systemctl status bluetooth
    sudo systemctl start bluetooth
    systemctl status bluetooth

### If controller not connect to PC, run the following commands on bluetoothctl

    [bluetoothctl#] scan on
    [bluetoothctl#] pair <gamepad>
    [bluetoothctl#] connect <gamepad>
    [bluetoothctl#] trust <gamepad>

Check the PS3 controller, then click the ***Truth & Authorise*** notification

--------------------------------------------------
## If notifications will not working correctly

    sudo pacman -S knotifications5 knotifyconfig5
  
- go to settings and notifications then enable all authentication pushs

--------------------------------------------------
If clipboard will not working correctly
-

- go to clipboard setings and set keyboard shotcut "Show Items at Mouse Posittion"

--------------------------------------------------
## KDE

- Konsole

install edna theme and set transparecsty %50

- Plasma

install tokyo night and set splash arch theme

reboot.

# **Shortcuts**

```
# kill active program
$alt+q
$: killactive

# rofi
$alt+r
$: rofi -modi drun -show drun -show-icons

# start browser (gecko)
$mod+w
$: firefox

# start browser (webkit-gtk)
$mod_shift+w
$: epiphany

# start terminal
$mod+return
$: alacritty

# start file manager
$mod+e
$: thunar

# start mail client
$mod+g
$: thunderbird

# start system monitor
$mod+h
$: ksysguard
    
# start package manager
$mod_shift+p
$: pamac-manager
```

# Firefox config

```
- Needed

extensions.pocket.enabled = false
browser.send_pings = false
dom.event.clipboardevents.enabled = false
media.eme.enabled = false
media.navigator.enabled = false
beacon.enabled = false
browser.safebrowsing.downloads.remote.enabled = false
network.IDN_show_punycode = true
    
- For Google IP
    
geo.enabled = false
geo.wifi.uri = blank
browser.search.geoip.url = blank
    
- For ultra super privacy
    
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
