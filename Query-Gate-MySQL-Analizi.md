# 🕵️‍♀️ Query Gate: MySQL Misconfiguration & Network Reconnaissance

**Platform:** Siber Vatan Laboratuvarı  
**Kategori:** Network Security / Database Exploitation  
**Durum:** ✅ Tamamlandı

## 🎯 Senaryo ve Zorluk (The Challenge)
Bu laboratuvarın amacı, hedef sistemdeki güvenlik açığını tespit edip gizli bilgiye (White Hat Hacker ismine) ulaşmaktı. Başlangıçta hedef makinede hangi servisin çalıştığını ve veritabanı ile nasıl iletişim kurulacağını (SQL Syntax) bilmiyordum.

## 🛠️ Keşif Aşaması (Reconnaissance)
Hedef makineyi (172.20.x.x) analiz etmek için **Nmap** aracıyla port taraması gerçekleştirdim.

```bash
nmap 172.20.7.45
# Sonuç: 3306/tcp OPEN (MySQL)
Analiz: Tarama sonucunda 3306 portunun açık olduğunu ve MySQL veritabanı servisinin çalıştığını tespit ettim. Veritabanı portunun dış ağa açık olması, kritik bir Güvenlik Yapılandırma Hatasıdır (Security Misconfiguration).
