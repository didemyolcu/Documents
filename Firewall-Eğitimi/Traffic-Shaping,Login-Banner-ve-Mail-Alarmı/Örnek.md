# FortiGate Traffic Shaping, Login Banner ve Interface Down Mail Alarmı

Bu doküman aşağıdaki işlemleri içerir:

1. Personel internet hızını 20 Mbps ile sınırlandırma
2. Firewall giriş ekranına uyarı mesajı ekleme
3. Interface down olduğunda mail gönderme
4. Zabbix sunucusunu SNMPv3 ile ekleme

---

# Senaryo

## Gereksinimler

- Personel internet hızı maksimum 20 Mbps olacak.
- Firewall giriş ekranında uyarı yazısı çıkacak.
- Interface down olduğunda `berk.sirin@cozumtek.com` adresine mail gidecek.
- `10.10.100.50` IP’li Zabbix sunucusu SNMPv3 ile bağlanacak.

---

# 1. Internet Hızını 20 Mbps ile Sınırlandırma

# Traffic Shaper Oluşturma

## Menü

```text
Policy & Objects → Traffic Shapers → Create New
```

## Ayarlar

| Ayar | Değer |
|---|---|
| Name | `personel_20mbps` |
| Type | Shared |
| Traffic Priority | Medium |
| Bandwidth Unit | Mbps |
| Maximum Bandwidth | 20 |
| Guaranteed Bandwidth | Disabled |

---

## Açıklama

- Shared type seçildiğinde aynı subnetteki kullanıcılar ortak havuzu kullanır.
- Maximum bandwidth değeri kullanıcıların çıkabileceği maksimum internet hızıdır.
- Guaranteed bandwidth kapalı olduğunda minimum hız garantisi verilmez.

---

# Traffic Shaping Policy Oluşturma

## Menü

```text
Policy & Objects → Traffic Shaping Policy
```

## Ayarlar

| Ayar | Değer |
|---|---|
| Name | `personel-20` |
| Source | `personel-subnet` |
| Destination | all |
| Service | all |
| Action | Apply Shaper |
| Outgoing Interface | `internet-zone` |
| Shared Shaper | `personel_20mbps` |

---

## Reverse Shaper

Reverse shaper internetten içeri gelen trafiği (download) sınırlar.

Shared shaper ise dışarı çıkan trafiği (upload) sınırlar.

---

# 2. Firewall Login Banner Ekleme

## GUI Yöntemi

### Menü

```text
System → Replacement Messages → Extended View
```

## Ayar

| Alan | Değer |
|---|---|
| Post-login Disclaimer Message | "Hoş Geldiniz" |

Kaydedilir.

---

# CLI ile Login Banner Açma

```bash
config system global
    set post-login-banner enable
end
```

---

# 3. Interface Down Mail Alarmı

# Mail Ayarları

## Menü

```text
System → Settings
```

## Ayarlar

| Ayar | Değer |
|---|---|
| Email Service | ON |
| SMTP Server | smtp.gmail.com |
| Port | 25 |
| Username | cozumtek_fortigate |
| Password | xxxxx |
| Security Mode | SMTPS |
| Default Reply To | fortigate@cozumtek.com |

---

# Automation Stitch Oluşturma

## Menü

```text
Security Fabric → Automation → Create New
```

## Ayarlar

| Ayar | Değer |
|---|---|
| Name | `interface-down-uyari` |
| Trigger | FortiOS Event Log |
| Event | Interface status changed |
| Action | Email |
| Minimum Interval | 300 |

---

## Mail Ayarları

| Alan | Değer |
|---|---|# FortiGate Traffic Shaping, Login Banner ve Interface Down Mail Alarmı

Bu doküman aşağıdaki işlemleri içerir:

1. Personel internet hızını 20 Mbps ile sınırlandırma
2. Firewall giriş ekranına uyarı mesajı ekleme
3. Interface down olduğunda mail gönderme

---

# 1. Internet Hızını 20 Mbps ile Sınırlandırma

# Traffic Shaper Oluşturma

## Menü

```text
Policy & Objects → Traffic Shapers → Create New
```

## Ayarlar

| Ayar | Değer |
|---|---|
| Name | `personel_20mbps` |
| Type | Shared |
| Traffic Priority | Medium |
| Bandwidth Unit | Mbps |
| Maximum Bandwidth | 20 |
| Guaranteed Bandwidth | Disabled |

---

## Açıklama

- Shared type seçildiğinde aynı subnetteki kullanıcılar ortak havuzu kullanır.
- Maximum bandwidth değeri kullanıcıların çıkabileceği maksimum internet hızıdır.
- Guaranteed bandwidth kapalı olduğunda minimum hız garantisi verilmez.

---

# Traffic Shaping Policy Oluşturma

## Menü

```text
Policy & Objects → Traffic Shaping Policy
```

## Ayarlar

| Ayar | Değer |
|---|---|
| Name | `personel-20` |
| Source | `personel-subnet` |
| Destination | all |
| Service | all |
| Action | Apply Shaper |
| Outgoing Interface | `internet-zone` |
| Shared Shaper | `personel_20mbps` |

---

## Reverse Shaper

Reverse shaper internetten içeri gelen trafiği (download) sınırlar.

Shared shaper ise dışarı çıkan trafiği (upload) sınırlar.

---

# 2. Firewall Login Banner Ekleme

## GUI Yöntemi

### Menü

```text
System → Replacement Messages → Extended View
```

## Ayar

| Alan | Değer |
|---|---|
| Post-login Disclaimer Message | "Hoş Geldiniz" |

Kaydedilir.

---

# CLI ile Login Banner Açma

```bash
config system global
    set post-login-banner enable
end
```

---

# 3. Interface Down Mail Alarmı

# Mail Ayarları

## Menü

```text
System → Settings
```

## Ayarlar

| Ayar | Değer |
|---|---|
| Email Service | ON |
| SMTP Server | smtp.gmail.com |
| Port | 25 |
| Username | cozumtek_fortigate |
| Password | xxxxx |
| Security Mode | SMTPS |
| Default Reply To | fortigate@cozumtek.com |

---

# Automation Stitch Oluşturma

## Menü

```text
Security Fabric → Automation → Create New
```

## Ayarlar

| Ayar | Değer |
|---|---|
| Name | `interface-down-uyari` |
| Trigger | FortiOS Event Log |
| Event | Interface status changed |
| Action | Email |
| Minimum Interval | 300 |

---

## Mail Ayarları

| Alan | Değer |
|---|---|
| To | berk.sirin@cozumtek.com |
| Subject | Interface Down Uyarısı |
| Body | Interface %{log.srcintf}% DOWN oldu. Zaman: %{log.date}% %{log.time}% |
| To | berk.sirin@cozumtek.com |
| Subject | Interface Down Uyarısı |
| Body | Interface %{log.srcintf}% DOWN oldu. Zaman: %{log.date}% %{log.time}% |

---

# 4. Zabbix SNMPv3 Yapılandırması

## Amaç

`10.10.100.50` IP’li Zabbix sunucusunun firewall cihazını SNMPv3 ile izlemesi.

---

# GUI Üzerinden Yapılandırma

## Menü

```text
System → SNMP
```

## Oluşturma

```text
SNMPv3 → Create New
```

---

## Ayarlar

| Ayar | Değer |
|---|---|
| Username | zabbix |
| Authentication | Enabled |
| Authentication Algorithm | SHA256 |
| Authentication Password | xxxxx |
| Encryption Algorithm | AES |
| Encryption Password | xxxxx |

---

## Hosts

| Ayar | Değer |
|---|---|
| IP Address | 10.10.100.50 |
| Port | 161 |

---

# CLI Yapılandırması

```bash
config system snmp user
    edit zabbix
        set source-ip 10.10.100.1
    next
end
```

---

## Açıklama

`source-ip` firewall cihazının SNMP trafiğini hangi IP üzerinden göndereceğini belirler.

Bu örnekte:

```text
10.10.100.1
```

firewall’ın LAN IP adresidir.
