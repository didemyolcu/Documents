# ZABBİX KURULUM DÖKÜMANI
Bu döküman **Ubuntu 24.04** makine üzerinde gerçekleştirilmiştir. 
Servis : Zabbix 7.0 LTS

## **1. Veritabanı Kurulumu**
**1.1 Sistemi güncelle**  
`sudo apt update && sudo apt upgrade `
**1.2_ PostgreSQL paketlerini kur.**  
`sudo apt install postgresql`
**1.3 PostgreSQL servisi çalışıyor mu kontrol et**  
`sudo systemctl status postgresql`
(Active: active (running) olmalı)  
  

## **2. Zabbix Kurulumu**
En güncel versiyonlar için : [Zabbix Kurulum ](https://www.zabbix.com/download?zabbix=7.0&os_distribution=ubuntu&os_version=24.04&components=server_frontend_agent_2&db=mysql&ws=apache)
**Zabbix Version :** 7.0 LTS
**OS Distribution :** Ubuntu
**OS Version :** 24.04 (Noble)
**Zabbix Component :** Server, Frontend, Agent 2
**Database :** PostgreSQL
**Web Server :** Apache

**2.1 Zabbix Deposunu Yükle**
`sudo su`
`wget https://repo.zabbix.com/zabbix/7.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_7.0+ubuntu24.04_all.deb `
`dpkg -i zabbix-release_latest_7.0+ubuntu24.04_all.deb`
`apt update`

**2.2 Zabbix Server, Frontend , Agent2 ‘ yi yükle**
`apt install zabbix-server-pgsql zabbix-frontend-php php8.3-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent2`
**2.3 Agent2 eklentilerini yükle**
`apt install zabbix-agent2-plugin-mongodb zabbix-agent2-plugin-mssql zabbix-agent2-plugin-postgresql`
**2.4 Database Oluştur**
`sudo -u postgres createuser --pwprompt zabbix `
`sudo -u postgres createdb -O zabbix zabbix`
`zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix`
**2.5 /etc/zabbix/zabbix_server.conf Dosyasını Düzenle**
`nano /etc/zabbix/zabbix_server.conf`
`DBPassword=password`

**2.5 Zabbix server’ı çalıştır**
`systemctl restart zabbix-server zabbix-agent2 apache2`
`systemctl enable zabbix-server zabbix-agent2 apache2`

## 3. Zabbix Arayüzü Aç
`http://host/zabbix`
Giriş Bilgileri
Username : Admin
Password : zabbix


