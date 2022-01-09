# SteelSeries Arctis 9 fix for Ubuntu 20.04/Linux Mint 20

## Notes

* This should work with any distribution that uses PulseAudio 13.99/14.x, but the paths where you have to put the files may be different for other distributions.
* **PulseAudio 15 already has a patch to fix the issue with the Arctis 9.** If your distro is using PulseAudio 15 and it still doesn't work, this repo will probably not help you.
* I have only tested this on Linux Mint 20.3, which is based on Ubuntu 20.04. Use at your own risk.

## Install

### 1. Check your version of PulseAudio

Check your version of PulseAudio:
```
$ pactl --version
```

The result should look something like this:
```
pactl 13.99.1
Compiled with libpulse 13.99.0
Linked with libpulse 13.99.0
```

This solution is designed to work with versions 13.99/14.x. It probably won't work with other versions.

### 2. Unplug your headset.

### 3. Copy the files to where they need to be

**Please note that these file paths are specific to Ubuntu 20.04 and its derivatives. Other distributions may use different paths.**

```
$ sudo cp 99-arctis9.rules /lib/udev/rules.d
$ sudo cp steelseries-arctis-common-usb-audio-arctis9.conf /usr/share/pulseaudio/alsa-mixer/profile-sets
```

### 4. Restart PulseAudio and udevd

```
$ pkill pulseaudio
$ sudo udevadm control --reload-rules
$ sudo udevadm trigger
```

### 5. Plug your headset back in.

Check the Sound control panel shows the two output devices and one input device.

## Uninstall

### 1. Unplug your headset.

### 2. Remove the files

```
$ sudo rm /lib/udev/rules.d/99-arctis9.rules
$ sudo rm /usr/share/pulseaudio/alsa-mixer/profile-sets/steelseries-arctis-common-usb-audio-arctis9.conf
```

### 3. Restart PulseAudio and udevd

```
$ pkill pulseaudio
$ sudo udevadm control --reload-rules
$ sudo udevadm trigger
```

## Other headsets?

Maybe! Add the appropriate udev rule to the `99-arctis9.rules` and see! If you do, let me know if it works for you.

