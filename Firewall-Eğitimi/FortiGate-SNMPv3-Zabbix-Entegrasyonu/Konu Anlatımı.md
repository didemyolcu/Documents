
# FortiGate Üzerinde SNMPv3 Yapılandırması

Bu dokümanda FortiGate cihazının Zabbix gibi monitoring sistemlerine SNMPv3 ile nasıl açıldığı anlatılmaktadır.

Amaç:

- Firewall’ın monitoring sistemine güvenli şekilde eklenmesi
- SNMP trafiğinin şifrelenmesi
- Sadece belirli IP’lerin erişebilmesi

---

# 1. SNMP Menüsüne Gir

## Menü

```text
System → SNMP
```

Burada firewall’ın monitoring ayarları yapılır.

---

# 2. SNMPv3 User Oluştur

## Menü

```text
SNMPv3 → Create New
```

Firewall’a bağlanacak monitoring sistemi için kullanıcı oluşturulur.

---

# 3. Username Belirle

| Alan | Açıklama |
|---|---|
| Username | Monitoring sisteminin bağlanırken kullanacağı kullanıcı adı |

Örnek:

```text
zabbix
```

---

# 4. Authentication Aç

| Alan | Değer |
|---|---|
| Authentication | Enable |

Bu ayar:

```text
Monitoring sistemi gerçekten yetkili mi?
```

kontrolünü sağlar.

---

# 5. Authentication Algorithm Seç

| Algoritma | Açıklama |
|---|---|
| MD5 | Eski |
| SHA1 | Orta |
| SHA256 | Önerilen |

Genellikle:

```text
SHA256
```

kullanılır.

---

# 6. Authentication Password Gir

Monitoring sistemi ile firewall arasında kullanılacak doğrulama parolasıdır.

---

# 7. Encryption Aç

| Alan | Açıklama |
|---|---|
| Encryption Algorithm | SNMP trafiğini şifreler |

---

# 8. Encryption Algorithm Seç

| Algoritma | Açıklama |
|---|---|
| DES | Eski |
| AES | Önerilen |

Genellikle:

```text
AES
```

kullanılır.

---

# 9. Encryption Password Gir

SNMP trafiğinin şifrelenmesinde kullanılacak paroladır.

---

# 10. Hosts Kısmını Doldur

Burada:

```text
Kim SNMP isteği gönderebilir?
```

belirlenir.

## Alanlar

| Alan | Açıklama |
|---|---|
| IP Address | Monitoring server IP’si |
| Port | SNMP portu |

---

# Port 161

SNMP’in standart portudur.

| Servis | Port |
|---|---|
| SNMP | 161 |

---

# 11. Source-IP Ayarla

Bazı durumlarda firewall’ın SNMP paketini hangi IP ile göndereceği belirtilmelidir.

## CLI

```bash
config system snmp user
    edit <username>
        set source-ip <firewall-ip>
    next
end
```

---

# Source-IP Ne İşe Yarar?

Firewall’ın cevap paketlerini hangi interface/IP üzerinden göndereceğini belirler.

Özellikle:

- çok interface varsa
- routing karışıksa
- monitoring stabil değilse

kullanılır.

---

# Monitoring Sistemi Tarafında Gereken Bilgiler

Monitoring sistemine şunlar girilir:

| Alan | Açıklama |
|---|---|
| SNMP Version | v3 |
| Username | Firewall’daki username |
| Authentication Protocol | SHA256 |
| Authentication Password | Authentication şifresi |
| Privacy Protocol | AES |
| Privacy Password | Encryption şifresi |
| Port | 161 |

---

# Trafik Akışı

```text
Monitoring Server
      ↓
SNMPv3 Request
      ↓
FortiGate
      ↓
Şifreli Response
      ↓
Monitoring Server
```

---

# Dikkat Edilmesi Gerekenler

- SNMPv2 yerine SNMPv3 kullan
- SHA256 tercih et
- AES tercih et
- Sadece monitoring IP’lerine izin ver
- Güçlü parola kullan
- SNMP’i internete açma
