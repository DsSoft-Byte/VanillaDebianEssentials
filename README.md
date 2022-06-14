# VanillaDebianEssentials
My often-updated list of essential debian mods/patches to improve the amazing distro for vanilla enjoyers.

# For minecrafters, that drag click
There is a *bug*  in libinput that caps the CPS on 8?! there is DragClickOnLinux.sh here in #main to fix this issue,
it will restart the PC immediatly after execution so take care of that.

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

# Removing cdrom from sources
sudo sed -i '/cdrom/d' /etc/apt/sources.list

# Loading i2c module on boot (openrgb essential)
sudo nano /etc/modules.list

*add*  i2c-dev

# Fixing the stupid delay on volume change with keyboard buttons
sudo nano /etc/pulse/daemon.conf

*uncomment*  enable-deferred-volume  *set "yes" to "no"*

pulseaudio -k && pulseaudio --start

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

# To be continiued
To add to this list, clone or pull request
Will add what i will need later on.
