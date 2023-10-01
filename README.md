
# Connecting to Wi-Fi
- iwctl
- device list
- station wlan0 scan
- station wlan0 get-networks
- station wlan0 connect 'your wifi name'
- station wlan0 show
- ping gnu.org

The system has been installed, run:

      sudo pacman -Syu

If you need refresh to keys:
-

- sudo pacman -S archlinux-keyring
- sudo pacman-key --list-keys brett@i--b.com
- sudo pacman-key --refresh

# Installation
After the Install

Configure & Speed Up Pacman
-

    sudo nano /etc/pacman.conf

Remove # on
- Color
- Parallel Downloads = 5
- [multilib]
- Include = /etc/pacman.d/mirrorlist

Add
- ILoveCandy

Update pacman
- sudo pacman -Syu

Updating mirrorlist
-

    sudo pacman -S reflector && sudo cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.bak && sudo reflector --verbose --latest 10 --protocol https --sort rate --save /etc/pacman.d/mirrorlist && sudo pacman -Syu

# Chaotic AUR

    sudo pacman-key --recv-key 3056513887B78AEB --keyserver keyserver.ubuntu.com && sudo pacman-key --lsign-key 3056513887B78AEB && sudo pacman -U 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-keyring.pkg.tar.zst' 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-mirrorlist.pkg.tar.zst'
ㅤ

    sudo nvim /etc/pacman.conf
ㅤ

      [chaotic-aur]  
      Include = /etc/pacman.d/chaotic-mirrorlist
      
# Get yay

    sudo pacman -S --needed git base-devel && git clone https://aur.archlinux.org/yay.git && cd yay && makepkg -si

# Install ZSH
    sudo pacman -S zsh zsh-completions && chsh -s /usr/bin/zsh
    
- git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
- git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
- git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k

      nvim ~/.zshrc

/plugins
- plugins=( git zsh-autosuggestions zsh-syntax-highlighting )

/ZSH_THEME
- ZSH_THEME="powerlevel10k/powerlevel10k"

      source .zshrc

# Installing fish

    sudo pacman -S fish fisher && fisher install IlanCosman/tide@v5 && chsh -s /usr/bin/fish

# Packages to Install

requirements:

    sudo pacman -S git ksh scrcpy npm netctl dialog recode net-tools jq curl wget cargo locate blueman htop bpytop neofetch fastfetch zip unzip unrar nodejs make python podman gvfs cmatrix vi vim neovim ufw tlp tlp-rdw lib32-mesa lib32-amdvlk lib32-vulkan-radeon vulkan-radeon amdvlk lib32-alsa-plugins lib32-libpulse lib32-openal speech-dispatcher lsb-release network-manager-applet wine-stable ffmpegthumbnailer tumbler pipewire pipewire-pulse pavucontrol flatpak && sudo systemctl enable tlp.service && sudo pacman -Syu

applications:

    sudo pacman -S pamac-nosnap antimicrox bitwarden celluloid thunar alacritty kitty kdenlive obs-studio piper qbittorrent qdirstat rustdesk-bin parsec-bin spotify vscodium upscayl-bin ungoogled-chromium youtube-music-bin metadata-cleaner akregator nuclear-player-bin cheese granatier jre-openjdk jdk-openjdk && git clone https://github.com/NvChad/NvChad ~/.config/nvim --depth 1 && nvim

flatpak:

    flatpak install spacecadetpinball flatseal jstest_gtk md.obsidian.Obsidian

AUR:

    yay -S pup pfetch cpufetch tuxi devour firefox-pwa-bin urn-git lyrebird spotube-bin easyssh

Driver
-

    yay -S optimus-manager
ㅤ

    yay -S mesa lib32-mesa vulkan-intel vulkan-icd-loader ocl-icd lib32-ocl-icd intel-compute-runtime xf86-video-ati xf86-video-intel xf86-video-amdgpu libva-mesa-driver lib32-libva-mesa-driver mesa-vdpau lib32-mesa-vdpau

reboot

Editing tuxi config
-

nvim /usr/bin/tuxi

line 18

    [ -n "$TUXI_LANG" ] && LANGUAGE="$TUXI_LANG" || LANGUAGE="tr"

line 886
      
    user_agent="Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) QtWebEngine/5.15.2 Chrome/87.0.4280.144 Safari/537.36"


# Installing Zen kernel
- sudo pacman -S linux-zen linux-zen-headers
- sudo nvim /etc/default/grub

/GRUB_SAVEDEFAULT="true"  
remove # (uncomment)

/GRUB_DEFAULT=0  
make GRUB_DEFAULT=saved

    sudo grub-mkconfig -o /boot/grub/grub.cfg

reboot

on the grub menu, select the linux-zen kernel. on the next time will automatically select the zen kernel

# Changing GRUB time
- sudo nvim /etc/default/grub

/GRUB_TIMEOUT=5  
make GRUB_TIMEOUT=0

    sudo grub-mkconfig -o /boot/grub/grub.cfg

reboot

# Mounting Disk

first, creating mount folder
- cd /mnt
- sudo mkdir Depo

list disks uuid
- lsblk -f

or
- ls -l /dev/disk/by-uuid              

then
- sudo nvim /etc/fstab

      UUID=uuid_paste_here              /mnt/Depo     ntfs     defaults      0 0
- systemctl daemon-reload
- sudo mount -a

reboot

# Adding SWAP (4GiB)
- sudo dd if=/dev/zero of=/swapfile bs=1M count=4096
- sudo chmod 600 /swapfile
- sudo mkswap /swapfile
- sudo swapon /swapfile
- swapon --show
- sudo nvim /etc/fstab

      /swapfile                                 none           swap    defaults         0 0

reboot

Deleting Swap file
-
- sudo swapoff -v /swapfile
- sudo rm /swapfile

reboot

# Showing stars on sudo password
- sudo nvim /etc/sudoers

add

    Defaults pwfeedback

# *Shortcuts*

rofi -modi drun -show drun -show-icons


    firefox
    # open firefox
    $mod+w
    -firefox

    terminal
    # open konsole
    $mod+enter
    -konsole

    ksysguard
    # open kde system guard
    $mod+h
    -systemmonitor

    discovery
    # open discover
    $mod+shift+s
    -plasma-discover

    pamac
    # open pamac
    $mod+shift+p
    -pamac-manager

ALT + Q = killactive

# Firefox config

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

# KDE

-Konsole

install edna theme and set transparecsty %50

-Plasma

install tokyo night and set splash arch theme

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

Removing color on noefetch
-

      sudo nvim /home/taha/.config/neofetch/config.conf

- Add # on **info cols**

--------------------------------------------------
If notifications will not working correctly
-

      sudo pacman -S knotifications knotifyconfig
  
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

# Hyprland
 
    sudo pacman -S hyprland xdg-desktop-portal-hyprland qt5-wayland qt6-wayland qt5ct qt6ct waybar hyprpaper hyprpicker wl-clipboard cliphist swaybg mako dunst swaylock grimblast grim tesseract tesseract-data-eng tesseract-data-tur tesseract-data-rus tesseract-data-deu wlrobs-hg nwg-look polkit-kde-agent playerctl

reboot.
