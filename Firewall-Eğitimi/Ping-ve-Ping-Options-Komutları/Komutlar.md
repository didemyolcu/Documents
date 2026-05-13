
# FortiGate Ping ve Ping-Options Komutları

Bu doküman, FortiGate üzerinde kullanılan temel bağlantı test komutlarını ve kullanım senaryolarını açıklamaktadır.

---

# 1. execute ping

## Ne İşe Yarar?

`execute ping` komutu, hedef IP adresine erişim olup olmadığını test etmek için kullanılır.

FortiGate üzerinden ICMP paketi göndererek bağlantı kontrolü sağlar.

---

## Temel Kullanım

```bash
execute ping <hedef_ip>
```

---

## Örnek

```bash
execute ping 8.8.8.8
```

Bu örnek, FortiGate’in internet erişimi olup olmadığını test eder.

---

## Nerelerde Kullanılır?

### Gateway Kontrolü

Firewall’un gateway’e erişip erişemediğini kontrol etmek için kullanılır.

Örnek:

```bash
execute ping 192.168.1.1
```

---

### İnternet Kontrolü

İnternet bağlantısının aktif olup olmadığını test etmek için kullanılır.

Örnek:

```bash
execute ping 8.8.8.8
```

---

### Karşı Firewall Erişim Testi

Site-to-Site VPN veya farklı lokasyonlardaki firewall cihazlarının erişilebilirliği kontrol edilir.

Örnek:

```bash
execute ping 10.10.10.1
```

---

### VPN Tünel Testi

VPN tünelinin aktif çalışıp çalışmadığı test edilir.

Örnek:

```bash
execute ping 172.16.1.1
```

---

### VLAN’lar Arası İletişim Testi

Farklı VLAN’ların birbirine erişimi kontrol edilir.

Örnek:

```bash
execute ping 192.168.20.1
```

---

# 2. execute ping-options source

## Ne İşe Yarar?

`execute ping-options source` komutu, ping paketinin hangi interface veya IP adresi üzerinden gönderileceğini belirler.

---

## Neden Önemlidir?

FortiGate üzerinde birden fazla interface bulunduğunda, firewall varsayılan route’a göre farklı bir interface üzerinden çıkış yapabilir.

Bu durumda yapılan ping testi yanlış sonuç verebilir.

Kaynak IP belirlenerek testin doğru interface üzerinden yapılması sağlanır.

---

## Temel Kullanım

```bash
execute ping-options source <kaynak_ip>
```

---

## Örnek

```bash
execute ping-options source 192.168.10.1
```

Bu komut, ping paketlerinin `192.168.10.1` IP adresine sahip interface üzerinden gönderilmesini sağlar.

---

# Birlikte Kullanım Örneği

## Senaryo

- VLAN10 IP adresi: `192.168.10.1`
- VLAN20 IP adresi: `192.168.20.1`

VLAN10’dan VLAN20’ye erişim testi yapılacaktır.

---

## Adım 1 — Kaynak Interface Belirleme

```bash
execute ping-options source 192.168.10.1
```

---

## Adım 2 — Hedefe Ping Atma

```bash
execute ping 192.168.20.1
```

---

# Nerelerde Kullanılır?

## Inter-VLAN Testleri

Farklı VLAN’lar arasında iletişim testi yapmak için kullanılır.

---

## VPN Routing Testleri

VPN trafiğinin doğru interface üzerinden çıkıp çıkmadığını kontrol etmek için kullanılır.

---

## SD-WAN Testleri

SD-WAN ortamlarında trafiğin hangi WAN hattından çıktığını doğrulamak için kullanılır.

---

## Multi-WAN Ortamları

Birden fazla internet hattı bulunan yapılarda doğru WAN interface’inin kullanılıp kullanılmadığı test edilir.

---

# Kullanışlı Ek Komutlar

## Ping Ayarlarını Görüntüleme

```bash
execute ping-options view-settings
```

---

## Ping Sayısını Değiştirme

```bash
execute ping-options repeat-count 10
```

---

## Paket Boyutu Belirleme

```bash
execute ping-options data-size 1400
```

---

## Ping Ayarlarını Sıfırlama

```bash
execute ping-options reset
```

---

# Özet

| Komut | Amaç |
|---|---|
| `execute ping` | Hedefe erişim testi yapmak |
| `execute ping-options source` | Ping’in hangi interface/IP üzerinden çıkacağını belirlemek |
| `execute ping-options reset` | Ping ayarlarını varsayılana döndürmek |
| `execute ping-options view-settings` | Aktif ping ayarlarını görüntülemek |

---
