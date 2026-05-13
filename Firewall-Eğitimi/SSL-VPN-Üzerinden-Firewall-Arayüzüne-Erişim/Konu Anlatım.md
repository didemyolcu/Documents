# FortiGate SSL-VPN Üzerinden Firewall Arayüzüne Erişim

Bu dokümanda:

- Sadece IT grubunun SSL-VPN üzerinden firewall arayüzüne erişmesi
- Administrator hesabında trusted host kullanılması
- SSL-VPN kullanıcılarına firewall GUI erişimi verilmesi

anlatılmaktadır.

---

# Amaç

- Firewall arayüzünü internete açmamak
- Sadece VPN yapan IT kullanıcılarının erişebilmesi
- Administrator hesabını trusted host ile korumak

---

# 1. Administrator Trusted Host Ayarı

## Menü

```text
System → Administrators
```

---

# Administrator Kullanıcısını Düzenle

```text
admin → Edit
```

---

# Trusted Host Aç

| Alan | Açıklama |
|---|---|
| Restrict login to trusted hosts | Enable |

---

# Trusted Host Ekle

## IT VPN Subneti

| Alan | Değer |
|---|---|
| Trusted Host 1 | IT VPN subneti |

Bu sayede:

```text
Sadece IT VPN subnetinden gelen kullanıcılar
admin hesabına giriş yapabilir.
```

---

# Local Ağ Eklemek

## Neden Gerekli?

Kendi bulunduğun subneti eklemezsen:

```text
Firewall erişimin kesilebilir.
```

---

# Local Subnet

| Alan | Değer |
|---|---|
| Trusted Host 2 | Local yönetim subneti |

---

# 2. Firewall Policy Oluştur

## Menü

```text
Policy & Objects → IPv4 Policy
```

---

# Policy Oluştur

| Alan | Açıklama |
|---|---|
| Name | IT_to_FWGUI |
| Incoming Interface | ssl.root |
| Outgoing Interface | Server/LAN interface |
| Source | IT VPN subneti veya IT VPN group |
| Destination | Firewall interface IP |
| Action | Accept |

---

# Destination Nedir?

Firewall’ın hangi interface IP’sine erişilecekse o IP yazılır.

Örnek:

```text
10.10.100.1
```

---

# Service Ayarı

## HTTPS Servisi

Firewall GUI erişimi HTTPS üzerinden yapılır.

Eğer GUI portu:

```text
10443
```

ise:

```text
TCP/10443
```

servisi açılmalıdır.

---

# Ping Açmak

İstenirse:

```text
PING
```

servisi de eklenebilir.

---

# Service Örneği

| Service |
|---|
| HTTPS |
| TCP/10443 |
| PING |

---

# Action

| Alan | Değer |
|---|---|
| Action | Accept |

---

# Neden SSL-VPN Üzerinden Yönetim Yapılır?

Çünkü:

- Firewall GUI internete açılmaz
- Yönetim trafiği şifrelenir
- Sadece VPN kullanıcıları erişebilir
- Yetkisiz erişim azaltılır

---

# Dikkat Edilecek Noktalar

- Trusted host yanlış girilirse erişim kaybolabilir
- Local subnet mutlaka eklenmeli
- Sadece IT grubuna izin verilmeli
- GUI hangi portta çalışıyorsa o port açılmalı
- Mümkünse sadece HTTPS kullanılmalı
