# Raspberry PiHole Zero

This installation is build on top of [Hypriot OS](https://hypriot.com/) which has Docker pre-installed. Where applicable, it's built with the assumption that Macs will be used to connect/interface with the raspberry pi (e.g. choice of network mount)

## Flash OS to SD Card

### Install Flash tool
Follow the installation instructions [here](https://github.com/hypriot/flash#installation) to install the Flash tool.

### Download user-data.yaml file

Download the following files:
- https://github.com/austinmcconnell/raspberry-pihole/blob/master/user-data.yaml.sample
- https://github.com/austinmcconnell/raspberry-pihole/blob/master/config.txt

Rename user-data.yaml.sample to user-data.yaml

Edit the file and change the following items:
 - password for the pihole user
 - Set your wifi name as the ssid value
 - Set your wifi password as the psk value 

**Note: The Raspberry Pi Zero can only connect to 2.4 GHz wifi networks, not 5 GHz networks**

### Format your SD card

Format your SD card as exfat with a Master Boot Record with the following command:

```bash
diskutil eraseDisk exfat pihole MBRFormat /dev/diskN
```

Flash HypriotOS to your SD card by running the following command:

```bash
flash --userdata path/to/user-data.yml --bootconf path/to/config.txt https://github.com/hypriot/image-builder-rpi/releases/download/v1.11.1/hypriotos-rpi-v1.11.1.img.zip
```

Insert the SD card into the raspberry pi, plug in hdmi cable (optional), and power up the raspbery pi zero. It'll take at least 5 minutes to updated all the packages.

## SSH into Server

After 5 - 10 minutes have passed, try to ssh into your raspberry pi zero.

```bash
ssh pihole@pihole.local
```

If you didn't change the password earlier, the default password is `hypriot`. **CHANGE IT**. Simply type the following command and you'll be able to change your password

```bash
$ passwd
```

Install Pi Hole.

```bash
curl -sSL https://install.pi-hole.net | bash
```
