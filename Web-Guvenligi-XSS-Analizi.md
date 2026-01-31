

```markdown
# 🕸️ Web Güvenliği: Cross-Site Scripting (XSS) Analizi

**Platform:** Siber Vatan Laboratuvarları
**Kategori:** Web Application Security
**Konu:** XSS (Reflected, Stored, DOM)

## 🎯 1. XSS Nedir?
XSS (Cross-Site Scripting), saldırganın hedef web sitesine zararlı JavaScript kodları enjekte etmesiyle oluşan bir zafiyettir. Bu zafiyet sayesinde kullanıcıların oturum bilgileri (Cookies) çalınabilir veya tarayıcıları manipüle edilebilir.

## 🧠 2. Laboratuvar Çalışmalarım ve Analizler

### 🔹 A. Reflected XSS (Yansıyan)
Kullanıcıdan alınan girdinin, veritabanına kaydedilmeden **anında** ekrana yansıtıldığı durumlarda oluşur. Genellikle arama kutularında veya hata mesajlarında görülür.
* **Senaryo:** Arama kutusuna `<script>alert(1)</script>` yazdım ve sayfa yenilendiğinde pop-up açıldı.
* **Risk:** Genellikle oltalama (phishing) linkleri üzerinden kurbanlara gönderilir.

### 🔹 B. Stored XSS (Depolanan)
En tehlikeli XSS türüdür. Zararlı kod veritabanına **kalıcı olarak** kaydedilir.
* **Senaryo:** Bir "Yorum Yap" alanına zararlı script kodunu bıraktım.
* **Sonuç:** O sayfayı ziyaret eden **her kullanıcı** (yönetici dahil) bu kodu farkında olmadan çalıştırdı.

### 🔹 C. DOM-Based XSS
Sunucu taraflı değil, tamamen tarayıcıdaki (Client-side) JavaScript kodlarının hatalı işlenmesinden kaynaklanır. Sayfa kaynağı değişmez ama tarayıcıdaki DOM yapısı manipüle edilir.

## 🛠️ 3. Kullandığım Araçlar
* **Burp Suite:** İstekleri yakalamak ve payload denemeleri yapmak için (Repeater modülü).
* **Payload Lists:** Farklı filtreleri atlatmak için kullanılan XSS vektörleri.

## 🚀 4. Önleme Yöntemleri (Mitigation)
* **Input Validation:** Kullanıcıdan gelen veri mutlaka filtrelenmeli (Örn: özel karakterlerin engellenmesi).
* **Output Encoding:** Veri ekrana basılırken HTML Entity formatına (`&lt;` `&gt;`) dönüştürülmeli.
