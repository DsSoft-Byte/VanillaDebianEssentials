# VanillaDebianEssentials
My often-updated list of essential debian mods/patches to improve the amazing distro for vanilla enjoyers.

# For minecrafters, that drag click
There is a *bug*  in libinput that caps the CPS on 8?! there is DragClickOnLinux.sh here in #main to fix this issue,
it will restart the PC immediatly after execution so take care of that.

# Enable Panel and window border transparency!
To get an effect like in the screenshot go to KDE Settings -> Workspace Behaviour -> Desktop Effects -> Untick "Background Contrast" and "Blur"
Right Click the bottom dock panel go to edit mode, enable transparency! Done!

# Add yourself to the sudo group
sudo usermod -aG sudo newuser

relog and you will be in the group

sudo whoami

expected output: root

# nvidia, fuck you
Debian comes natively with the nouveau graphics drivers for nvidia GPUs. This will help you to install the proprietary drivers.
nvidia 340 drivers and under are only supported on Buster and older!

su

sudo init 3

Press Alt + F1 if init 3 did not place you in an terminal

sudo nano /etc/modprobe.d/blacklist.conf
blacklist nouveau
blacklist lbm-nouveau
options nouveau modeset=0
alias nouveau off
alias lbm-nouveau off

sudo nano /etc/default/grub
*add*  nouveau.modeset=0  *before*  **Quiet**

sudo nano /etc/modprobe.d/nouveau-kms.conf
options nouveau modeset=0

sudo update-initramfs -u

sudo shutdown -r now

sudo apt install nvidia-driver *will install NEWEST driver*

# Davinci Resolve Unsupported GPU....
sudo apt install nvidia-opencl-icd


# Adding missing dependencies
sudo apt-get -f install

# Removing cdrom from sources
sudo sed -i '/cdrom/d' /etc/apt/sources.list

# Loading i2c module on boot (openrgb essential)
sudo nano /etc/modules

*add*  i2c-dev

# Fixing the stupid delay on volume change with keyboard buttons
sudo nano /etc/pulse/daemon.conf (No need for this on KDE)

*uncomment*  enable-deferred-volume  *set "yes" to "no"*

pulseaudio -k && pulseaudio --start

# Lutris/Wine Windows games tools

sudo dpkg --add-architecture i386 && sudo apt update

sudo apt install nvidia-driver-libs:i386

WARNING: If you're forced to use a legacy driver, you will want to instead install one of nvidia-legacy-390xx-driver-libs:i386, nvidia-legacy-340xx-driver-libs:i386, or nvidia-legacy-304xx-driver-libs:i386. 

(Credits to the Debian documentation https://wiki.debian.org/NvidiaGraphicsDrivers)

# Java install
sudo dpkg -i jdk-18_linux-x64_bin.deb  **jdk-18** is variable to the version that will be newest!! i use jdk-18

sudo mkdir /usr/lib/jvm

sudo nano /etc/environment

Add this line in the environment file:

the "jdk18" depends how how the file in /usr/lib/jvm/XXX is named

JAVA_HOME="/usr/lib/jvm/jdk-18"

The commands below will inform the System that Java is installed in that patch and that this Java should be used instead of OpenJRE

sudo update-alternatives --install "/usr/bin/java" "java" "/usr/lib/jvm/jdk-18/bin/java" 0

sudo update-alternatives --install "/usr/bin/javac" "javac" "/usr/lib/jvm/jdk-18/bin/javac" 0

sudo update-alternatives --set java /usr/lib/jvm/jdk-18/bin/java

sudo update-alternatives --set javac /usr/lib/jvm/jdk-18/bin/javac


These Commands will output the patch of the installed version Make sure the patch is correct!!!!


update-alternatives --list java

update-alternatives --list javac



This command will output the installed version



java -version

# armv7l/Aarch64/Rpi Java Installation

sudo apt install -y wget apt-transport-https

sudo mkdir -p /etc/apt/keyrings

sudo wget -O - https://packages.adoptium.net/artifactory/api/gpg/key/public | sudo tee /etc/apt/keyrings/adoptium.asc

sudo echo "deb [signed-by=/etc/apt/keyrings/adoptium.asc] https://packages.adoptium.net/artifactory/deb $(awk -F= '/^VERSION_CODENAME/{print$2}' /etc/os-release) main" | sudo tee /etc/apt/sources.list.d/adoptium.list



# XFCE Log-in remember user
XFCE's "LightDM" GTK Greeter does not remember users so here is the fix:

su

sudo nano /etc/lightdm/lightdm.conf

#greeter-hide-users=false  *uncomment* should look like this: greeter-hide-users=false

Save and relog/reboot

# bspwm setup guide

https://dev.to/l04db4l4nc3r/bspwm-a-bare-bones-window-manager-44di

# MacOS KDE Plasma layout tutorial

https://store.kde.org/s/Opendesktop/p/1399346

# For Qt problems (Only applies to KDE Plasma)

sudo apt-get install qt4-qmake
sudo apt-get install qt5-qmake

# Run Dolphin (FileManager) as root

pkexec env DISPLAY=$DISPLAY XAUTHORITY=$XAUTHORITY KDE_SESSION_VERSION=5 KDE_FULL_SESSION=true dolphin

# Install Kvantum (KDE)

sudo apt install qt5-style-kvantum qt5-style-kvantum-themes

# Beautiful "Rice" & easy to do

Using Pax theme

* Pax-Kvantum theme
* Kvantum dark application style
* Pax Look-and-Feel "Global" theme
* Shiny-Plasma style
* Relaxed-Icons
* Pax aurorae Window decorations

Look "neofetch.png"

# Fix "Concurrent Streams" issue on Bookworm

Please note, that this "hack/edit" will "upgrade" your system to "unstable"

* sudo nano /etc/apt/sources.list
* delete everything except the 2 first lines
* edit your sources.list like below

deb http://deb.debian.org/debian/ unstable main non-free contrib

deb-src http://deb.debian.org/debian/ unstable main non-free contrib

* Only these two lines should be in your sources.list, update and security entries are not needed becuase unstable = rolling, like Arch.



# To be continiued
To add to this list, clone or pull request
Will add what i will need later on.
