
# FortiGate SNMPv3 Zabbix Entegrasyonu

Bu doküman, FortiGate cihazının Zabbix sunucusuna SNMPv3 ile eklenmesini anlatır.

---

# Senaryo

## Gereksinim

`10.10.100.50` IP adresine sahip Zabbix sunucusu, FortiGate cihazını SNMPv3 ile izlemek istiyor.

Zabbix tarafında cihazı ekleyebilmek için gerekli parametrelerin paylaşılması gerekiyor.

---

# Amaç

- Firewall’ın güvenli şekilde izlenmesi
- SNMPv3 ile şifreli haberleşme sağlanması
- Zabbix’in CPU, RAM, interface ve trafik bilgilerini çekebilmesi

---

# SNMPv3 Kullanıcısı Oluşturma

## Menü

```text
System → SNMP
```

---

# SNMPv3 User Oluşturma

```text
SNMPv3 → Create New
```

---

# Kullanıcı Ayarları

| Ayar | Değer |
|---|---|
| Username | `zabbix` |
| Authentication | Enabled |
| Authentication Algorithm | `SHA256` |
| Authentication Password | `xxxxx` |
| Encryption Algorithm | `AES` |
| Encryption Password | `xxxxx` |

---

# Host Yetkisi

## Hosts

| Ayar | Değer |
|---|---|
| IP Address | `10.10.100.50` |
| Port | `161` |

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

# Source-IP Açıklaması

| Ayar | Değer |
|---|---|
| source-ip | `10.10.100.1` |

Bu IP:

- Firewall’ın LAN IP adresidir.
- SNMP paketlerinin hangi IP’den çıkacağını belirler.

---

# Zabbix Tarafında Kullanılacak Bilgiler

| Parametre | Değer |
|---|---|
| SNMP Version | v3 |
| Security Name | zabbix |
| Authentication Protocol | SHA256 |
| Authentication Password | xxxxx |
| Privacy Protocol | AES |
| Privacy Password | xxxxx |
| Port | 161 |

---

# Trafik Akışı

```text
Zabbix Server
      ↓
SNMPv3 Request
      ↓
FortiGate
      ↓
Şifreli SNMP Response
      ↓
Zabbix
```

---

# Dikkat Edilmesi Gerekenler

- SNMPv2 yerine SNMPv3 kullanılmalıdır.
- MD5 yerine SHA256 tercih edilmelidir.
- DES yerine AES tercih edilmelidir.
- SNMP erişimi yalnızca Zabbix IP’sine verilmelidir.
- Source-IP doğru subnet üzerinden seçilmelidir.
