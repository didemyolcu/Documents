# Zabbix Agent Kurulumu
Bu kurulum dökümanı **Rocky-9-Linux** makine üstünde yapılmıştır.

Diğer kurulumlar için : [Zabbix Agent](https://www.zabbix.com/download?zabbix=7.0&os_distribution=rocky_linux&os_version=9&components=agent_2&db=&ws=)
Zabbix Version : 7.0 LTS
OS Distribution : Rocky Linux 
OS Version : 9
Zabbix Component : Agent2
Database : ---
Web Server : ---

## **1. Zabbix Agent 2 Repo'larını Yükle.**
**1.1 Öncelikle EPEL var mı kontrol et.**
`sudo su`
`ls /etc/yum.repos.d/ | grep epel`
Çıktı epel.repo ise 
 `sudo nano /etc/yum.repos.d/epel.repo`
 [epel] bloğunun içine 
 `excludepkgs=zabbix*` ekle.
 **1.2 Zabbix depolarını kuralım.**
 `rpm -Uvh https://repo.zabbix.com/zabbix/7.0/rocky/9/x86_64/zabbix-release-latest-7.0.el9.noarch.rpm`
`dnf clean all`

## 2. Zabbix Agent 2'yi yükleyelim.
``dnf install zabbix-agent2``

## 3. Zabbix Agent 2 eklentilerini kuralım.
`dnf install zabbix-agent2-plugin-mongodb zabbix-agent2-plugin-mssql zabbix-agent2-plugin-postgresql`

## 4. Zabbix Agent 2'yi başlatalım.
`systemctl restart zabbix-agent2`
`systemctl enable zabbix-agent2`

 

