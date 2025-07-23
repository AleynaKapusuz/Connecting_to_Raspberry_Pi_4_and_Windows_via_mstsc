# Raspberry Pi’yi Uzaktan Masaüstü (MSTSC) ile Kullanmak

## 1- Raspberry Pi Imager’ı İndir

Windows kurulum dosyasını şu adresten alın: https://rpi.imager.

## 2- microSD’yi Hazırla

⚠️ İşletim Sistemi Seç: “Raspberry Pi OS (64-bit)” – Bookworm.

İmajı kartına yazın ve güvenli bir şekilde çıkarın.

## 3- İlk Açılış Ayarlarını Pi Üzerinden Yapın

Monitör, klavye ve fareyi bağlayın.

İlk kurulum sihirbazında SSH dâhil tüm bağlantı seçeneklerini etkinleştirin.

## 4- Windows’ta Pi’nin IP’sini Bulun
```
ping raspberrypi.local
```
Raspberry Pi'in içinden ayarlardan SSH'ı açın.

## 5- Pi’ye SSH ile Bağlanın
```
ssh pi@raspberrypi.local
```

## 6- Sistemi Güncelleyin
```
sudo apt update && sudo apt full-upgrade -y
sudo reboot
```

# XVNC ile başlatmalısın: 

## 7- TigerVNC sunucusunu kurun
```
sudo apt update
sudo apt install tigervnc-standalone-server tigervnc-common -y
sudo mkdir -p /usr/lib/xrdp
sudo ln -s /usr/lib/x86_64-linux-gnu/xrdp/libvnc.so /usr/lib/xrdp/libvnc.so
echo "startlxde" > ~/.xsession
sudo nano /etc/xrdp/startwm.sh
```

/etc/xrdp/startwm.sh dosyasının içi bu şekilde olmalı: 
```
#!/bin/sh
unset DBUS_SESSION_BUS_ADDRESS
unset XDG_RUNTIME_DIR
exec startxfce4
```

Daha sonra Servisleri yeniden başlat:
```
sudo systemctl restart xrdp
sudo systemctl restart vncserver-x11-serviced
```
```
vncserver :10
```

## 8- XRDP’yi Kurun ve Yapılandırın
```
sudo apt install -y xfce4 xfce4-goodies
sudo apt install xrdp -y
sudo raspi-config        # settings menu
# 3 → Display Options → D1 → select X11 (disable Wayland)
sudo systemctl enable xrdp
sudo systemctl restart xrdp
```
sudo nano /etc/xrdp/xrdp.ini
yazdıktan sonra xrdp.ini içi bu şekilde olmalı:
```
[Xvnc]
name=Xvnc
lib=libvnc.so
username=ask
password=ask
ip=127.0.0.1
port=-1
code=20
```

~/.xsession dosyanın iç kısmı bu şekilde olmalı:
```
#!/bin/sh
exec /usr/bin/startlxde-pi
```

## 9- XRDP Sorun Çözümü: Wayland Devre Dışı:
```
sudo apt install -y lightdm
```

Ardından sudo raspi-config tekrar → 5 Performance Options → P3 VNC → DISABLED (VNC, xrdp ile çakışır) yapın.

## 10- X11 Kurma:
```
sudo apt purge x11-utils x11-xserver-utils x11-session-utils xauth xfonts-100dpi xfonts-75dpi xfonts-scalable xinit xorg-docs-core
```

## 11- Windows’tan MSTSC ile Bağlanın

Win + R → mstsc yazın.

Computer: Pi’nin IP adresini girin.

Şifre: Pi’de belirlediğiniz kullanıcı şifresi.


Hepsi bu kadar — artık Raspberry Pi’nize Uzak Masaüstü (Remote Desktop) oturumu ile bağlanabilirsiniz.

## 12- MQTT Kurulumu ve Yapılandırması:

Mosquitto MQTT Broker kur:
```
sudo apt install -y mosquitto mosquitto-clients
sudo systemctl enable mosquitto
sudo systemctl start mosquitto
```

Durum kontrol:
```
sudo systemctl status mosquitto
```

Port kontrol (1883):
```
sudo netstat -tulnp | grep 1883
```
