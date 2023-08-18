# Raspberry Pi 4 Setup Instructions

* Use 2022-01-28-raspios-bullseye-armhf.img Latest GUI based OS install (needs to be the 32 bit version i think)
* Use the Raspberry Pi Imager to set up WIFI,SSH,DATETIME etc... UPON install
* Complete the rest VIA SSH
* The below was done with the main user named "Administrator"

```
sudo raspi-config
-enable vnc
```

Update System

```
sudo apt-get update
sudo apt-get upgrade
```

Install ftpd (optional for easier file uploads)

```
sudo apt-get install pure-ftpd
```

Set virtual monitor so no screen is required. I used Mode 4
(mode 76 is 1080/60hz) 
(mode 4 is 720/60hz)

```
sudo nano /boot/config.txt

hdmi_force_hotplug=1
hdmi_group=1
hdmi_mode=76
```
Then reboot

Install Open Frameworks

```
wget https://openframeworks.cc/versions/v0.11.0/of_v0.11.0_linuxarmv6l_release.tar.gz
mkdir openFrameworks
tar vxfz of_v0.11.2_linuxarmv6l_release.tar.gz -C openFrameworks --strip-components 1

cd /home/administrator/openFrameworks/scripts/linux/debian
sudo ./install_dependencies.sh

make Release -C /home/administrator/openFrameworks/libs/openFrameworksCompiled/project
```

REMOVE libopenmaxil from library includes, this lib is not included in the latest OS ISO and casues all project builds to fail

```
nano /home/administrator/openFrameworks/libs/openFrameworksCompiled/project/linuxarmv6l/config.linuxarmv6l.default.mk 
// coment out "# PLATFORM_LIBRARIES += openmaxil"
```

To test if all worked well, go into the examples directy and into any of the projects, i sugest eth graphics ones. make then run

```
cd into example project dir
make
then ./bin/projectname to run
```
