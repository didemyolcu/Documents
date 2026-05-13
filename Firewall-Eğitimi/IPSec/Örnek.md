# IPSec Site-to-Site VPN Kurulumu

Bu doküman, iki farklı lokasyon arasında IPSec Site-to-Site VPN bağlantısının kurulumu için temel adımları içerir.

---

# 1. VPN Tüneli Oluşturma

## Genel Ayarlar

| Ayar | Değer |
|---|---|
| Name | `deneme_vpn` |
| Remote Gateway | Static IP Address |
| IP Address | `86.123.32.12` *(Karşı tarafın WAN IP adresi)* |
| Interface | `port1` *(İnternete çıkılan arayüz)* |

---

## Authentication Ayarları

| Ayar | Değer |
|---|---|
| Method | Pre-Shared Key |
| Pre-Shared Key | `xxxxx` |
| IKE Version | `1` |

> **Not:**  
> Pre-Shared Key değeri iki tarafta da birebir aynı olmalıdır.

---

## Phase 1 Proposal

| Ayar | Değer |
|---|---|
| Encryption | `AES128` |
| Authentication | `SHA256` |
| Key Lifetime | `28800` |

---

## Phase 2 Selectors

| Ayar | Değer |
|---|---|
| Name | `vpn-deneme-ph2` |
| Local Address | `192.168.20.0/24` *(Yerel ağ)* |
| Remote Address | `192.168.12.0/24` *(Karşı taraf ağı)* |
| Encryption | `AES128` |
| Authentication | `SHA256` |
| PFS (Perfect Forward Secrecy) | `Disabled` |
| Auto-negotiate | `Enabled` |

---

## Auto-negotiate Açıklaması

### Enabled (Açık)
VPN tüneli sürekli aktif durumda kalır ve trafik beklemeden ayağa kalkar.

### Disabled (Kapalı)
VPN yalnızca trafik geldiğinde açılır.  
İlk bağlantıda kısa süreli ping kaybı yaşanabilir.

> **Öneri:**  
> Site-to-site bağlantılarda ve sürekli trafik bulunan ortamlarda `Enabled` kullanılması tavsiye edilir.

---

# 2. Firewall Policy (Kural) Oluşturma

## VPN → LAN Kuralı

| Ayar | Değer |
|---|---|
| Name | `vpn-port1` |
| Incoming Interface | `deneme-vpn` |
| Outgoing Interface | `port1-vlan10` |
| Source | `all` |
| Destination | `all` |
| Service | `all` |
| Action | `Accept` |
| NAT | `Disabled` |

> **Önemli:**  
> Bu kuralın tam tersi yön için de oluşturulması gerekir.  
> Yani hem gidiş hem dönüş trafiğine izin verilmelidir.

---

# 3. Static Route Oluşturma

| Ayar | Değer |
|---|---|
| Destination | `192.168.12.0/24` |
| Interface | `vpn-deneme` |

Bu işlem sayesinde karşı ağın trafiği VPN tüneline yönlendirilir.

---

# Dikkat Edilmesi Gerekenler

- Tüm ayarlar karşı tarafta da aynı şekilde yapılandırılmalıdır.
- Encryption, Authentication ve Phase ayarları birebir eşleşmelidir.
- Yanlış yapılandırma karşı tarafın bağlantısını kesebilir.
- Değişiklik yapmadan önce mevcut yapılandırmanın yedeğinin alınması önerilir.
