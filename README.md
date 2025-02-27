## Hyprland for Void Linux

This repository contains template files for building [Hyprland](https://github.com/hyprwm/Hyprland) using xbps-src.

### Usage

1) You may want to start by making a directory where you can keep the relevant repositories

```
mkdir ~/repos
cd ~/repos
```

2) Set up a [void-packages](https://github.com/void-linux/void-packages) clone for building templates files

```
git clone https://github.com/void-linux/void-packages
cd void-packages
./xbps-src binary-bootstrap
cd ..
```

3) Clone this repository:

```
git clone https://github.com/Makrennel/hyprland-void.git
cd hyprland-void
```

4) Append shared libraries to the end of your void-packages shared libraries

```
cat common/shlibs >> ../void-packages/common/shlibs
```

5) Copy srcpkgs to your void-packages srcpkgs directory

```
cp -r srcpkgs/* ../void-packages/srcpkgs
```

6) Build and install packages

```
cd ../void-packages
./xbps-src pkg hyprland
sudo xbps-install -R hostdir/binpkgs hyprland
```

### Running

In order to run Hyprland you will need to install some additional packages which will depend on your setup, for example a [session and seat manager](https://docs.voidlinux.org/config/session-management.html) and [graphics drivers](https://docs.voidlinux.org/config/graphical-session/graphics-drivers/index.html).

### Updating

If Hyprland updates and this repository changes, you may want to perform a hard reset and clean of your cloned void-packages repository to ensure changes are correctly applied when repeating steps 4 and 5 after a git pull on both void-packages and hyprland-void. (BEWARE: This will also reset any changes you have made to any other packages locally - you will have to figure it out yourself in this case)

```
sudo xbps-install -Su # Update system normally first to avoid building every package needing update from source

cd ~/repos/void-packages
git clean -fd
git reset --hard
git pull

cd ../hyprland-void
git pull

cat common/shlibs >> ../void-packages/common/shlibs # Repeat steps 2 and 3
cp -r srcpkgs/* ../void-packages/srcpkgs

cd ../void-packages
./xbps-src update-sys
```

### Extra
This repository also includes other templates which may be of interest for:

- hyprpaper
- xdg-desktop-portal-hyprland

You may also be interested in [EWW](https://github.com/elkowar/eww), for which a template is available in a [separate repository](https://github.com/Makrennel/eww-void) as it is not specific to Hyprland.
