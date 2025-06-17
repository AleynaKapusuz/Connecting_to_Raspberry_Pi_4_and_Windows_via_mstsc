# Connecting_to_Raspberry_Pi_4_and_Windows_via_mstsc

Connecting to a Raspberry Pi 4 and Windows via mstsc

# Raspberry Pi Remote-Desktop Setup — Step-by-Step

## 1- Raspberry Pi Remote-Desktop Setup — Step-by-Step (English)
Download Raspberry Pi Imager
Get the Windows installer from https://rpi.imager.

## 2- Flash the microSD

⚠️ Choose OS: “Raspberry Pi OS (64-bit)” – Bookworm.

Write the image and eject the card safely.

## 3- Do the first-boot setup on the Pi itself

Connect monitor, keyboard and mouse.

In the first-run wizard enable all connectivity options, including SSH.

## 4- Find the Pi’s IP from Windows
```
ping raspberrypi.local
```

## 5- SSH into the Pi
```
ssh pi@raspberrypi.local
```

## 6- Update the system
```
sudo apt update && sudo apt full-upgrade -y
sudo reboot
```

## 7- Install and configure xrdp
```
sudo apt install xrdp -y
sudo raspi-config        # settings menu
# 3 → Display Options → D1 → select X11 (disable Wayland)
sudo systemctl enable xrdp
sudo systemctl restart xrdp
```

Run sudo raspi-config again → 5 Performance Options → P3 VNC → set to DISABLED (VNC conflicts with xrdp).

## 8- Connect from Windows with MSTSC

Win + R → mstsc

Computer: enter the Pi’s IP address.

Password: the password you set on the Pi.


That’s it — you should now have a Remote Desktop session into your Raspberry Pi.





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

## 5- Pi’ye SSH ile Bağlanın
```
ssh pi@raspberrypi.local
```

## 6- Sistemi Güncelleyin
```
sudo apt update && sudo apt full-upgrade -y
sudo reboot
```

## 7- XRDP’yi Kurun ve Yapılandırın
```
sudo apt install xrdp -y
sudo raspi-config        # settings menu
# 3 → Display Options → D1 → select X11 (disable Wayland)
sudo systemctl enable xrdp
sudo systemctl restart xrdp
```

Ardından sudo raspi-config tekrar → 5 Performance Options → P3 VNC → DISABLED (VNC, xrdp ile çakışır) yapın.

## 8- Windows’tan MSTSC ile Bağlanın

Win + R → mstsc yazın.

Computer: Pi’nin IP adresini girin.

Şifre: Pi’de belirlediğiniz kullanıcı şifresi.


Hepsi bu kadar — artık Raspberry Pi’nize Uzak Masaüstü (Remote Desktop) oturumu ile bağlanabilirsiniz.









