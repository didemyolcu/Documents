# FortiGate SSL-VPN Yapılandırması

Bu doküman, FortiGate üzerinde departman bazlı SSL-VPN erişimi yapılandırmasını içerir.

---

# Senaryo

## WAN Bilgileri

| Ayar | Değer |
|---|---|
| WAN Interface | `wan1` |
| WAN IP | `76.76.76.76/29` |
| Gateway | `76.76.76.75` |

---

## LAN / Server VLAN

| Ayar | Değer |
|---|---|
| Network | `10.10.100.0/24` |
| Gateway | `10.10.100.1` |

---

## Sunucular

| Sunucu | IP |
|---|---|
| AD Server | `10.10.100.100` |
| Logo Server | `10.10.100.101` |
| File Server | `10.10.100.102` |
| ITSM Server | `10.10.100.103` |

---

# İstenen Yapı

- SSL-VPN erişimi sadece Türkiye’den açık olacak.
- Departman bazlı yetkilendirme yapılacak.
- Her grup sadece izin verilen sunuculara erişebilecek.
- Outsource kullanıcıları iç ağa erişemeyecek.
- Outsource kullanıcıları internete firewall üzerinden çıkacak.
- VPN kullanıcıları DNS olarak AD sunucusunu kullanacak.

---

# Yetki Matrisi

| Grup | Erişebileceği Kaynaklar |
|---|---|
| IK | AD + File Server |
| Muhasebe | AD + Logo |
| IT | Tüm Sunucular |
| Yönetim | AD + File Server + ITSM |
| Outsource | Sadece İnternet |

---

# VPN IP Havuzları

| Grup | VPN Pool |
|---|---|
| IK | `172.16.10.0/28` |
| Muhasebe | `172.16.11.0/28` |
| IT | `172.16.12.0/28` |
| Yönetim | `172.16.13.0/28` |

---

# 1. WAN Ayarı

## Menü

```text
Network → Interfaces → wan1
```

## Yapılandırma

| Ayar | Değer |
|---|---|
| Mode | Manual |
| IP | `76.76.76.76/29` |

### Neden Yapılır?
Firewall’ın internete çıkabilmesi için WAN arayüzüne gerçek IP atanır.

---

# 2. Default Route Oluşturma

## Menü

```text
Network → Static Routes → Create New
```

## Yapılandırma

| Ayar | Değer |
|---|---|
| Destination | `0.0.0.0/0` |
| Gateway | `76.76.76.75` |
| Interface | `wan1` |

### Neden Yapılır?
Firewall hangi trafiği hangi gateway üzerinden internete göndereceğini öğrenir.

---

# 3. Zone Oluşturma

## Menü

```text
Network → Interfaces → Zones
```

---

## Internet Zone

| Ayar | Değer |
|---|---|
| Name | `internet-zone` |
| Members | `wan1` |

---

## Server Zone

| Ayar | Değer |
|---|---|
| Name | `server-zone` |
| Members | `server-vlan` |

---

## Server VLAN

| Ayar | Değer |
|---|---|
| Name | `server` |
| Interface | `port1` |
| IP/Netmask | `10.10.100.1/24` |
| Ping | Enabled |

### Neden Yapılır?
Zone yapısı policy yönetimini kolaylaştırır ve karışıklığı azaltır.

---

# 4. Address Object Oluşturma

## Menü

```text
Policy & Objects → Addresses
```

---

## AD Server

| Ayar | Değer |
|---|---|
| Name | `AD-10.10.100.100` |
| IP/Netmask | `10.10.100.100/32` |

---

## Diğer Sunucular

- `LOGO-10.10.100.101`
- `FILE-10.10.100.102`
- `ITSM-10.10.100.103`

### Neden Yapılır?
Policy yazarken IP yerine isim kullanılır. Yönetim daha kolay olur.

---

# 5. User Group Oluşturma

## Menü

```text
User & Device → User Groups → Create New
```

## Gruplar

```text
IK_VPN_grb
IT_VPN_grb
MUHASEBE_VPN_grb
OUTSOURCE_VPN_grb
YONETIM_VPN_grb
```

### Neden Yapılır?
Kullanıcılara yetkiyi tek tek değil grup bazlı vermek için kullanılır.

---

# 6. VPN IP Pool Oluşturma

## Menü

```text
Policy & Objects → Addresses → Create New
```

---

## Örnek

| Ayar | Değer |
|---|---|
| Name | `IK_VPN_pool` |
| Type | Subnet |
| IP/Netmask | `172.16.10.0/28` |

---

## Diğer Havuzlar

| Pool | Ağ |
|---|---|
| MUHASEBE_VPN_pool | `172.16.11.0/28` |
| IT_VPN_pool | `172.16.12.0/28` |
| YONETIM_VPN_pool | `172.16.13.0/28` |
| OUTSOURCE_VPN_pool | Ayrı subnet |

### Neden Yapılır?
VPN’e bağlanan kullanıcılara dağıtılacak IP aralıkları belirlenir.

---

# 7. SSL-VPN Portal Oluşturma

## Menü

```text
VPN → SSL-VPN Portals → Create New
```

---

# IK Portal

| Ayar | Değer |
|---|---|
| Name | `IK_PORTAL` |
| Tunnel Mode | Enabled |
| Split Tunneling | Enabled |
| Routing Address | `AD-10.10.100.100` + `FILE-10.10.100.102` |
| Source IP Pools | `IK_VPN_pool` |

### Neden Yapılır?
IK kullanıcılarının sadece izin verilen sistemlere erişmesi sağlanır.

---

# Muhasebe Portal

| Ayar | Değer |
|---|---|
| Routing Address | `AD + LOGO` |

### Neden Yapılır?
Muhasebe kullanıcıları yalnızca gerekli sistemlere erişir.

---

# IT Portal

| Ayar | Değer |
|---|---|
| Routing Address | Tüm sunucular |

### Neden Yapılır?
IT ekibi tüm sistemleri yönetebilmelidir.

---

# Yönetim Portal

| Ayar | Değer |
|---|---|
| Routing Address | `AD + FILE + ITSM` |

### Neden Yapılır?
Yönetim birden fazla kritik sisteme erişim sağlar.

---

# Outsource Portal

| Ayar | Değer |
|---|---|
| Tunnel Mode | Enabled |
| Split Tunnel | Disabled |
| Source IP Pool | `OUTSOURCE_VPN_pool` |

### Neden Yapılır?
Outsource kullanıcılarının iç ağa erişmesi engellenir. Sadece internet kullanırlar.

---

# 8. SSL-VPN Settings

## Menü

```text
VPN → SSL-VPN Settings
```

---

## Genel Ayarlar

| Ayar | Değer |
|---|---|
| Listen Interface | `internet-zone` |
| Listen Port | `10443` |

### Neden Yapılır?
SSL-VPN’in dışarıdan hangi interface ve port üzerinden dinleyeceği belirlenir.

---

# Türkiye Kısıtlaması

## Host Oluşturma

| Ayar | Değer |
|---|---|
| Name | `Turkiye` |
| Type | Geography |
| Country | Turkey |

### Neden Yapılır?
Yalnızca Türkiye’den gelen bağlantılara izin verilir.

---

# Address Range

```text
Specify custom IP ranges
```

## Kullanılacak Havuzlar

```text
IK_VPN_pool
IT_VPN_pool
MUHASEBE_VPN_pool
OUTSOURCE_VPN_pool
YONETIM_VPN_pool
```

### Neden Yapılır?
VPN kullanıcılarına hangi IP havuzundan IP verileceği belirlenir.

---

# DNS Ayarı

| Ayar | Değer |
|---|---|
| DNS Server #1 | `10.10.100.100` |

### Neden Yapılır?
VPN kullanıcıları DNS sorgularını AD sunucusuna gönderir.

---

# Authentication / Portal Mapping

| User Group | Portal |
|---|---|
| IK_VPN_grb | IK_portal |
| IT_VPN_grb | IT_portal |
| MUHASEBE_VPN_grb | muhasebe_portal |
| YONETIM_VPN_grb | yonetim_portal |
| OUTSOURCE_VPN_grb | outsource_portal |

### Neden Yapılır?
Kullanıcının grubuna göre doğru VPN yetkisini alması sağlanır.

---

# 9. SNAT (Outsource İçin)

## Menü

```text
Policy & Objects → IP Pools → Create New
```

## Yapılandırma

| Ayar | Değer |
|---|---|
| Name | `outsource-snat` |
| Type | Overload |
| External IP | `76.76.76.77` |

### Neden Yapılır?
Outsource kullanıcıları internete belirli bir sabit IP ile çıkar.

---

# 10. Firewall Policy

## Menü

```text
Policy & Objects → IPv4 Policy
```

---

# Outsource → Internet Policy

| Ayar | Değer |
|---|---|
| Incoming Interface | `ssl.root` |
| Outgoing Interface | `internet-zone` |
| Source | `OUTSOURCE_VPN_pool` + `OUTSOURCE_VPN_grb` |
| Destination | all |
| Service | all |
| Action | accept |
| NAT | Enabled |

---

## IP Pool Configuration

| Ayar | Değer |
|---|---|
| Use Dynamic IP Pool | Enabled |
| IP Pool | `outsource-snat` |

### Neden Yapılır?
Outsource kullanıcılarının firewall üzerindeki belirlenen IP ile internete çıkması sağlanır.

---

# IK → AD Policy

| Ayar | Değer |
|---|---|
| Source | `IK_VPN_pool` + `IK_VPN_grb` |
| Destination | `AD-10.10.100.100` |
| Service | `AD-Services` |
| NAT | Disabled |

### Neden Yapılır?
IK kullanıcılarının sadece gerekli AD servislerine erişmesi sağlanır.

---

# Diğer Policyler

Aynı mantıkla:

- Muhasebe → Logo
- Yönetim → ITSM
- IT → Tüm sunucular

policyleri oluşturulmalıdır.

### Neden Yapılır?
Her departmanın yalnızca ihtiyacı olan sistemlere erişmesi için.

---

# Trafik Akışı

```text
Kullanıcı
   ↓
SSL-VPN
   ↓
DNS Sorgusu
   ↓
İç Ağ / İnternet Trafiği
   ↓
Firewall Policy
   ↓
NAT
   ↓
İnternet
```

### Neden Yapılır?
VPN trafiğinin firewall üzerinden kontrollü ve güvenli şekilde yönlendirilmesi sağlanır.

---

# Dikkat Edilmesi Gerekenler

- Policy sırası önemlidir.
- NAT yalnızca gerekli policylerde açılmalıdır.
- Split Tunnel yanlış yapılandırılırsa tüm trafik VPN’e düşebilir.
- SSL-VPN erişimi mutlaka ülke bazlı sınırlandırılmalıdır.
- Gereksiz şekilde `service: all` kullanılmamalıdır.
- Mümkün olduğunca özel servis objeleri kullanılmalıdır.
