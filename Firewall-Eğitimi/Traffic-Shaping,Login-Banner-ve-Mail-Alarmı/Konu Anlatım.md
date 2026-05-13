
# FortiGate Traffic Shaping, Login Banner ve Mail Alarmı Yapılandırmaları

Bu doküman FortiGate üzerinde:

- Internet hız limitleme
- Login banner ekleme
- Interface down mail alarmı oluşturma

işlemlerinin temel yapılandırma adımlarını içerir.

---

# 1. Traffic Shaping (Internet Hız Limitleme)

## Traffic Shaper Oluştur

### Menü

```text
Policy & Objects → Traffic Shapers → Create New
```

### Ayarlar

| Ayar | Açıklama |
|---|---|
| Name | Shaper adı |
| Type | Shared / Per-IP |
| Traffic Priority | Trafik önceliği |
| Bandwidth Unit | Mbps |
| Maximum Bandwidth | Maksimum hız limiti |
| Guaranteed Bandwidth | Minimum hız garantisi |

---

## Traffic Shaping Policy Oluştur

### Menü

```text
Policy & Objects → Traffic Shaping Policy
```

### Ayarlar

| Ayar | Açıklama |
|---|---|
| Source | Limitleme uygulanacak kullanıcı/subnet |
| Destination | Hedef |
| Service | Servis |
| Action | Apply Shaper |
| Outgoing Interface | İnternet interface’i |
| Shared Shaper | Kullanılacak shaper |
| Reverse Shaper | Download limiti |

---

# 2. Login Banner Ekleme

## GUI

### Menü

```text
System → Replacement Messages → Extended View
```

### Alan

```text
Post-login Disclaimer Message
```

İstenilen mesaj yazılır ve kaydedilir.

---

## CLI

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

### Yapılandırılacak Alanlar

| Ayar | Açıklama |
|---|---|
| SMTP Server | Mail sunucusu |
| Port | SMTP portu |
| Username | Mail hesabı |
| Password | Mail şifresi |
| Security Mode | SSL/TLS |
| Reply To | Gönderici adresi |

---

# Automation Oluşturma

## Menü

```text
Security Fabric → Automation → Create New
```

### Trigger

| Ayar | Değer |
|---|---|
| Trigger Type | FortiOS Event Log |
| Event | Interface status changed |

---

### Action

| Ayar | Açıklama |
|---|---|
| Action Type | Email |
| To | Mail adresi |
| Subject | Mail başlığı |
| Body | Mail içeriği |

---

# Notlar

- Shared Shaper ortak bandwidth kullanır.
- Per-IP her kullanıcıya ayrı limit verir.
- Reverse shaper download trafiğini sınırlar.
- Automation ile olay bazlı işlem yapılabilir.
- Login banner güvenlik ve yasal uyarı amacıyla kullanılır.
