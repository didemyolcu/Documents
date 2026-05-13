

# FortiGate Firmware Güncelleme

Bu doküman FortiGate cihazının firmware güncelleme işlemini içerir.

---

# Senaryo

| Bilgi | Değer |
|---|---|
| Model | FortiGate 100E |
| Mevcut Sürüm | 7.2.10 |
| Hedef Sürüm | 7.2.13 |

---

# 1. Mevcut Firmware Versiyonunu Kontrol Et

## Menü

```text
Dashboard → Status → System Information
```

---

# Kontrol Edilecek Alan

| Alan | Açıklama |
|---|---|
| Firmware Version | Kullanılan firmware sürümü |

Örnek:

```text
v7.2.10 (Mature)
```

---

# 2. Konfigürasyon Yedeği Al

## CLI

```bash
execute backup config flash
```

---

# Amaç

Firmware güncellemesi öncesinde:

- mevcut ayarların yedeğini almak
- rollback ihtimaline karşı hazırlıklı olmak

---

# 3. Doğru Firmware Dosyasını İndir

## Fortinet Support Portal

Fortinet support hesabına giriş yapılır.

---

# Current Product

| Alan | Değer |
|---|---|
| Model | FortiGate-100E |

---

# Current Version

| Alan | Değer |
|---|---|
| Current Firmware | 7.2.10 |

---

# Upgrade To

| Alan | Değer |
|---|---|
| Target Firmware | 7.2.13 |

---

# Önemli

Ara sürüm varsa:

```text
Sıralı upgrade yapılmalıdır.
```

Örnek:

```text
7.0.x → 7.2.x
```

gibi büyük geçişlerde doğrudan upgrade desteklenmeyebilir.

---

# Firmware Dosyasını İndir

Model seçildikten sonra:

```text
Download
```

ile firmware dosyası indirilir.

---

# 4. Firmware Güncellemesini Başlat

## Menü

```text
Dashboard → System Information → Firmware
```

---

# Firmware Upload

```text
Update Firmware
```

butonuna basılır.

---

# Dosya Yükleme

İndirilen:

```text
.out
```

uzantılı firmware dosyası seçilir.

---

# Güncellemeyi Başlat

Firmware dosyası yüklendikten sonra:

```text
Upgrade
```

başlatılır.

---

# Güncelleme Sırasında

- cihaz reboot olur
- interface trafiği kesilir
- erişim geçici olarak kapanır

---

# 5. Güncelleme Sonrası Kontrol

## Menü

```text
Dashboard → System Information
```

---

# Kontrol

| Alan | Beklenen |
|---|---|
| Firmware Version | 7.2.13 |

---

# Dikkat Edilecek Noktalar

- Doğru model firmware’i indirilmeli
- Güncelleme öncesi backup alınmalı
- Ara sürüm gerekiyorsa sırayla geçilmeli
- Maintenance window’da yapılmalı
- HA varsa upgrade sırası planlanmalı
