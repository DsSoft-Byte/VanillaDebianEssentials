# VanillaDebianEssentials
My often-updated list of essential debian mods/patches to improve the amazing distro for vanilla enjoyers.

# For minecrafters, that drag click
There is a *bug* in libinput that caps the CPS on 8?! there will be an script to fix that uploaded soon or may already be here in #main
It will restart the PC immediatly after execution so take care of that.

# nvidia, fuck you
Debian comes natively with the nouveau graphics drivers for nvidia GPUs so this will fix that
nvidia 340 drivers and under are only supported on Buster and older!

su
sudo init 3

Press Alt + F1 is init 3 did not place you in an terminal

sudo nano /etc/modprobe.d/blacklist.conf
blacklist nouveau
blacklist lbm-nouveau
options nouveau modeset=0
alias nouveau off
alias lbm-nouveau off

sudo nano /etc/default/grub
*add* nouveau.modeset=0 *before* **Quiet**

sudo nano /etc/modprobe.d/nouveau-kms.conf
options nouveau modeset=0

sudo update-initramfs -u

sudo shutdown -r now

sudo apt install nvidia-driver *will install NEWEST driver*

# Removing cdrom from sources
sudo sed -i '/cdrom/d' /etc/apt/sources.list

# Loading i2c module on boot (openrgb essential)
sudo nano /etc/modules.list
*add* i2c-dev

# Fixing the stupid delay on volume change with keyboard buttons
sudo nano /etc/pulse/daemon.conf
*uncomment* enable-deferred-volume *set "yes" to "no"*
pulseaudio -k && pulseaudio --start

# To be continiued
To add to this list, clone or pull request
Will add what i will need later on.
