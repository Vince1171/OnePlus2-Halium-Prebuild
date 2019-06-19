# OnePlus2-Halium-Prebuild

## what works what don't work?
 * [x] boot
  * [x] graphics
  * [ ] calls
  * [x] sound
  * [x] gps
  * [x] wifi (FIXED)
  * [ ] Bluetooth (WIP+)
  * [ ] Camera
  * [x] anbox


### For Ubuntu Touch

just use the prebuild image just as  a normal compiled image.
install it with the JBB's halium-install script [here](https://github.com/JBBgameich/halium-install)
and get the ubports edge rootfs from [here](https://ci.ubports.com/job/xenial-hybris-edge-rootfs-armhf/lastSuccessfulBuild/artifact/out/ubuntu-touch-hybris-xenial-edge-armhf-rootfs.tar.gz)
```./halium-install -p ut ubuntu-touch-hybris-xenial-edge-armhf-rootfs.tar.gz system.img```
```sudo fastboot flash boot halium-boot.img```

then while in TWRP
```adb shell 'touch /data/.writable_image; mkdir /a; mount /data/rootfs.img /a; echo manual | tee /a/etc/init/rsyslog.override;  touch /a/.writable_device_image; umount /a; sync'```


some command are needed in order to get a working UT device (run as root).
```
chmod 666 /dev/kgsl-3d0
adduser --force-badname --system --home /nonexistent --no-create-home --quiet _apt
echo manual | tee /etc/init/apparmor.override
```

### For Ubuntu Touch Anbox (WIP)

follow the instruction above, then follow this.

~reflash the boot~ (anbox binder is now integrated into the default halium-noot.img)

```sudo fastboot flash boot halium-boot-anbox.img```

 ~check if exist~
~/dev/anbox-binder~


~if it doesn't, you are not using the right halium-boot~

then
```
sudo apt install anbox-ubuntu-touch
sudo wget -q --show-progress -O /home/phablet/anbox-data/android.img http://cdimage.ubports.com/anbox-images/android-armhf-64binder.img
touch /home/phablet/anbox-data/.enable
```
<br />
some permition fixes are needed.

```
sudo chmod -R o+wrx /home/phablet/anbox-data/data
sudo start -q anbox-container
#personnaly this one fail
start -q anbox-session
```

reboot, wait 2 minutes then reboot again
