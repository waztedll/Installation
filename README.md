
# Connecting to Wi-Fi
- iwctl
- device list
- station wlan0 scan
- station wlna0 get-networks
- station wlan0 connect <your wifi name>
- station wlan0 show
- ping gnu.org

The system has been installed, run:
sudo pacman -Syu

-If you need refresh to keys:

- sudo pacman -S archlinux-keyring
- sudo pacman-key --list-keys bretti@i--b.com
- sudo pacman-key --refresh

# Installation
After the Install

-Configure & Speed Up Pacman

- sudo nano /etc/pacman.conf

- Remove # on-desktop-portal-hyprland-git
- Color
- Parallel Downloads = 5
- [multilib]
- Include = /etc/pacman.d/mirrorlist

Add
- ILoveCandy

-Update pacman

- sudo pacman -Sy

-Updating mirrorlist

- sudo pacman -S reflector
- sudo cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.bak
- sudo reflector --verbose --latest 10 --protocol https --sort rate --save /etc/pacman.d/mirrorlist
- sudo pacman -Sy

# Get yay
- sudo pacman -S --needed git base-devel && git clone https://aur.archlinux.org/yay.git && cd yay && makepkg -si

# Install ZSH
- echo $SHELL
- sudo pacman -S zsh zsh-completions
- chsh -l
- chsh -s chsh -s /usr/bin/zsh
- git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
- git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

/plugins
- plugins=(
    git
    zsh-autosuggestions
    zsh-syntax-highlighting
)

- git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
- nvim .zshrc
- set theme "powerlevel10k/powerlevel10k"
- source .zshrc

# Packages to Install

-Install

git
tlp
pup
recode
jq
curl
vi
vim
nvim
mako
dunst
touch
wget
cargo
locate
htop
bpytop
neofetch
pfetch
ufetch
cpufetch
zip
unzip
make
python
podman
gvfs
nodejs
unrar
cmatrix (optional)
enable firefox pwa
rofi
netctl
dialog
npm
scrcpy

AUR packages:
devour
tuxi
pup
touch
pfetch
cpufetch

lib:
- lib32-alsa-plugins lib32-libpulse lib32-openal

In one code: 
- sudo pacman -Syu git tlp scrcpy npm netctl dialog recode jq curl wget cargo locate htop bpytop neofetch zip unzip unrar nodejs make python podman gvfs cmatrix vi vim neovim mako dunst lib32-alsa-plugins lib32-libpulse lib32-openal && sudo pacman -Syu

reboot

-Editing tuxi config

18- [ -n "$TUXI_LANG" ] && LANGUAGE="$TUXI_LANG" || LANGUAGE="tr"

886- user_agent="Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) QtWebEngine/5.15.2 Chrome/87.0.4280.144 Safari/537.36"

-Enable firefox pwa
- yay firefox-pwa-bin

# Applications
pamac
antimicrox
bitwarden
celluloid
thunar
alacritty
jstest-gtk
kitty
kdenlive
mousai
obs studio
obsidian
piper
qbittorrent
qdirstat
rustdesk
spotify
urn-git
code

# Installing Zen kernel
- sudo pacman -S linux-zen linux-zen-headers
- sudo nvim /etc/default/grub
- search /GRUB_SAVEDEFAULT=true

remove # (uncomment)

- search /GRUB_DEFAULT=0

make GRUB_DEFAULT=saved

- sudo grub-mkconfig -o /boot/grub/grub.cfg

reboot

on the grub menu, select the linux-zen kernel. on the next time will automaticly select

# Changing GRUB time
- sudo nvim /etc/default/grub
- search /GRUB_TIMEOUT=5

 make GRUB_TIMEOUT=0

- sudo grub-mkconfig -o /boot/grub/grub.cfg

reboot

# Mounting Disk

first, creating mount folder
- cd /mnt
- sudo mkdir Depo

list disks with uuid
- lsblk -f

or
- ls -l /dev/disk/by-uuid              

then
- sudo nvim /etc/fstab
UUID=uuid_paste_here              /mnt/Depo     ntfs     defaults      0 0
- :wq!
- sudo mount -a
- systemctl daemon-reload
- sudo mount -a

reboot

# Adding SWAP (4GiB)
- sudo dd if=/dev/zero of=/swapfile bs=1M count=4096
- sudo chmod 600 /swapfile
- sudo mkswap /swapfile
- sudo swapon /swapfile
- swapon --show

- sudo nano /etc/fstab

/swapfile                                 none           swap    defaults         0 0

reboot

# Showing stars on sudo password
- sudo nvim /etc/sudoers
- Defaults pwfeedback

# Then
-Change firefox config bkz: .mozilla

-Check the bluetooth

If bluetooth not working, run this commands

- sudo rfkill list
- sudo rfkill unblock bluetooth
- sudo systemctl status bluetooth
- sudo systemctl start bluetooth
- sudo systemctl status bluetooth

-Check the PS3 controller

Truth & Authorise

-Removing color on noefetch

- sudo nvim /home/taha/.config/neofetch/config.conf

Add # on info cols

-Installing wine

- sudo pacman -S wine wine-mono wine-gecko

-Install flatpak

- sudo pacman -S flatpak

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

-Needed
extensions.pocket.enabled = false
browser.send_pings = false
dom.event.clipboardevents.enabled = false
media.eme.enabled = false
media.navigator.enabled = false
beacon.enabled = false
browser.safebrowsing.downloads.remote.enabled = false
network.IDN_show_punycode = true

-For Google IP
geo.enabled = false
geo.wifi.uri = blank
browser.search.geoip.url = blank

-For ultra super privacy

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

# Spotify

- bash <(curl -sSL https://raw.githubusercontent.com/SpotX-CLI/SpotX-Linux/main/install.sh)

# Java

- sudo pacman -S jre-openjdk
- sudo pacman -S jdk-openjdk
- java -version

# Snap

- yay -Sy snapd
- sudo systemctl enable snapd
- sudo systemctl start snapd

# Chaotic AUR

- sudo pacman-key --recv-key 3056513887B78AEB --keyserver keyserver.ubuntu.com
- sudo pacman-key --lsign-key 3056513887B78AEB
- sudo pacman -U'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-keyring.pkg.tar.zst' 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-mirrorlist.pkg.tar.zst'
- sudo nvim /etc/pacman.conf
- [chaotic-aur]
  Include = /etc/pacman.d/chaotic-mirrorlist
      
# KDE

-Konsole

install edna theme and set transparecsty %50

-Plasma

install tokyo night and set splash arch theme

# Notification

knotifications % knotifyconfig packages download
- sudo pacman -S knotifications knotifyconfig
go to settings and notifications then enable all authentication pushs

-Clipboard

go to clipboard setings and set keyboard shotcut "Show Items at Mouse Posittion" Meta+V

# Hyprland
 
- sudo pacman -Syu hyprland xdg-desktop-portal-hyprland qt5-wayland qt6-wayland qt5ct qt6ct waybar hyprpaper blueman swaybg mako dunst nwg-look polkit-kde-agent && pacman -Syu
- yay -S xdg-desktop-portal-hyprland-git

reboot.
