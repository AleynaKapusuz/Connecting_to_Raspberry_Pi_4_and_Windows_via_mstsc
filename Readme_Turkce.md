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



