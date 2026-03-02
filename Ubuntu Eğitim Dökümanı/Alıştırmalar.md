


## **Linux eğitim dökümanı**

## İlk Problemlerimiz

- Terminali aç ve **shell versiyonunu** öğren.
`Echo $0` → hangi shelli kullandığımızı öğren.
Örn çıktı : -bash
`bash –version`
örn çıktı: 5.2.21

- Metin editörü kullarak **masaüstünde boş bir döküman** oluştur.
`nano deneme.txt`
Didem Yolcu 
CTRL+O 
CTRL+X

- Terminal kullanarak döküman içeriğine ismini yazdır.
`echo "Didem" > deneme.txt` : Dosyanın üstüne yazar.
`echo "Didem" >> deneme.txt` : Dosyanın en altına ekler.

- Döküman içeriğini terminalde çıktı olarak al.
`cat deneme.txt`


Döküman içeriğine soy adını da ekle. **(İçeriği silmeden)**
`echo "Yolcu" >> deneme.txt` : Dosyanın en altına ekler.
 

Döküman içeriğini eğitmen biografisi ile **değiştir**. :)
`cp dokuman.txt deneme.txt`  
  
Döküman içeriğinde geçen **güvenlik** kelimesinin geçtiği satırı terminale çıktı olarak al.
`grep "güvenlik" deneme.txt `



## Alıştırma Soruları:

1.  Metin editörü kullanarak Documents dizini içerisinde boş bir döküman oluşturalım. Dökümanın adı **ilk** olsun.
    `mkdir BolumSonu`
    `touch BolumSonu/ilk`

2.  Oluşturduğumuz dökümanın içerisine kullandığımız **Shell'in adını ve versiyonunu** yazdıralım.
    `echo $SHELL >> ilk` 
    `echo $BASH_VERSION >> ilk`

    
3.  Terminalde **ilk** adlı dökümanımızın içeriğini aynı dizinde **shell** adlı başka bir dökümana aktaralım.
    `cp ilk shell`
      
    
4.  shell adlı dökümanımızın içeriğinde **free** kelimesi geçen satırları **özgürlükiçin** adında başka bir dökümana aktaralım.
   `cat shell | grep free >> ozgurlukicin`
      

5.  Link :https://drive.google.com/open?id=1KJo92GiJVhwR4JuzsTu-dVs1D2a79jRi
Paylaşılan linkteki dökümanı indirelim. Döküman içeriğinde **özgür** kelimesi geçen satırı **özgürlükiçin** adındaki dökümanımıza ekleyelim.
`wget --no-check-certificate 'https://docs.google.com/uc?export=download&id=1KJo92GiJVhwR4JuzsTu-dVs1D2a79jRi' -O dokuman.txt` 
`grep "özgür" dokuman.txt > ozgurlukicin` 

## İkinci Problemlerimiz

 - "_Home_" dizini içerisinde "**ilk**" adında bir dosya oluştur.
`mkdir Home`
`touch ilk`

 - "_Home_" dizini içerisinde "**denemedizin**" adında bir dizin oluştur.
`mkdir /Home/denemedizin`

 - "**_ilk_**" adlı dosyayı sil, "_Home_" dizini içerisinde "**ikinci**" adında boş bir dosya oluştur.
`rm ilk`
`touch ikinci`

 - _Home_ dizininin içeriğini görüntüle.
`cd Home`
`ls`
yada 
`ls Home`

 - _denemedizin_ adlı dizini sil ve "Home" dizini içerisinde _denemedizin2_ adlı boş bir dizin oluştur.
`rm -r denemedizin`
`mkdir denemedizin2`

 - "**ikinci**" adlı dosyayı "_denemedizin2_" adlı dizine taşı.
`mv ikinci denemedizin2`

- _denemedizin2_ adlı dizini Desktop dizinine taşı.
`mv denemedizin Desktop`

- _denemedizin2_ adlı dizine gir ve **ikinci** adlı dosyayı aynı dizin içerisine kopyala.Dizin içeriğini görüntüle.
`cp ikinci ikinci2`

-  _denemedizin2_ adlı dizini _Documents_ dizinine kopyala. 
`cp Desktop/denemedizini2 Documents` 

- Terminalde **ikinci** adlı dosyayı ara ve bul.
`find -name ikinci`

- _denemedizin2_ adlı dizinde bulunan **ikinci** adlı dosyayı arşivle ve daha sonra masaüstüne taşıyıp arşivden çıkart.
`tar -cvf denemedizin.tar denemedizin2/`
`mv Documents/denemedizin.tar Desktop/`
`tar -xvf denemedizin2.tar`

- _denemedizin2_ adlı dizini arşivle ve home dizini içerisinde _arsivdencıkart_ adlı boş bir dizin içerisine çıkart.
`tar -xvf Desktop/denemedizin.tar`

- Masaüstünde bulunan ikinci adlı dosya içeriğine / dizini içeriğini yönlendir.
- `ls / > _Home_/Documents/denemedizin2/ikinci`


- **ikinci** adlı dosya içeriğinin **_ilk 8 satırını_** masaüstünde **üçüncü** adlı boş bir dosyaya yönlendir.
`head -n 8 ikinci >> Desktop/üçüncü`

- **Üçüncü** adlı dosyanın içeriğini **dördüncü** adlı boş bir dosyaya içeriği tersten aktarıcak şekilde yönlendir.
`tac üçüncü >> dördüncü` 


## Bölüm Sonu Alıştırma Soruları

https://drive.google.com/open?id=1fi9NoBFoUvJMmtiEh5nv-CSfsmnRPL3e

1. Linkteki Dosyayı arşivden /home/"kullanıcı-adınız"/Documents/IlkSoru adlı dizine çıkaralım
`wget --no-check-certificate https://drive.google.com/open?id=1fi9NoBFoUvJMmtiEh5nv-CSfsmnRPL3e -O Ilksoru.tar`
`tar -xf Ilksoru.tar -C ~/Documents/ilksoru`


2. Dizin İçeriğini Masaüstüne Taşıyalım.
`mv Documents/ilksoru/içerik1 Desktop/`

3. Taşıdığımız dizini Masaüstünde "ÜçüncüSoru" adlı boş bir dizin içerisine kopyayalim.
 `cp -r Desktop/ilksoru Desktop/üçüncüsoru`

4. Terminal üzerinde "içerik1" adlı dosyaları bulalım.
`sudo find / -name içerik1`

5. Bulduğumuz dosyaların içeriklerini tek tek Masaüstü içerisinde "beşincidosya" adında bir dosya içerisine yönlendirelim.(Dosya içerikleri birbirine eklensin)
`cd Desktop`
`cat ilksoru/içerik1 >> besincisoru`
`cat ilksoru/içerik1 >> besincisoru`
6. "beşincidosya" içeriğine Masaüstü dizin içerik çıktısını ekleyelim.
`ls ~/Desktop >> besincidosya `

7. "beşincidosya" adlı dosya içeriğinin ilk satırına "bölümSonu" kelimesini ekleyip kaydedelim ve çıkalim.
`vi besincidosya`
i + bölümSonu + esc + wq

8. Dosya içeriğini tersten yazdırıp "son" kelimesi geçen satırları filtreleyelim.
`tac besincidosya | grep son`

## Üçüncü Problemlerimiz

- Sistemde **oturumu açmış olduğun** kullanıcı(ları) terminalde çıktı olarak al.
 `w`

- Oturumu açık olan kullanıcının kullanıcı **id'sini** öğren.
`id`
**NOT : ** 0 id'si her zaman root'dadır. İsim root yerine başka bir şey olabilir. 

- Sistemdeki bütün kullanıcıları görüntüle.
`cat /etc/passwd`
` cat /etc/passwd | grep didem `

- Oturum açtığın kullanıcının bulunduğu **grupları** öğren.
`groups`
`cat /etc/group`
- Oturum açtığın kullanıcı ile _/etc_ içerisinde bir dosya oluştur.
`sudo touch /etc/deneme`

- **Root** kullanıcısı olarak login ol.
`sudo su`

- Terminal üzerinden kullanıcı değişikliği yap.
`su didem`

- Masaüstünde sadece **root** kullanıcısının yetkilere sahip olduğu boş bir döküman oluştur. Dökümanın adı _yetki_ olsun.
`sudo touch yetki`

- Yeni bir kullanıcı oluştur, kullanıcının adı **yetkilibey** olsun.
`sudo adduser yetkilibey`

- Yeni bir grup oluştur. Grubun adı **yetkililer** olsun.
`sudo gruopadd yetkililer`

- Oturum açtığın kullanıcıyı "**yetkililer**" adlı gruba ekle.
`sudo usermod -aG yetkililer yetkili`

- _yetki_ adı verdiğimiz dökümanın sahibini **yetkilibey** olarak değiştir.
 `sudo chown yetkili yetki/`

- _yetki_ adı verdiğimiz dökümanın grup sahipliği yetkililer grubunda dahil et.
`sudo chown yetkili:yetkililer yetki/`

- Oturum açtığınız kullanıcı ile _yetki_ adlı dökümanın içeriğine **_yetkilendirildim_** yazısını yönlendir.
`sudo sh -c 'echo Yetkilendirildim. >> yetki/yeni`

- **yetkilibey** adlı kullanıcıyı sistemden kaldır.
`sudo deluser yetkili`

- **yetkililer** adlı grubu sistemden kaldır.
 `sudo delgroup yetkililer` 
 

## Bölüm Sonu Alıştırma

1. Terminal Üzerinden **_ilkgrup_** adında bir grup oluştur.
`sudo groupadd ilkgrup`
2. Terminal üzerinden **_ikincigrup_** adında bir grup oluştur.
`sudo groupadd ikincigrup`
3. [Linkteki](https://drive.google.com/open?id=1C5UrkjvuVP4RT3UbAJqBpXVFui27CYF_) dosyayı indirip arşivden çıkart.
`wget "https://drive.google.com/uc?export=download&id=1C5UrkjvuVP4RT3UbAJqBpXVFui27CYF_" -O bolumsonu.tar`

4. bolumsonu içeriğini bolumsonu2 adlı dosyaya yönlendir. _(sudo yetkisi olmadan yönlendirme gerçekleşmeli)_
`sudo chmod 700 bolumsonu`
`sudo chmod 700 bolumsonu2`
`cat bolumsonu >> bolumsonu2`

5. Terminal üzerinden **sahip** adında bir kullanıcı oluştur.
`sudo adduser sahip`

6. **sahip** adlı kullanıcıyı **_ikincigrup_**'**_a_** ekle
`sudo usermod  -aG ikincigrup sahip`
7. Oturum açtığın **kullanıcını _ilkgrup 'a_** ekle
`sudo usermod -aG ilkgrup didem`

8. bolumsonu adlı dosyanın sahibi oturum açtığın **kullanıcın**, grup sahipliği **_ilkgrup_** olsun
`sudo chown :ilkgrup bolumsonu`

9. bolumsonu2 adlı dosyanın sahibi **sahip** adlı kullanıcı, grup sahipliği ise **_ikincigrup_** olsun.
`sudo chown sahip:ikincigrup bolumsonu2`

10.  bolumsonu adlı dosyanın içeriğini bolumsonu2 adlı dosyaya yönlendir_.(Sudo yetkisi olmadan gerçekleşmeli + Other grubuna yetki vermeden.)
`cat bolumsonu >> bolumsonu2`

**11-Grupları ve kullanıcıları sistemden temizle**
`sudo deluser sahip`
`sudo delgroup ilkgrup`

# Dördüncü Problemlerimiz

- Sistemde çalışan **süreçleri** görüntüle.
`ps aux`
- **_Gedit_** programını çalıştıralım ve **PID** değerini görüntüle.
`gedit &`
`ps aux | grep gedit`

- Sadece _root_ kullanıcısına ait **süreçleri** görüntüle.
`ps -U root -u root u`

- **_Gedit_** programının **sürecini** sonlandır.
`pkill gedit`

- **_Gedit_** programını tekrar çalıştıralım, **PID** değerini bul ve süreci **arkaplanda** çalıştır.
`gedit &`
`pgrep gedit`
CTRL+Z
bg 
fg 

- **Arkaplandaki** süreçleri görüntüle.
`jobs -l`

- Sistemde çalışan **_servisleri_** görüntüle.
`systemctl list-units --type=service --status=running`

- User servislerinin _lokasyonunu_ görüntüle.
`systemctl --user show-environment`

- _Arayüz servisimizi kapat ve yeniden başlat._
`sudo systemctl stop display-manager`
