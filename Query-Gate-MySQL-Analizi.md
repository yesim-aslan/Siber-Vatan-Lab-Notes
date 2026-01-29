 # 🕵️‍♀️ Query Gate: MySQL Misconfiguration & Network Reconnaissance

**Platform:** Siber Vatan Laboratuvarı  
**Kategori:** Network Security / Database Exploitation  
**Durum:** ✅ Tamamlandı

## 🎯 Senaryo ve Zorluk (The Challenge)
Bu laboratuvarın amacı, hedef sistemdeki güvenlik açığını tespit edip gizli bilgiye (White Hat Hacker ismine) ulaşmaktı. Başlangıçta hedef makinede hangi servisin çalıştığını ve veritabanı ile nasıl iletişim kurulacağını (SQL Syntax) bilmiyordum.

## 🛠️  Keşif Aşaması (Reconnaissance)
Hedef makineyi (172.20.x.x) analiz etmek için **Nmap** aracıyla port taraması gerçekleştirdim.

```bash
nmap 172.20.7.45
# Sonuç: 3306/tcp OPEN (MySQL)
```
Analiz: Tarama sonucunda 3306 portunun açık olduğunu ve MySQL veritabanı servisinin çalıştığını tespit ettim. Veritabanı portunun dış ağa açık olması, kritik bir Güvenlik Yapılandırma Hatasıdır (Security Misconfiguration).

🧠 Matematiksel Yaklaşım: İlişkisel Cebir (Relational Algebra)
Bir Matematik bölümü öğrencisi olarak, SQL dilini ezberlemek yerine, bu dilin temelini oluşturan İlişkisel Cebir (Relational Algebra) ve Kümeler Teorisi mantığını inceledim. Veritabanı yapısını şu şekilde modelledim:
Evrensel Küme ($E$)  : Veritabanı Sunucusu (Tüm verilerin tutulduğu alan).
Alt Kümeler ($A, B \subset E$) : Tablolar (Tables). Veriler satır ve sütun matrisleri şeklinde tutulur.
 Fonksiyonlar ($f(x)$): Sorgular (Queries). SELECT komutu aslında bir filtreleme fonksiyonudur.
Bu bakış açısıyla komutların mantığını şu şekilde oturttum:
SHOW DATABASES $\rightarrow$ Evrensel kümedeki elemanları listele
USE database $\rightarrow$ İşlem yapılacak alt kümeyi seç.
SELECT * FROM table $\rightarrow$``` Matrisin tüm satır ve sütunlarını getir.
🔓 Sömürü ve Erişim (Exploitation)

Sisteme sızmak için en temel güvenlik ihlali olan "Varsayılan Kimlik Bilgileri" (Default Credentials) zafiyetini test ettim. root (yönetici) kullanıcısı ile şifresiz bağlanmayı denedim:
```mysql -u root -h 172.20.7.45`
`` 
Sonuç: Bağlantı başarılı! Sistem herhangi bir parola sormadan yönetici (root) yetkisi verdi. Bu, sistem yöneticisinin yaptığı kritik bir hatadır.
🕵️‍♀️Veri Çıkarma (Data Exfiltration)

Sisteme erişim sağladıktan sonra, SQL (İlişkisel Sorgu) komutlarını kullanarak gizli veriye adım adım ulaştım:
```,SHOW DATABASES;
-- Sonuç: 'detective_inspector' veritabanı tespit edildi.
```
Hedef Tabloyu Bulma:
```USE detective_inspector;
SHOW TABLES;
-- Sonuç: 'hacker_list' tablosu bulundu.
```
Veriyi Okuma (Matris Gösterimi):
SELECT * FROM hacker_list; 
 
Bu sorgu sonucunda tablodaki veriler listelendi ve "White-Hat" (Beyaz Şapkalı) hacker olan "Hackviser" kullanıcısının kimliği tespit edildi.
🚀 Kazanımlar (Key Takeaways)
Misconfiguration: En güçlü şifreleme algoritmaları bile kullanılsa, varsayılan (default) ayarların değiştirilmemesi sistemi savunmasız bırakır.
Analitik Düşünce: SQL Injection veya veritabanı sömürüsü, sadece kod bilmek değil; verinin nasıl modellendiğini (matematiksel yapısını) anlamaktır.
Keşif (Recon): Nmap taraması yapılmadan bir saldırı vektörü belirlenemez.
Yeşim Aslan | Matematik Öğrencisi & Siber Güvenlik Araştırmacısı
