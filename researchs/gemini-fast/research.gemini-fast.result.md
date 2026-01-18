# Research Result for gemini-fast

# IoT Güvenlik Açıkları ve Hızlı Çözümler (Özet)

Gemini Fast modülü ile yapılan tarama sonucunda, ev tipi IoT cihazları için en kritik noktalar aşağıda özetlenmiştir.

## En Sık Rastlanan 3 Güvenlik Açığı

1.  **Varsayılan Şifreler (Default Passwords):**
    * Cihazların fabrika çıkışlı `admin/1234` gibi şifrelerle gelmesi ve kullanıcının bunu değiştirmemesi. Mirai gibi botnetlerin bir numaralı giriş kapısıdır.

2.  **Güncellenmeyen Yazılımlar (Outdated Firmware):**
    * Kullanıcıların cihaz güncellemelerini takip etmemesi sonucu, yıllar önce keşfedilmiş açıkların (exploit) hala aktif kalması.

3.  **Güvensiz Ağ İletişimi:**
    * Cihazların verileri şifrelemeden (HTTP veya Telnet üzerinden) açık metin olarak göndermesi. Ağ dinlendiğinde şifreler çalınabilir.

## En Hızlı 3 Çözüm Önerisi

1.  **Güçlü Parola Politikası:**
    * Cihazı kutudan çıkarır çıkarmaz varsayılan şifreyi en az 12 karakterli, karmaşık bir şifre ile değiştirin.

2.  **Otomatik Güncelleme:**
    * Mümkünse cihaz ayarlarından "Otomatik Güncelleme" seçeneğini aktif edin veya ayda bir mobil uygulamadan kontrol sağlayın.

3.  **Ağ Segmentasyonu (Misafir Ağı):**
    * Akıllı cihazları (süpürge, lamba vb.) modeminizdeki "Misafir Ağı"na (Guest Network) bağlayın. Böylece hacklenseler bile kişisel bilgisayarınıza erişemezler.
