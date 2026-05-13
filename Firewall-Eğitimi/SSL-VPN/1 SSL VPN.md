
# FortiGate SSL-VPN Kısa Konu Anlatımı

# SSL-VPN Nedir?

SSL-VPN, kullanıcıların internet üzerinden güvenli şekilde şirket ağına bağlanmasını sağlayan VPN teknolojisidir.

Temel mantık:

```text
Kullanıcı → İnternet → FortiGate → İç Ağ
```

FortiGate:

- kullanıcıyı doğrular
- IP verir
- yetki kontrolü yapar
- izin verilen kaynaklara erişim sağlar

---

# SSL-VPN Yapısındaki Temel Bileşenler

| Yapı | Görevi |
|---|---|
| WAN Interface | İnternet bağlantısı |
| User Group | Kullanıcıları gruplamak |
| IP Pool | VPN kullanıcılarına IP dağıtmak |
| SSL-VPN Portal | Kullanıcının erişim yetkilerini belirlemek |
| Address Object | Sunucuları tanımlamak |
| Firewall Policy | Trafiğe izin vermek |
| Portal Mapping | Kullanıcıyı doğru portala yönlendirmek |

---

# 1. WAN Ayarı

## Nasıl Oluşturulur?

```text
Network → Interfaces → wan1
```

## Neden Yapılır?

Firewall’ın internete çıkabilmesi ve SSL-VPN yayını yapabilmesi için.

---

# 2. Default Route

## Nasıl Oluşturulur?

```text
Network → Static Routes → Create New
```

## Örnek

```text
Destination : 0.0.0.0/0
Gateway : ISP Gateway
```

## Neden Yapılır?

Firewall’ın internet trafiğini hangi gateway üzerinden göndereceğini belirlemek için.

---

# 3. Zone Oluşturma

## Nasıl Oluşturulur?

```text
Network → Interfaces → Zones
```

## Neden Yapılır?

Policy yönetimini kolaylaştırmak için.

Örnek:

```text
internet-zone
server-zone
```

---

# 4. Address Object

## Nasıl Oluşturulur?

```text
Policy & Objects → Addresses → Create New
```

## Örnek

```text
AD-Server → 10.10.100.100
```

## Neden Yapılır?

IP yerine isim kullanarak yönetimi kolaylaştırmak için.

---

# 5. User Group

## Nasıl Oluşturulur?

```text
User & Device → User Groups → Create New
```

## Örnek

```text
IK_VPN_grb
IT_VPN_grb
```

## Neden Yapılır?

Kullanıcılara grup bazlı yetki vermek için.

---

# 6. VPN IP Pool

## Nasıl Oluşturulur?

```text
Policy & Objects → Addresses → Create New
```

## Örnek

```text
172.16.10.0/28
```

## Neden Yapılır?

VPN kullanıcılarına dağıtılacak IP aralığını belirlemek için.

---

# 7. SSL-VPN Portal

## Nasıl Oluşturulur?

```text
VPN → SSL-VPN Portals → Create New
```

## Temel Ayarlar

| Ayar | Görev |
|---|---|
| Tunnel Mode | VPN tünelini açar |
| Split Tunnel | Trafik yönünü belirler |
| Routing Address | Erişilecek sistemleri belirler |
| Source IP Pool | Kullanılacak IP havuzu |

## Neden Yapılır?

Her kullanıcı grubuna farklı erişim yetkisi vermek için.

---

# Split Tunnel

## Açık ise

Sadece şirket trafiği VPN’den geçer.

## Kapalı ise

Tüm trafik VPN’den geçer.

---

# 8. SSL-VPN Settings

## Nasıl Yapılır?

```text
VPN → SSL-VPN Settings
```

---

# Listen Interface

VPN’in hangi interface üzerinden yayın yapacağını belirler.

Örnek:

```text
wan1
```

---

# Listen Port

VPN’in çalışacağı portu belirler.

Örnek:

```text
10443
```

---

# DNS Ayarı

VPN kullanıcılarının kullanacağı DNS sunucusudur.

Genellikle AD Server kullanılır.

---

# Portal Mapping

## Neden Yapılır?

Kullanıcının grubuna göre doğru portalı kullanmasını sağlamak için.

Örnek:

```text
IK_VPN_grb → IK_portal
```

---

# 9. SNAT / IP Pool NAT

## Nasıl Oluşturulur?

```text
Policy & Objects → IP Pools → Create New
```

## Neden Yapılır?

VPN kullanıcılarının belirli IP ile internete çıkmasını sağlamak için.

---

# 10. Firewall Policy

## Nasıl Oluşturulur?

```text
Policy & Objects → IPv4 Policy → Create New
```

## Temel Alanlar

| Alan | Görevi |
|---|---|
| Incoming Interface | Trafiğin geldiği yer |
| Outgoing Interface | Trafiğin gittiği yer |
| Source | Kaynak |
| Destination | Hedef |
| Service | Port / protokol |
| Action | İzin / engel |
| NAT | NAT yapılacak mı |

---

# NAT Kullanımı

## NAT Açık

Genellikle:

```text
VPN → İnternet
```

trafiğinde kullanılır.

---

## NAT Kapalı

Genellikle:

```text
VPN → İç Ağ
```

trafiğinde kullanılır.

---

# Trafik Akışı

```text
Kullanıcı
   ↓
SSL-VPN
   ↓
Kimlik doğrulama
   ↓
IP dağıtımı
   ↓
Firewall Policy
   ↓
İç Ağ / İnternet
```

---

# Özet

SSL-VPN’de temel amaç:

- Kullanıcıyı güvenli bağlamak
- Doğru IP vermek
- Yetki kontrolü yapmak
- Sadece izin verilen kaynaklara erişim sağlamak
- Trafiği firewall üzerinden kontrol etmektir.
