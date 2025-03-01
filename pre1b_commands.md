# Fedora 41 Post-installation Commands

Resources
- [ItsFoss](https://itsfoss.com/things-to-do-after-installing-fedora/)
- [HackingTheHike](https://www.hackingthehike.com/)
- [dnf5 docs](https://dnf5.readthedocs.io/en/latest/dnf5.conf.5.html#options-for-both-main-and-repo)
- [RPM Fusion](https://rpmfusion.org/Configuration)
- [NVIDIA drivers](https://rpmfusion.org/Howto/NVIDIA)

## Edit the DNF configuration file
```bash
$ sudo vi /etc/dnf/dnf.conf
```
Add the following lines to the file

```config
max_parallel_downloads=10
fastestmirror=True
deltarpm=True
```
## Update & Reboot
```bash
$ sudo dnf update
# Reboot system
$ systemctl reboot
```
## RPM Fusion repositories
```bash
$ sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm

$ sudo dnf config-manager setopt fedora-cisco-openh264.enabled=1
```
Check the newly added repos
```bash
$ ls /etc/yum.repos.d/
```

Re-run the update command with `refresh` flag
```bash
$ sudo dnf update --refresh
```
Run the following commands
```bash
$ sudo dnf update @core
$ sudo dnf install rpmfusion-free-release-tainted
$ sudo dnf install rpmfusion-nonfree-release-tainted 
$ sudo dnf install dnf-plugins-core
```

## Multimedia related packages
```bash
$ sudo dnf group install multimedia
$ sudo dnf install gstreamer1-plugin-openh264 mozilla-openh264
$ sudo dnf group install sound-and-video
```

## Installing a package using Terminal
```bash
$ sudo dnf install <package name>
# Example
$ sudo dnf install vlc
```

## Additional packages
```bash
$ sudo dnf install unzip p7zip p7zip-plugins unrar
$ sudo dnf install gedit vim
```

## Disabling SELINUX
Check the status
```bash
$ sestatus
```
Open `selinux` file with `vim`
```bash
$ sudo vim /etc/sysconfig/selinux
```
Edit the line following line
```config
SELINUX=enforcing
```
to
```config
SELINUX=disabled
```
Reboot system and check the status again

## NVIDIA drivers
Check the device
```bash
$ lspci | grep -e VGA
```

Run
```bash
$ sudo dnf install akmod-nvidia
```

If you have a CUDA compatible card, run
```bash
$ sudo dnf install xorg-x11-drv-nvidia-cuda
```

Build and install drivers by running
```bash
$ sudo akmods
$ systemctl reboot
```
If this step is skipped, the drivers will be installed during your next reboot.

Check the installed drivers
```bash
$ nvidia-smi
```
