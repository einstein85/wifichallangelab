# WiFiChallengeLab Cheat Sheet

This repository provides a concise cheat sheet for **WiFiChallengeLab**, created to serve as a quick-reference guide during lab practice.

## Purpose
- Summarize essential commands and attack workflows  
- Provide quick access to commonly used tools and techniques  
- Offer practical notes gathered during hands-on exercises  
- Help streamline your workflow while solving WiFiChallengeLab challenges  

## Contents
- Common WiFi attack commands  
- Troubleshooting steps  
- Useful shortcuts and workflow tips  
- Additional notes for efficient lab usage  

## Notes
This cheat sheet is intended for educational and lab-use purposes only.  
Please ensure that all activities are performed in controlled, authorized environments.

---

If you would like a more detailed version with sample commands or attack flows included, I can extend this README.

## 💡 HIZLI İPUÇLARI

### MAC Adresi Bulma
```bash
# Kendi MAC'ini öğren
macchanger --show wlan0mon
# veya
ip link show wlan0mon
# veya
ifconfig wlan0mon
```

### Kanal Değiştirme
```bash
iwconfig wlan0mon channel [CHANNEL]
```

### Monitor Mod Sorunları
```bash
# Eğer monitor mod başlatamıyorsan:
airmon-ng check kill
ifconfig wlan0 down
iwconfig wlan0 mode monitor
ifconfig wlan0 up
```

### Handshake Kontrol
```bash
# Capture dosyasında handshake var mı?
aircrack-ng wpa_capture-01.cap
# "1 handshake" yazdığını göreceksin
```

### Parola Listesi Oluşturma
```bash
# 8 karakterlik sayısal parolalar
crunch 8 8 0123456789 -o numbers.txt

# Kelime + 2 rakam
john --wordlist=words.txt --rules --stdout > mutated.txt
```

### Deauth Troubleshooting
```bash
# Deauth çalışmıyorsa channel doğru mu kontrol et:
iwconfig wlan0mon
# Channel'ı hedef ağla aynı yap:
iwconfig wlan0mon channel [TARGET_CHANNEL]
```

---

## 🚨  KRİTİK NOTLAR

### Zaman Yönetimi
- ⏰ Her senaryo için **MAX 60 dakika** ayır
- ⏰ İlk 10 dakika: Keşif ve bilgi toplama
- ⏰ 30-40 dakika: Saldırı gerçekleştirme
- ⏰ Son 10 dakika: Bağlanma ve proof alma

### Sık Yapılan Hatalar
❌ Monitor mod açıkken bağlanmaya çalışmak
❌ Channel'ı yanlış ayarlamak
❌ Hex key'de iki nokta işaretlerini kullanmak
❌ BSSID ve Client MAC'i karıştırmak
❌ wpa_supplicant çalışırken dhclient yapmayı unutmak

### Mutlaka Kontrol Et
✅ Handshake yakalandı mı? (airodump'ta sağ üstte)
✅ Data paketleri artıyor mu? (#Data sütunu)
✅ Monitor mod kapalı mı? (bağlanmadan önce)
✅ Channel doğru mu?
✅ Config dosyası söz dizimi doğru mu?

### Alternatif Komutlar
```bash
# wpa_supplicant başka yöntem:
wpa_supplicant -B -D nl80211 -i wlan0 -c config.conf

# p alma alternatif:
lynx -dump http://192.168.1.1/
```

---

## 📋 PARAMETRE REFERANSI

### airodump-ng
- `--band abg` → 2.4 + 5 GHz
- `-c [CH]` → Kanal filtresi
- `--bssid [MAC]` → BSSID filtresi
- `-w [FILE]` → Dosyaya kaydet
- `--wps` → WPS bilgisi göster

### aireplay-ng
- `-0` → Deauth attack
- `-1` → Fake authentication
- `-3` → ARP replay attack
- `-a [MAC]` → Access Point MAC
- `-c [MAC]` → Client MAC
- `-h [MAC]` → Source MAC (kendi MAC'in)

### aircrack-ng
- `-w [WORDLIST]` → Parola listesi
- `-e [ESSID]` → SSID filtresi
- `-b [BSSID]` → BSSID filtresi

### wpa_supplicant
- `-D nl80211` → Driver
- `-i [INTERFACE]` → Interface
- `-c [CONFIG]` → Config dosyası
- `-B` → Background'da çalıştır

---

## 🎓 BAŞARI İÇİN SON TAVSİYELER

1. **Pratik Yap**: Her senaryoyu 3-5 kez tekrarla
2. **Hız Kazan**: Komutları ezberle, kopyala-yapıştır kullan
3. **Sakin Kal**: Bir şey çalışmazsa alternatif yöntem dene
4. **Logları Oku**: Hata mesajlarını oku ve anla
5. **Zamanı Koru**: 20 dakika sonuç alamadıysan başka senaryoya geç, sonra dön


## References
Content on this page was developed with the help of material from:

- https://www.emmanuelsolis.com/oswp.html
- https://github.com/koutto/pi-pwnbox-rogueap/wiki
- https://github.com/s0lst1c3/eaphammer/wiki
- https://www.aircrack-ng.org/doku.php
- https://www.cellstream.com/reference-reading/tipsandtricks/410-3-ways-to-put-your-wi-fi-interface-in-monitor-mode-in-linux
- https://wiki.netbsd.org/tutorials/how_to_use_wpa_supplicant/
- https://w1.fi/cgit/hostap/plain/hostapd/hostapd.conf
- https://wiki.innovaphone.com/index.php?title=Howto:802.1X_EAP-TLS_With_FreeRadius



