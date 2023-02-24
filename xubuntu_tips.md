Xubuntu Tips and Commands
=========================

### Xubuntu Remove packages
```
sudo apt remove snapd libreoffice* thunderbird update-manager parole pidgin
sudo apt remove unattended-upgrades ubuntu-advantage-tools
sudo apt-mark hold snapd
sudo apt autoremove -y
```
### Xubuntu Packages to Install
```
sudo apt install ssh tmux mosh htop eog audaciou rssync git jq python3-pip net-tools 
sudo apt install rhythmbox grilo-plugins-0.3  plank apt-transport-https
sudo apt install csh gfortran 
```

## Install Microsoft Edge 
```
sudo apt install software-properties-common apt-transport-https wget
wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/edge stable main"
sudo apt install microsoft-edge-stable
```

## Install Visual Studio code
```
sudo apt-get install wget gpg
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg
sudo sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'
rm -f packages.microsoft.gpg
sudo apt update
sudo apt install code 
```



### .vimrc File Example
```
colorscheme darkblue
autocmd VimResized * wincmd =
filetype plugin on
if has("gui_running")
  " GUI is running or is about to start.
  " Maximize gvim window (for an alternative on Windows, see simalt below).
  set lines=30 columns=84
else
endif
```

### Find and convert all flac files to mp3 files 
use find
```
find -name "*.flac" -exec bash -c 'ffmpeg -i "{}" -y -acodec libmp3lame -ab 256k "${0/
.flac}.mp3"' {} \;
```
use for loop
```
for i in *.flac; do ffmpeg -i "$i" -ab 256k -map_metadata 0 -id3v2_version 3 -f mp3 "${i%.*}.mp3"; done
```

### Latitude Wireless Blink fix
```
sudo -i
echo 'options iwlwifi led_mode=1' >> /etc/modprobe.d/wlan.conf
modprobe -r iwlwifi && modprobe iwlwifi
```

### Pihole tcp 53 port Error Fix
```
sudo systemctl stop systemd-resolved
sudo systemctl disable systemd-resolved
```

### Burn iso to UBS Drive
assume usb drive is mounted in /dev/sdb
```
sudo dd bs=4M if=/media/share/software/xubuntu-18.04.5-desktop-amd64.iso of=/dev/sdb conv=fdatasync status=progress
```

### fstab entry for samba file
```
//192.168.68.130/sambashare /media/share cifs username=user,password=password,iocharset=utf8 0 0
```

### crontab entry
Back up everyday at 4 am
```
0 4 * * * rsync -avzh Documents/share /media/WD1500GB/
```

### Update docker-compose image
```
docker-compose pull
```

### pihole tcp 53 error
docker-compose up -d error, issue the following command
```
sudo systemctl stop systemd-resolved
sudo systemctl disable systemd-resolved
```

### powershell command to check disk io speed
run as admin
```
winsat disk -ran -write -drive c
winsat disk -ran -read -drive c
```
###  Rhythmbox DLNA 

```
After much searching on the internet without any real help I found the answer myself.

In Ubuntu 14.10 the default media player Rhythmbox can be used as a music client to access DLNA server. The only problem is that not all necessary files are installed by default.

There are just few steps to take:

Enable Grilo DLNA client in Rhythmbox. Go to Tools -> Plugins and make sure that "Grilo Media Browsing" (or similar) is enabled.

Install Grilo plugins. Open "Ubuntu Software Center", search for "grilo-plugins" and install package "grilo-plugins-0.2".

You are done now. Open Rhythmbox and should already see your DLNA server in the left column. You can browse it and play your music. If you do not see it, try clicking little "+" sign on the bottom left and then "Find new devices" (or similar). See picture below.
```
