# Research Result for gemini-pro

# IoT Cihazlarında Güvenlik Zafiyetleri ve Ağ Tabanlı Saldırı Tespit Sistemleri (IDS) Analizi

## 1. Giriş
Nesnelerin İnterneti (IoT) cihazlarının kullanımının artmasıyla birlikte, bu cihazların barındırdığı güvenlik zafiyetleri siber saldırganlar için geniş bir saldırı yüzeyi oluşturmuştur. Bu rapor, IoT cihazlarındaki yaygın açıkları ve ağ tabanlı tespit yöntemlerini inceler.

## 2. Yaygın IoT Güvenlik Zafiyetleri (OWASP IoT Top 10)
Yapılan araştırmalar ve OWASP verilerine göre en kritik zafiyetler şunlardır:

### 2.1. Zayıf, Tahmin Edilebilir veya Sert Kodlanmış Parolalar
Çoğu IoT cihazı (Robot süpürgeler, IP kameralar), üretici tarafından atanan `admin:admin`, `root:1234` gibi varsayılan şifrelerle gelir. Kullanıcıların bunları değiştirmemesi, cihazları Brute-Force saldırılarına açık hale getirir.

### 2.2. Güvensiz Ağ Servisleri
Cihazlar üzerinde gereksiz yere açık bırakılan Telnet (Port 23) ve SSH (Port 22) portları, saldırganların cihaza uzaktan erişim sağlamasına olanak tanır.

### 2.3. Şifreleme Eksikliği
Veri transferi sırasında (Data-in-transit) ve saklama sırasında (Data-at-rest) şifreleme kullanılmaması, Man-in-the-Middle (MitM) saldırılarıyla verilerin çalınmasına neden olur.

## 3. Saldırı Vektörü Analizi: Mirai Botnet Örneği
Mirai botneti, IoT cihazlarındaki zafiyetleri şu adımlarla sömürür:
1.  **Tarama (Scanning):** Rastgele IP adreslerine TCP SYN paketleri göndererek açık Telnet portlarını (23) tarar.
2.  **Kaba Kuvvet (Brute Force):** Açık port bulduğunda, önceden tanımlanmış 60 adet yaygın kullanıcı adı/şifre kombinasyonunu dener.
3.  **Enfeksiyon:** Giriş başarılı olursa, cihazın belleğine kötü amaçlı yazılımı indirir ve cihazı bir "Zombi"ye dönüştürür.
4.  **Komuta Kontrol (C2):** Cihaz, saldırganın C2 sunucusundan emir beklemeye başlar (Genellikle DDoS saldırısı için).

## 4. Raspberry Pi Tabanlı IDS/IPS Çözümleri
"IoT Shield" projesi kapsamında kullanılabilecek savunma mekanizmaları şunlardır:

### 4.1. Snort / Suricata Entegrasyonu
Raspberry Pi, ağ trafiğini dinleyen bir "köprü" (bridge) veya "gateway" olarak yapılandırılabilir.

* **İmza Tabanlı Tespit:** Bilinen saldırı kalıplarını yakalar.
    * *Örnek Snort Kuralı (Telnet Erişim Denemesi):*
        `alert tcp $EXTERNAL_NET any -> $HOME_NET 23 (msg:"TELNET connection attempt"; sid:1000001; rev:1;)`
* **Anomali Tabanlı Tespit:** Normal trafik dışındaki davranışları (örn. bir kameranın gece 03:00'te Çin'deki bir sunucuya yüksek boyutta veri göndermesi) tespit eder.

## 5. Sonuç
Ev ağlarının güvenliği için, uç noktada (modem arkasında) çalışan, imza ve anomali tabanlı analiz yapabilen donanımsal bir çözüm (IoT Shield), yazılım güncellemelerini yapamayan son kullanıcılar için en etkili savunma hattıdır.
