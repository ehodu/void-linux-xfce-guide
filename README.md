## How to install minimal XFCE on Void Linux step by step? See:

### Booting
Obviously, you'll need a bootable USB drive with the Void base ISO. I strongly recommend Ventoy for this purpose. Download it here: [Ventoy](https://github.com/ventoy/Ventoy). 

### Initializing base system
Void will open a cli interface and request for a new login. The login is always _anon_ and the pass is _voidlinux_. After logging in, call the script `void-installer`. The screen will show some interfaces to configure network, packages, permissions, etc.

### Setting things up
In this step, you'll configure network, packages of ISO, mirrors, etc. See:

1 - _Keyboard_. Choose your default keyboard and press `Enter`. 

2 - _Network_. You'll have to put it manually. Put the network name, the protocol and the pass. For example, if your network's name is _Jane_, your protocol is _wpa_ (most common) and your pass is _jane123_, just do it on the fields. 

3 - _Source_. I strongly recommend select it from ISO, not from network. You'll get a minimal installation of the system by doing that.

4 - _Hostname_. Choose the PC hostname, like: _Void_, _VoidLinux_, or whatever you want. 

5 - _Locale_. Basically, the locale you are in. It'll appear with the language abreviation, the country abreviation and the unicode. Like: _en_US-UTF-8_. After that, choose your timezone. For example, _America/Sao_Paulo_. 

6 - _RootPassword_. If you don't wanna set any password for root access, just jump it. 

7 - _UserAccount_. Put your username to access system and choose a password for it. Like: _anon_ (user) and _meanon_ (pass). Afte that, choose what the user will control on system. I personally recommend the default choices and also _lp_, _network_, _users_, _storage_. To select options, press `Space`.  

8 - _BootLoader_. Choose GRUB, and set it to initialize with a graphical interface on your disk of installation. 

9 - _Partition_. That's the most simple part, don't be afraid. Select the disk and press for using _cfdisk_ (easy). It will open a black interface to set/delete/change type of partitions at the disk. If you already have partitions on disk, just delete all of them by changing one for one pressing _arrow_key_down_ in each one. Done, create a initial partition with 300M, and change its type to _EFI System_. Create another one to the the main system partition (_/_) and a last one to the the _/home_ partition, and let type by default (Linux filesystem). I don't recommend you using _swap_, do it by your own risk. Press _write_ when you finish it, and _quit_. 

10 - _Filesystems_. You'll have to configure some things on the disk partitions your just created. Click on it and select each partition previosly created. 

For example: 

_/dev/sda1_ 300M (click on `change`) |
type: vFAT (FAT32) |
mount point: _/boot/efi_

/dev/sda2 70G (click on `change`) |
type: ext4 |
mount point: _/_

/dev/sda3 100G (click on `change`) |
type: ext4 |
mount point: _/home_

Done, return to the main screen and click to install. Wait for system's installation and reboot system. Take out your USB and wait...

### Updating things

Your system will request your _login_ and _pass_. Void, by default, just accept installation of things using `sudo`. So, press `su`, type your pass and press `Enter`. You'll have a cli interface with a _#_. It means it worked. 

Then, just type all these commands I'll put here. That's a minimal installation with all things (basic) you'll need to use void. See:

```
xbps-install -u xbps 
xbps-install -Syu
xbps-install pulseaudio dbus xfce4 xorg-minimal xorg-fonts mesa-dri lightdm lightdm-gtk-greeter xfce4-terminal xfce4-plugins NetworkManager network-manager-applet

ln -s /etc/sv/dbus /var/service
ln -s /etc/sv/NetworkManager /var/service
ln -s /etc/sv/dbus /var/service
ln -s /etc/sv/lightdm /var/service
```
I won't explain how to use _bluetooth_ on it cause a possible way is to start it automatically on start, what is not a good choice. 

Done? Then type `reboot` and enjoy your system! Do these steps manually first, and one day I'll create a script to configure everything you need. Any question/suggestion? Lemme know. 

(Void is the best distro I've ever tried). 
