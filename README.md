The system has been installed, run:

    sudo pacman -Syu

If you need refresh to keys:
-

    sudo pacman -S archlinux-keyring && sudo pacman-key --refresh && sudo pacman-key --list-keys brett@i--b.com

# Installation
**Beginning install**

Configure & Speed Up Pacman
-

    sudo nano /etc/pacman.conf

Remove # on

`Color`  
`Parallel Downloads = 5`
    
`[multilib]`  
`Include = /etc/pacman.d/mirrorlist`

Add  

    ILoveCandy

Update pacman

    sudo pacman -Syu

Updating mirrorlist
-

    sudo pacman -S reflector --noconfirm && sudo cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.bak && sudo reflector --verbose --latest 10 --protocol https --sort rate --save /etc/pacman.d/mirrorlist && sudo pacman -Syu

# Chaotic AUR
first, downloading required packages

    sudo pacman-key --recv-key 3056513887B78AEB --keyserver keyserver.ubuntu.com && sudo pacman-key --lsign-key 3056513887B78AEB && sudo pacman -U 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-keyring.pkg.tar.zst' 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-mirrorlist.pkg.tar.zst'
then editing the pacman config

    sudo nano /etc/pacman.conf
include this codes

    [chaotic-aur]  
    Include = /etc/pacman.d/chaotic-mirrorlist

then updating the mirrors

    sudo pacman -S powerpill --noconfirm && sudo pacman -Sy && sudo powerpill -Su && sudo pacman -Su

# Packages to Install

## requirements:

    sudo pacman -S inxi linux-headers git base-devel yay ksh tcsh fast pup scrcpy yt-dlp rofi npm \
                   netctl dialog recode net-tools jq wget cargo locate htop btop \
                   fastfetch pfetch rufetch ufetch-git corectrl zip unzip p7zip unrar nodejs make  \
                   podman gvfs libva xsensors cmatrix vi vim neovim starship iotop ufw tlp tlp-rdw \
                   qt5ct qt6ct gnome-keyring otf-font-awesome ttf-jetbrains-mono-nerd noto-fonts-emoji \
                   speech-dispatcher translate-shell lsb-release network-manager-applet wine-stable \
                   firefox-pwa python ffmpegthumbnailer tumbler brightnessctl playerctl pipewire \
                   pipewire-pulse python-requests wireplumber pamixer pavucontrol kvantum mpv \
                   neofetch dracula-gtk-theme-git gtk-layer-shell hardinfo flatpak --needed

#### tlp

    sudo systemctl enable --now tlp.service

#### NvChad

    git clone https://github.com/NvChad/NvChad ~/.config/nvim --depth 1 && nvim

## applications:

    sudo pacman -S pamac-nosnap antimicrox bitwarden easyeffects celluloid thunar audacity \
                   alacritty kitty kdenlive kdeconnect thunderbird obs-studio piper qbittorrent \
                   qdirstat kdiskmark spotify vscodium discord gtkcord4 ventoy okular \
                   akregator epiphany cheese kweather ksysguard granatier kwrite viewnior \
                   krita steam upscayl ungoogled-chromium youtube-music metadata-cleaner \
                   mangohud goverlay gnome-dictionary dialect wike thunar-archive-plugin \
                   obsidian notesnook harmonoid jre-openjdk jdk-openjdk --needed
                   
optional: `signal-desktop nuclear-player-bin xdman lutris heroic-games-launcher-bin thorium-browser-bin tor-browser-bin librewolf epiphany octopi prismlauncher video-downloader duckstation-git hypnotix ruffle lightspark logseq-desktop-bin stremio syncthing armcord discover-overlay`

## flatpak:

    flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo \
    && flatpak install com.github.tchx84.Flatseal rustdesk com.parsecgaming.parsec com.github.k4zmu2a.spacecadetpinball io.gitlab.jstest_gtk.jstest_gtk org.localsend.localsend_app

## AUR:

    yay -S cpufetch tuxi devour urn-git lyrebird spotube-bin waypaper-git sklauncher-bin dol-git easyssh

# Hyprland

    yay -S --needed hyprland xdg-desktop-portal xdg-desktop-portal-hyprland qt5-wayland qt6-wayland \
                    waybar hyprpaper hyprpicker grimblast nwg-look wl-clipboard clipman mako swaybg \
                    swaylock-effects slurp grim rofi-lbonn-wayland-git tesseract tesseract-data-eng \
                    tesseract-data-tur tesseract-data-rus tesseract-data-deu wlrobs-hg wlogout \
                    wine-wl-git webcord polkit-kde-agent

### for weather

    curl -s https://raw.githubusercontent.com/yusufipk/hyprconf/master/waybar/modules/weather.sh | sh

# Installing Shells

Install ZSH
-

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

Installing fish
-

    sudo pacman -S fish fisher && fish && fisher install IlanCosman/tide@v6 && chsh -s /usr/bin/fish

# System Modules

Installing Zen kernel
-

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

Changing GRUB time
-

    sudo nvim /etc/default/grub

/GRUB_TIMEOUT=5  
make GRUB_TIMEOUT=0

    sudo grub-mkconfig -o /boot/grub/grub.cfg

reboot

Mounting Disk
-

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

Adding SWAP (4GiB)
-

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

Connecting to Wi-Fi
-

    nmtui

Driver
-

for dual gpus:

    yay -S optimus-manager

for open source amd & intel drivers:

    yay -S mesa lib32-mesa vulkan-radeon vulkan-intel lib32-vulkan-radeon lib32-vulkan-intel libva-mesa-driver lib32-libva-mesa-driver xf86-video-intel xf86-video-amdgpu vulkan-icd-loader lib32-vulkan-icd-loader --needed

for printers:

    yay -S cups

for bluetooth:

    yay -S bluez bluez-utils bluez-qt5 blueman

Applying GTK & QT themes
-

IMPORTANT: before the beginning be sure you have loaded ~/.themes and ~/.icons folders

### GTK

first download the dracula kvantum and tokyonight-se icons [here](https://rentry.org/x9tsn)

- firstly, extract the `TokyoNight-SE.tar.bz2` into `/usr/share/icons`
- secondly, open the `nwg-look` on wayland then select the `Dracula` into widgets, in icons select the `Tokyo Night-SE`

### QT

- firstly, extract the `Dracula.tar.xz`
- secondly, open the `kvantum` and select the Dracula folder and install it
- then click the change theme and select the Dracula

Applying GTK & icon themes on flatpak applications
-

    sudo flatpak override --filesystem=$HOME/.themes && sudo flatpak override --filesystem=$HOME/.icons

then choosing the right theme & icons

    sudo flatpak override --env=GTK_THEME=Dracula && sudo flatpak override --env=ICON_THEME=TokyoNight-SE

Showing stars on sudo password
-

    sudo nvim /etc/sudoers

add

    Defaults pwfeedback

Editing tuxi config
-

`nvim /usr/bin/tuxi`

line 18:

    [ -n "$TUXI_LANG" ] && LANGUAGE="$TUXI_LANG" || LANGUAGE="tr"

line 886:
      
    user_agent="Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) QtWebEngine/5.15.2 Chrome/87.0.4280.144 Safari/537.36"

Removing color on noefetch
-

    sudo nvim /home/taha/.config/neofetch/config.conf

- Add # on **info cols**

Backup your config files
-

    mkdir ~/backup && mkdir ~/backup/.config && mkdir ~/backup/.mozilla && mkdir ~/backup/.thunderbird && mkdir ~/backup/.themes && mkdir ~/backup/.icons

    rsync -a --delete ~/.config/ ~/backup/.config/
    rsync -a --delete ~/.mozilla/ ~/backup/.mozilla/
    rsync -a --delete ~/.thunderbird/ ~/backup/.thunderbird/
    rsync -a --delete ~/.themes/ ~/backup/.themes/
    rsync -a --delete ~/.icons/ ~/backup/.icons/
    rsync -a --delete ~/.aliases ~/backup/
    rsync -a --delete ~/.bashrc ~/backup/
    rsync -a --delete ~/.zshrc ~/backup/

# Error Solutions

--------------------------------------------------
If bluetooth not working, run this commands
-

- sudo rfkill list
- sudo rfkill unblock bluetooth
- sudo systemctl status bluetooth
- sudo systemctl start bluetooth
- sudo systemctl status bluetooth

Check the PS3 controller, then click the ***Truth & Authorise*** notification

--------------------------------------------------
If notifications will not working correctly
-

    sudo pacman -S knotifications5 knotifyconfig5
  
- go to settings and notifications then enable all authentication pushs

--------------------------------------------------
If clipboard will not working correctly
-

- go to clipboard setings and set keyboard shotcut "Show Items at Mouse Posittion"

--------------------------------------------------
KDE
-

- Konsole

install edna theme and set transparecsty %50

- Plasma

install tokyo night and set splash arch theme

reboot.

# *Shortcuts*

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
