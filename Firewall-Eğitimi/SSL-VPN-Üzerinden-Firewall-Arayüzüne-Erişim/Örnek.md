
# FortiGate SSL-VPN Üzerinden Firewall GUI Erişimi

## Görev

- Firewall arayüzüne sadece SSL-VPN yapan IT grubu erişebilsin.
- Administrator kullanıcısında trusted host kullanılsın.

---

# 1. Administrator Trusted Host Ayarı

## Menü

```text
System → Administrators
```

---

# Admin Kullanıcısını Düzenle

```text
admin → Edit
```

---

# Trusted Host Aç

| Alan | Değer |
|---|---|
| Restrict login to trusted hosts | Enable |

---

# Trusted Hostlar

| Alan | Değer |
|---|---|
| Trusted Host 1 | `172.16.12.0/28` |
| Trusted Host 2 | `192.168.0.0/24` |

---

# Açıklama

| Subnet | Amaç |
|---|---|
| `172.16.12.0/28` | IT VPN subneti |
| `192.168.0.0/24` | Local erişimin kopmaması |

---

# 2. Firewall Policy Oluştur

## Menü

```text
Policy & Objects → IPv4 Policy
```

---

# Policy Ayarları

| Alan | Değer |
|---|---|
| Name | `IT_to_FWGUI` |
| Incoming Interface | `ssl.root` |
| Outgoing Interface | `server-zone` |
| Source | `IT_VPN` + `IT_VPN_grb` |
| Destination | `10.10.100.1` |
| Action | `Accept` |

---

# Service Ayarları

| Service | Açıklama |
|---|---|
| PING | Firewall’a ping atabilsin |
| TCP/10443 | HTTPS GUI erişimi |

---

# Açıklama

Firewall GUI:

```text
HTTPS/10443
```

üzerinden çalıştığı için policy’de:

```text
TCP/10443
```

servisi açılır.

---

# Sonuç

Bu yapı sayesinde:

- Sadece IT VPN kullanıcıları firewall GUI’ye erişebilir.
- Administrator hesabı trusted host ile korunur.
- Firewall yönetim paneli internete açık olmaz.
