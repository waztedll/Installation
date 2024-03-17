The system has been installed, run:

    sudo pacman -Syu

## If you need refresh to keys:

    sudo pacman -S archlinux-keyring && sudo pacman-key --refresh && sudo pacman-key --list-keys brett@i--b.com

# Beginning install

## Configure & Speed Up Pacman

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

# Chaotic AUR

firstly, downloading required packages

    sudo pacman-key --recv-key 3056513887B78AEB --keyserver keyserver.ubuntu.com && sudo pacman-key --lsign-key 3056513887B78AEB && sudo pacman -U 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-keyring.pkg.tar.zst' 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-mirrorlist.pkg.tar.zst' --noconfirm

then editing the pacman config

    sudo vim /etc/pacman.conf

include this codes

    [chaotic-aur]  
    Include = /etc/pacman.d/chaotic-mirrorlist

# Packages to Install

## requirements:

    sudo pacman -S inxi linux-headers man-db git base-devel yay fast pup scrcpy yt-dlp ytfzf \
                   netctl dialog bind recode net-tools jq wget locate htop btop android-tools \
                   fastfetch pfetch zip unzip p7zip unrar make gvfs libva xsensors cmatrix \
                   rsync vi vim neovim starship tlp qt5ct qt6ct gnome-keyring firefox-pwa fzf \
                   ttf-hack ttf-hack-nerd otf-font-awesome ttf-jetbrains-mono-nerd noto-fonts-emoji neofetch \
                   translate-shell lsb-release network-manager-applet wine-stable kdialog \
                   ffmpegthumbnailer tumbler brightnessctl playerctl pipewire pipewire-pulse \
                   python-requests wireplumber pamixer pavucontrol kvantum mpv mpv-mpris mtpfs \
                   dracula-gtk-theme-git gtk-layer-shell gvfs-mtp pacman-contrib thefuck \
                   cava tty-clock xdg-desktop-portal xdg-desktop-portal-gtk rate-mirrors --needed

#### tlp

    sudo systemctl enable --now tlp.service

## applications:

    yay -S firefox alacritty pamac-nosnap bitwarden thunar anki syncthing \
           kdeconnect kdiskmark thunderbird obs-studio piper qbittorrent cpu-x \
           vscodium discord ventoy thunar-volman thunar-archive-plugin \
           kweather ksysguard gnome-system-monitor viewnior krita steam upscayl \
           ungoogled-chromium youtube-music-git metadata-cleaner gnome-dictionary \
           dialect okular obsidian marker qmmp protonvpn-cli \
           xarchiver neovide jre-openjdk --needed

audio: `easyeffects audacity lsp-plugins-lv2`

optional: `gimp kdenlive antimicrox goverlay qdirstat celluloid kitty epiphany signal-desktop nuclear-player-bin xdman lutris heroic-games-launcher-bin tor-browser-bin librewolf epiphany octopi prismlauncher video-downloader duckstation-git hypnotix ruffle-git lightspark notesnook-bin logseq-desktop-bin stremio armcord discover-overlay mousai songrec soundux tokodon kdevelop handbrake 0ad osu ppsspp rustdesk parsec calibre dino wike gtkcord4 cpu-x github-desktop harmonoid davinci-resolve protonlaunch mcpelauncher-ui waypaper-git shotcut flowblade olive vidcutter neovide edex-ui wireshark`

game: `mindustry wesnoth granatier`

## flatpak:

    yay -S flatpak && flatpak --user remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo && flatpak install com.github.tchx84.Flatseal com.github.k4zmu2a.spacecadetpinball io.gitlab.jstest_gtk.jstest_gtk

## AUR:

    yay -S tuxi-git urn-git lyrebird sklauncher-bin localsend-bin fluent-reader-electron-bin

tool: `sherlock-git`  
game: `dol-git`

# Installing WM

## i3

    yay -S i3 polybar rofi picom scrot xclip xorg-xclipboard xcolor xwallpaper --needed

## Hyprland

    yay -S hyprland waybar xdg-desktop-portal-hyprland qt5-wayland qt6-wayland \
           hyprpaper hyprpicker grimblast slurp grim nwg-look wl-clipboard cliphist dunst \
           swaylock-effects rofi-lbonn-wayland tesseract tesseract-data-eng \
           tesseract-data-tur tesseract-data-rus tesseract-data-deu wlrobs-hg wlogout \
           webcord polkit-kde-agent --needed

# Installing Shell

## fish

    sudo pacman -S fish fisher && fish && fisher install IlanCosman/tide@v6 && chsh -s /usr/bin/fish

## Zsh

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

## Changing Limine time

    sudo nvim /boot/limine.cfg

make TIMEOUT=0

## Mounting Disk

first, creating mount folder
- `cd /mnt`
- `sudo mkdir Depo`

list disks uuid
- `lsblk -f` or `ls -l /dev/disk/by-uuid`              

then
- `sudo nvim /etc/fstab`

      UUID=paste_uuid_here              /mnt/Depo     ntfs     defaults      0 0
  
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

# Useful things

## Connecting to Wi-Fi

    nmtui

edit the connections and on ipv4 settings select the addresses only n enter the following ip addresses;

    9.9.9.9, 149.112.112.112

## Driver

for dual gpus:

    yay -S optimus-manager

for intel gpu:

    yay -S mesa lib32-mesa libva-mesa-driver lib32-libva-mesa-driver libva-intel-driver lib32-libva-intel-driver xf86-video-intel vulkan-intel lib32-vulkan-intel vulkan-icd-loader lib32-vulkan-icd-loader --needed

for amd gpu:

    yay -S mesa lib32-mesa libva-mesa-driver lib32-libva-mesa-driver xf86-video-amdgpu vulkan-radeon lib32-vulkan-radeon vulkan-icd-loader lib32-vulkan-icd-loader --needed

for bluetooth:

    yay -S bluez bluez-utils bluez-plugins bluez-qt5 blueman

for printers:

    yay -S cups

## Applying GTK & QT themes

for dracula kvantum: <https://store.kde.org/p/1370681/>  
for tokyonight-se icons: <https://github.com/ljmill/tokyo-night-icons>

### GTK

first download the dracula kvantum and tokyonight-se icons

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

    mkdir ~/backup/.config && mkdir ~/backup/.mozilla && mkdir ~/backup/.thunderbird && mkdir ~/backup/.themes && mkdir ~/backup/.icons

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

check and install

    sudo ./install_bin.sh
    sudo ./blockcheck.sh
    sudo ./install_easy.sh

## Adblock

    sudo curl -o /etc/hosts https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts

## Rofi

### Dictionary

- Download database via: <https://github.com/metwse/rofi-tdk.sh/releases/>

      sudo mv ~/Downloads/rofi-tdk.tar.gz /var/

## Showing stars on sudo password

    sudo nvim /etc/sudoers

add

    Defaults pwfeedback

## Editing tuxi config

`sudo nvim /usr/bin/tuxi`

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

- go to clipboard setings and set keyboard shortcut "Show Items at Mouse Posittion"

--------------------------------------------------
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
