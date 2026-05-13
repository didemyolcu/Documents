
# FortiGate İlk Kurulum ve Temel Yapılandırma

Bu doküman FortiGate cihazı ilk açıldığında yapılması gereken temel işlemleri içerir.

İçerik:

1. Firewall sıfırlama
2. Console bağlantısı
3. Management erişimi
4. İlk IP yapılandırması
5. Arayüz erişimi
6. Temel sistem ayarları
7. Yönetim portlarının değiştirilmesi
8. VLAN / Software Switch oluşturma

---

# 1. Firewall Sıfırlama

## Console Kablosunu Bağla

Firewall’ın:

```text
Console Port
```

girişine console kablosu bağlanır.

Diğer uç:

```text
Laptop / USB
```

cihazına takılır.

---

# Ubuntu Üzerinde Screen Kurulumu

```bash
sudo apt install screen
```

---

# Console Bağlantısı Aç

```bash
sudo screen /dev/ttyUSB0 9600
```

---

# Parametreler

| Alan | Açıklama |
|---|---|
| /dev/ttyUSB0 | USB-to-Serial cihazı |
| 9600 | Baud rate |

---

# Portu Bulmak

USB portu bilinmiyorsa:

```bash
dmesg | grep tty
```

komutu kullanılır.

---

# Factory Reset

Firewall’a giriş yaptıktan sonra:

```bash
execute factoryreset
```

komutu ile cihaz sıfırlanır.

---

# 2. Firewall’a İlk Erişim

# Fiziksel Bağlantı

```text
Firewall mgmt port → Laptop
```

şeklinde bağlanılır.

---

# Laptopa Statik IP Ver

## Ubuntu

```text
Ayarlar → Ağ → Kablolu Ayarlar
```

---

# IPv4 Ayarı

| Alan | Değer |
|---|---|
| Address | 192.168.1.10 |
| Netmask | 255.255.255.0 |
| Gateway | 192.168.1.99 |

---

# 3. FortiGate Management IP Ayarı

## Menü

```text
Network → Interfaces → mgmt
```

---

# Interface Ayarı

| Alan | Değer |
|---|---|
| Addressing Mode | Manual |
| IP/Netmask | 192.168.0.129/24 |

---

# Administrative Access

Açılması gereken servisler:

| Servis | Açıklama |
|---|---|
| HTTPS | Web GUI erişimi |
| SSH | CLI erişimi |
| PING | Ping testi |

---

# DHCP

```text
DHCP → Disabled
```

olmalıdır.

---

# Web Arayüzüne Erişim

Tarayıcıdan:

```text
https://192.168.0.129
```

adresine gidilir.

---

# 4. Temel Sistem Ayarları

## Menü

```text
System → Settings
```

---

# Hostname

| Alan | Değer |
|---|---|
| Hostname | Didem-FW |

---

# Timezone

| Alan | Değer |
|---|---|
| Timezone | GMT +3 Istanbul |

---

# NTP

```text
Enable NTP
```

açılır.

---

# NTP Nedir?

Firewall’ın saat senkronizasyonunu sağlar.

---

# FortiGuard

```text
FortiGuard
```

Fortinet’in:

- IPS
- AV
- URL Filtering
- Reputation

servislerini sağlar.

---

# 5. Yönetim Portlarını Değiştirme

Varsayılan portlar değiştirilerek güvenlik artırılabilir.

---

# Port Ayarları

| Servis | Port |
|---|---|
| HTTP | 8080 |
| HTTPS | 10443 |
| SSH | 2222 |
| Telnet | 2323 |

---

# Yeni GUI Erişimi

```text
https://192.168.0.129:10443
```

---

# 6. Software Switch Oluşturma

## Menü

```text
Network → Interfaces → Create New → Interface
```

---

# Ayarlar

| Alan | Değer |
|---|---|
| Name | internal-po |
| Type | Software Switch |

---

# Interface Members

Switch içine eklenecek portlar seçilir.

Örnek:

```text
port1
```

---

# Create Address Object Matching

```text
Disabled
```

olmalıdır.

---

# Software Switch Mantığı

Birden fazla fiziksel portu:

```text
Tek LAN gibi çalıştırır.
```

---

# 7. VLAN Oluşturma

## Menü

```text
Network → Interfaces → Create New → Interface
```

---

# VLAN Ayarları

| Alan | Açıklama |
|---|---|
| Name | VLAN adı |
| Type | VLAN |
| Interface | Parent interface |
| VLAN ID | VLAN numarası |
| IP/Netmask | VLAN gateway IP’si |

---

# Örnek

| Alan | Değer |
|---|---|
| Name | personel |
| VLAN ID | 50 |

---

# VLAN Mantığı

VLAN:

```text
Aynı switch üzerinde farklı ağlar oluşturur.
```

---

# İlk Kurulum Sonrası Kontroller

- GUI erişimi çalışıyor mu?
- SSH erişimi çalışıyor mu?
- Ping çalışıyor mu?
- Saat doğru mu?
- Port değişiklikleri çalışıyor mu?
- Interface IP’leri doğru mu?
- DHCP kapalı mı?
- Software switch doğru oluştu mu?

---

# Dikkat Edilecekler

- Management IP çakışmamalı
- HTTPS açık olmalı
- Gereksiz servisler kapatılmalı
- Varsayılan portlar değiştirilmeli
- NTP mutlaka açılmalı
- Factory reset sonrası admin şifresi değiştirilmeli
