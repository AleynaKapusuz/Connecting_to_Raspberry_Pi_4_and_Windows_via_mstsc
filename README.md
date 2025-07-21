# Using Raspberry Pi via Remote Desktop (MSTSC)

## 1 – Download Raspberry Pi Imager
Get the Windows installer from: https://rpi.imager

## 2 – Prepare the microSD Card
⚠️ Choose OS: “Raspberry Pi OS (64-bit)” – Bookworm.

Write the image to your SD card and safely eject it.

## 3 – Perform Initial Setup on the Pi
Connect a monitor, keyboard, and mouse.

During the setup wizard, enable all network options including SSH.

## 4 – Find the Pi's IP Address on Windows
```
ping raspberrypi.local
```

## 5 – Connect to the Pi via SSH
```
ssh pi@raspberrypi.local
```

## 6 – Update the System
```
sudo apt update && sudo apt full-upgrade -y
sudo reboot
```
# You Must Use XVNC:
## 7 – Install TigerVNC Server
```
sudo apt update
sudo apt install tigervnc-standalone-server tigervnc-common -y
sudo mkdir -p /usr/lib/xrdp
sudo ln -s /usr/lib/x86_64-linux-gnu/xrdp/libvnc.so /usr/lib/xrdp/libvnc.so
echo "startlxde" > ~/.xsession
sudo nano /etc/xrdp/startwm.sh
```
Inside /etc/xrdp/startwm.sh, the content should be:
```
#!/bin/sh
unset DBUS_SESSION_BUS_ADDRESS
unset XDG_RUNTIME_DIR
exec startxfce4
```

Then restart services:

```
sudo systemctl restart xrdp
sudo systemctl restart vncserver-x11-serviced
```

Start the VNC session manually:

```
vncserver :10
```

## 8 – Install and Configure XRDP
```
sudo apt install xrdp -y
sudo raspi-config        # settings menu
# 3 → Display Options → D1 → select X11 (disable Wayland)
sudo systemctl enable xrdp
sudo systemctl restart xrdp
```
Then run sudo raspi-config again → 5 Performance Options → P3 VNC → DISABLED (VNC conflicts with xrdp).

9 – Connect from Windows using MSTSC
Press Win + R → type mstsc

In the “Computer” field, enter the Pi’s IP address.

Password: the user password you set during Raspberry Pi setup.

That’s it — you can now connect to your Raspberry Pi via Remote Desktop!
