
# FortiGate IPSec Site-to-Site VPN Yapılandırması

---

# 1. IPSec VPN Oluştur

## Menü

```text
VPN → IPSec Tunnels → Create New
```

---

# Genel Ayarlar

| Alan | Açıklama |
|---|---|
| Name | VPN adı |
| Remote Gateway | Karşı firewall WAN IP’si |
| Interface | İnternete çıkan interface |

---

# Authentication

| Alan | Açıklama |
|---|---|
| Method | Pre-Shared Key |
| Pre-Shared Key | İki tarafta aynı olmalı |
| IKE Version | Karşı taraf ile aynı olmalı |

---

# Phase 1

| Alan | Açıklama |
|---|---|
| Encryption | AES128 / AES256 |
| Authentication | SHA256 |
| Key Lifetime | Anahtar süresi |

---

# Phase 2

| Alan | Açıklama |
|---|---|
| Local Address | Kendi subnet’in |
| Remote Address | Karşı subnet |
| Encryption | AES128 |
| Authentication | SHA256 |
| PFS | İki tarafta aynı olmalı |
| Auto-negotiate | VPN sürekli açık kalsın istiyorsan enable |

---

# 2. Firewall Policy Oluştur

## Menü

```text
Policy & Objects → IPv4 Policy
```

---

# VPN → LAN Policy

| Alan | Açıklama |
|---|---|
| Incoming Interface | VPN interface |
| Outgoing Interface | LAN interface |
| Source | Kaynak ağ |
| Destination | Hedef ağ |
| Service | Açılacak servis |
| Action | Accept |
| NAT | Disable |

---

# LAN → VPN Policy

Aynı policy’nin ters yönü de oluşturulur.

---

# 3. Static Route Oluştur

## Menü

```text
Network → Static Routes → Create New
```

---

# Route

| Alan | Açıklama |
|---|---|
| Destination | Karşı subnet |
| Interface | VPN interface |

---

# Kontrol

## VPN Status

```text
VPN → IPSec Monitor
```

Buradan:

- tunnel up/down
- phase1
- phase2

kontrol edilir.

---

# Dikkat

- İki taraftaki phase ayarları aynı olmalı
- PSK birebir aynı olmalı
- NAT kapalı olmalı
- Çift yönlü policy gerekli
- Route olmadan trafik geçmez
