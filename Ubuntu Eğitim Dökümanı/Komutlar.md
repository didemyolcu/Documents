
## Linux Mimarisi

Kernel )) Shell )) User Interface (UI) 

 - `echo $SHELL` : Unix/Linux sistemlerde şu anda kullandığın varsayılan kabuğun (örneğin `/bin/bash`, `/bin/zsh`) yolunu terminale yazdırır. 

- `echo $BASH_VERSION` : Sistemde çalışan **Bash kabuğunun sürüm numarasını** terminale yazdırır (örneğin `5.1.16`). 

-   `cd`: Terminalde bulunduğun dizini (klasörü) değiştirir.
    
-   `echo`: Verilen metni veya değişken değerini ekrana yazdırır.
    
-   `cat`: Dosya içeriğini terminalde görüntüler (veya birleştirir).
-- `-n flag` : Dosya içeriğini terminalde gösterirken **her satırın başına satır numarası ekler**.
    
-   `<`: Bir komutun girdisini bir dosyadan almasını sağlar (input redirect).
    
-   `>`: Bir komutun çıktısını bir dosyaya yazar (output redirect, varsa içeriği siler).
--    `>` : Çıktıyı dosyaya yazar **ve dosya varsa içeriğini silip üzerine yazar** (overwrite).
--  `>>` : Çıktıyı dosyanın **sonuna ekler**, mevcut içeriği silmez (append).

- `man`, bir komutun veya programın **kullanım kılavuzunu (manual sayfasını)** terminalde görüntüler (örneğin `man ls`).

- `|` (pipe) : bir komutun çıktısını başka bir komutun girdisi olarak aktarır.
- `grep`, dosya veya komut çıktısı içinde belirli bir metni (pattern) arayıp eşleşen satırları listeler.

-   `touch`: Yeni boş bir dosya oluşturur (veya varsa dosyanın tarih bilgisini günceller).
    
-   `mkdir`: Yeni bir dizin (klasör) oluşturur.

-   `rm`: Dosyaları (ve `-r` parametresiyle dizinleri) siler.
--   `rm -r dizin_adi` → Dizini ve içindekileri siler.
-- `rm -rf dizin_adi` → Dizini ve içindekileri **zorla ve onay sormadan** siler (dikkatli kullanılmalı).
    
-   `rmdir`: Sadece **boş** dizinleri siler.

- `ls`, bulunduğun dizindeki dosya ve klasörleri listeler.
--   `ls -l` → Detaylı liste (izinler, sahip, boyut, tarih).
    --   `ls -a` → Gizli dosyaları da gösterir (`.` ile başlayanlar).
    --   `ls -la` → Hem gizli dosyalar hem detaylı liste.
    --   `ls -h` → Boyutları okunabilir formatta gösterir (KB, MB).
    --   `ls -R` → Alt dizinleri de recursive olarak listeler.
    --   `ls -t` → Dosyaları değişiklik tarihine göre sıralar.
    --   `ls -S` → Dosyaları boyuta göre sıralar.

- `mv`, dosya veya klasörleri **taşımak** ya da **yeniden adlandırmak** için kullanılır.
--   `mv dosya.txt yeni.txt` → Dosyanın adını değiştirir.
--   `mv dosya.txt /hedef/klasor/` → Dosyayı başka bir dizine taşır.
- `rename`, birden fazla dosyanın adını belirli bir kurala göre **toplu olarak değiştirmek** için kullanılır (örneğin uzantı değiştirme veya metin değiştirme).

- `cp`, dosya veya klasörleri **kopyalamak** için kullanılır.
--   `cp dosya.txt kopya.txt` → Dosyayı aynı dizinde kopyalar.
--   `cp dosya.txt /hedef/klasor/` → Dosyayı başka dizine kopyalar.
--   `cp -r klasor/ yeni_klasor/` → Klasörü ve içindekileri kopyalar (recursive).

-   `find`: Belirtilen dizinde dosya/klasörleri **anlık olarak tarayarak** isim, tür, boyut gibi kriterlere göre arar.  
    Örnek: `find /home -name "*.txt"`
   
-   `locate`: Dosyaları **önceden oluşturulmuş bir veritabanı** üzerinden çok hızlı arar (güncel olması için `updatedb` gerekir).  
    Örnek: `locate dosya.txt`

- `tar`, birden fazla dosya ve klasörü **tek bir arşiv dosyasında toplamak** (veya arşivden çıkarmak) için kullanılır.
--   `tar -cvf arsiv.tar klasor/` → Arşiv oluşturur.
--   `tar -xvf arsiv.tar` → Arşivi çıkarır.
--   `tar -czvf arsiv.tar.gz klasor/` → Sıkıştırarak arşiv oluşturur (gzip).
--   `tar -xzvf arsiv.tar.gz` → `.tar.gz` arşivini çıkarır.

- `more`, uzun dosya içeriklerini **sayfa sayfa** görüntülemek için kullanılır; boşluk tuşuyla ilerlenir, `q` ile çıkılır.
- `head`: Bir dosyanın **başındaki** satırları gösterir (varsayılan 10 satır).
- `tail`: Bir dosyanın **sonundaki** satırları gösterir (varsayılan 10 satır).
- `tac`, bir dosyanın içeriğini **ters sırayla** (son satırdan başlayarak) gösterir; yani `cat` komutunun tersidir.
-    `nano`: Terminal tabanlı, **basit ve kullanıcı dostu** bir metin editörüdür; alt kısımda kısayollar gösterilir.   
-   `vi`: Terminal tabanlı, **güçlü ve modlu** (insert/command mode) bir metin editörüdür; daha karmaşık ama çok esnektir.

- `w` komutu, sistemde **şu anda oturum açmış kullanıcıları** ve ne yaptıklarını gösterir.
- `id` komutu, mevcut kullanıcının **UID (kullanıcı ID), GID (grup ID) ve üye olduğu grupları** tek satırda gösterir.
- `sudo` komutu, bir işlemi **geçici olarak yönetici (root) yetkileriyle** çalıştırmayı sağlar.
- `passwd` komutu, Linux’ta **kullanıcı şifresini değiştirmek veya ayarlamak** için kullanılır.
- `sudo su` komutu, mevcut kullanıcının yetkisini kullanarak **root (yönetici) kullanıcısına geçiş yapmayı** sağlar.
- `su` (switch user) komutu, Linux’ta **başka bir kullanıcı hesabına geçiş yapmak** için kullanılır ve genellikle hedef kullanıcının şifresini ister.


- Linux’ta yetkiler 3 kullanıcı kategorisine göre belirlenir:
**1️⃣ User (u)** → Dosyanın sahibi   (ilk 3)
**2️⃣ Group (g)** → Dosyanın ait olduğu grup (orta 3)  
**3️⃣ Other (o)** → Sistemindeki diğer tüm kullanıcılar (son 3)
Her kategori için 3 izin vardır:
**r (read)** → Okuma 4
**w (write)** → Yazma 2
**x (execute)** → Çalıştırma / Klasöre girme 1
     Görebilmek için  `ls -la`

- `chown` komutu, dosya veya klasörün **sahibini ve grubunu değiştirmek** için kullanılır.
- `chmod` komutu, dosya veya klasörün **okuma ( r ), yazma ( w ) ve çalıştırma ( x ) izinlerini ayarlamak** için kullanılır.
- `adduser` komutu, kullanıcıyı interaktif şekilde (home dizini, şifre, grup ayarlarıyla birlikte) oluşturan daha kullanıcı dostu bir araçtır.
- `useradd` komutu ise daha düşük seviyeli ve manuel ayar gerektiren temel kullanıcı oluşturma komutudur.
- `groupadd` komutu, Linux sistemde **yeni bir kullanıcı grubu oluşturmak** için kullanılır.
- `groups` komutu, bir kullanıcının **üye olduğu tüm grupları** listelemek için kullanılır.
- `usermod` komutu, mevcut bir kullanıcının **grup üyeliği, home dizini, shell veya UID gibi bilgilerini değiştirmek** için kullanılır.
- `deluser` komutu, kullanıcıyı (isteğe bağlı olarak home diziniyle birlikte) silen daha güvenli ve kullanıcı dostu bir araçtır.
- `userdel` komutu ise kullanıcı hesabını silen daha düşük seviyeli temel sistem komutudur.
- `gedit`, Linux’ta grafik arayüzlü (GUI) basit ve kullanımı kolay bir metin düzenleyicisidir. 


- `ps aux` komutu, Linux sistemde çalışan **tüm kullanıcıların tüm süreçlerini** CPU ve RAM kullanımı gibi detaylı bilgilerle birlikte listeler.
-- `ps -u root` (veya yaygın yazımıyla `ps u -U root`) komutu, sistemde **root kullanıcısına ait çalışan süreçleri** listeler.
- `kill` komutu, belirli bir **PID numarasına sahip süreci** sonlandırmak için kullanılır.
-- `kill -l` komutu, Linux’ta kullanılabilecek **tüm sinyal (signal) türlerini** listeler (örneğin `SIGTERM`, `SIGKILL` gibi).
-- `kill -9` komutu, belirtilen PID’ye **SIGKILL sinyali** göndererek süreci zorla ve anında sonlandırır (sürece kapanma şansı tanımaz).
-- `kill -15` komutu (varsayılan olarak `kill`), belirtilen PID’ye **SIGTERM (15)** sinyali göndererek süreci **nazikçe sonlandırmayı** ister; süreç kendini düzgün şekilde kapatma şansı bulur.
--  `killall` komutu, **isimle belirtilen tüm süreçleri** sonlandırmak için kullanılır.
- `pkill` komutu ise **süreç adını kullanarak** bir veya birden fazla süreci sonlandırmak için kullanılır.

- `systemctl` komutu, Linux’ta **systemd tabanlı servisleri ve sistem birimlerini yönetmek** için kullanılır.
--  `systemctl start servis` → Servisi başlatır
--   `systemctl stop servis` → Servisi durdurur
--   `systemctl restart servis` → Servisi yeniden başlatır
--   `systemctl status servis` → Servis durumunu gösterir
--   `systemctl enable servis` → Açılışta otomatik başlatır
--   `systemctl disable servis` → Açılışta başlamasını engeller
--   `systemctl reload servis` → Servisi kapatmadan yapılandırmayı yeniler
--   `systemctl list-units --type=service` → Servisleri listeler
--   `systemctl list-units --type=service --state=running` → Çalışan servisleri listeler

- `service` komutu, Linux’ta (özellikle eski init sistemlerinde) **servisleri başlatmak, durdurmak ve yeniden başlatmak** için kullanılan basit bir yönetim aracıdır.
--   `sudo service nginx start` → Servisi başlatır   
--   `sudo service nginx stop` → Servisi durdurur
--   `sudo service nginx restart` → Servisi yeniden başlatır
--   `sudo service nginx status` → Servis durumunu gösterir

## Kabuk Programlama
1. `nano server-health.sh`
2. `chmod +x server-health.sh`


> #!/bin/bash
> 
> LOG_FILE="/var/log/server-health.log" DATE=$(date "+%Y-%m-%d
> %H:%M:%S")
> 
> echo "======================================" echo "      SERVER
> HEALTH REPORT" echo "      $DATE" echo
> "======================================"
> 
> #Sistem Güncelleme Kontrolü echo "" echo "🔄 Checking for updates..." apt update -qq > /dev/null 2>&1 UPDATES=$(apt list --upgradable
> 2>/dev/null | grep -v "Listing" | wc -l)
> 
> if [ "$UPDATES" -gt 0 ]; then
>     echo "⚠️  $UPDATES package(s) can be upgraded." else
>     echo "✅ System is up to date." fi
> 
> #Disk Kullanımı echo "" echo "💾 Disk Usage:" df -h | grep -E '^/dev/' 
> 
> #RAM Kullanımı echo "" echo "🧠 Memory Usage:" free -h
> 
> #CPU Load echo "" echo "⚙️ CPU Load:" uptime
> 
> #Docker Kontrol echo "" if command -v docker &> /dev/null; then
>     echo "🐳 Docker Status:"
>     systemctl is-active docker
>     docker ps --format "table {{.Names}}\t{{.Status}}" else
>     echo "🐳 Docker not installed." fi
> 
> #Nginx Kontrol echo "" if systemctl list-unit-files | grep -q nginx; then
>     echo "🌐 Nginx Status:"
>     systemctl is-active nginx else
>     echo "🌐 Nginx not installed." fi
> 
> echo "" echo "======================================" echo "Report
> completed at $DATE" echo "======================================"
> 
> # Log kaydı echo "Report generated at $DATE" >> $LOG_FILE
3. `./server-health.sh`

- `dpkg`, Debian tabanlı sistemlerde (`.deb`) paketlerini **kurmak/kaldırmak**, **bilgi sorgulamak** ve **kurulu paketleri yönetmek** için kullanılan düşük seviye paket yönetim komutudur.
-- `dpkg -l`, sistemde **kurulu (ve/veya bilinen) paketleri** listeleyip her birinin **durumunu** (ii, rc vb.), **sürümünü** ve kısa **açıklamasını** gösterir.
- `apt`, Debian tabanlı sistemlerde paket depolarından yazılım **kurmak/güncellemek/kaldırmak** ve bağımlılıkları otomatik yönetmek için kullanılan paket yönetim aracıdır.
-  `apt update`, sistemin APT depo (repository) listesini yenileyip **paket indekslerini günceller**; yani hangi paketin hangi sürümü depolarda var, onu güncel hale getirir (paketleri kurmaz).
- `apt install <paket>`, depolardan seçtiğin paketi **indirip kurar** ve gerekiyorsa **bağımlılıklarını da otomatik yükler**.
- `apt search <anahtar_kelime>`, depolardaki paketleri isim/açıklamalarına göre **arama** yapıp eşleşen paketleri listeler.
- `apt install build-essential`, C/C++ derlemek için gereken temel geliştirme araçlarını (özellikle `gcc/g++`, `make` ve ilgili başlık/araçlar) sisteme kurar.
- `make`, bir projedeki **Makefile** kurallarını okuyup kaynak kodu **derleyerek hedefleri (build/test/install vb.) otomatik oluşturan** komuttur
