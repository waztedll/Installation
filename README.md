The system has been installed, run:
sudo pacman -Syu

-You need refresh to keys:

- sudo pacman -S archlinux-keyring
- sudo pacman-key --list-keys bretti@i--b.com
- sudo pacman-key --refresh

# Installation
After the Install

-Configure & Speed Up Pacman

- sudo nano /etc/pacman.conf

- Remove # on
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

/plugins
- plugins=( 
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
pup
recode
jq
curl
vim
nvim
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
nodejs
unrar
cmatrix (optional)
enable firefox pwa
rofi

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
- sudo pacman -Syu git recode jq curl wget cargo locate htop bpytop neofetch zip unzip unrar nodejs make python podman cmatrix vim neovim lib32-alsa-plugins lib32-libpulse lib32-openal

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

# Changing GRUB
- sudo nvim /etc/default/grub

GRUB_TIMEOUT=0

- sudo grub-mkconfig -o /boot/grub/grub.cfg

reboot

# Adding SWAP (4GiB)
- sudo dd if=/dev/zero of=/swapfile bs=1M count=4096
- sudo chmod 600 /swapfile
- sudo mkswap /swapfile
- sudo swapon /swapfile
- swapon --show

- sudo nano /etc/fstab

/swapfile                                 none           swap    defaults         0 0

reboot.

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

# KDE

-Konsole

install edna theme and set transparecsty %50

-Plasma

install tokyo night and set splash arch theme
