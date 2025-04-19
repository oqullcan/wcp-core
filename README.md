# WCP (White Cat Protocol) - Çekirdek Protokol Kütüphanesi (wcp-core) 🐾

**Özet**

Bu belge, `wcp-core` adlı Rust protokol kütüphanesinin geliştirme vizyonunu, felsefesini ve teknik hedeflerini özetlemektedir. Proje, dijital iletişimde kullanıcı özerkliği, mahremiyeti ve güvenliğini temelden ele alan, modern kriptografi, proaktif gizlilik teknikleri ve kuantum sonrası kriptografiye hazırlık gibi konulara odaklanan bir altyapı oluşturmayı amaçlamaktadır. Geliştirme, ismini aldığı "**Beyaz Kedi**"ye ithafen büyük bir titizlikle yürütülmektedir.

**Not:** Bu repository şu anda **boştur**. Kod tabanı, detaylı spesifikasyonlar ve API dokümantasyonu, proje belirli bir olgunluğa ulaştığında ve ilk dahili incelemeler tamamlandığında buraya yüklenecektir. Bu README, o zamana kadar projenin vizyonunu, mevcut ilerlemesini ve gelecek planlarını belgelemektedir. Amacımız, kod yayınlanmadan önce bile şeffaf bir geliştirme süreci sunmaktır.

---

## 1. Projenin Felsefesi ve Teknik Motivasyon

WCP-Core, mevcut iletişim sistemlerinin potansiyel zayıflıklarına ve gelişen tehditlere yanıt olarak, aşağıdaki temel ilkelerle geliştirilmektedir:

*   🔒 **Güvenlik Temeli:**
    *   **Kanıtlanmış Modellerden İlham:** Temelde Noise Protocol Framework (özellikle XX benzeri el sıkışma akışları hedeflenerek) ve Double Ratchet Algoritması gibi endüstri standardı, kanıtlanmış kriptografik modellerin kavramlarından yararlanılır.
    *   **Güvenilir Kütüphaneler:** Yalnızca denetlenmiş, topluluk tarafından güvenilen Rust kriptografi kütüphaneleri (`ring` gibi) ve gerektiğinde belirli algoritmalar için dikkatle yönetilen FFI bağlamaları (`libsodium-sys` gibi, `unsafe` blokları sıkı bir şekilde izole edilerek) kullanılır.
    *   **Bellek Güvenliği:** Rust'ın sağladığı bellek güvenliği garantilerinden tam olarak faydalanılır ve `#![forbid(unsafe_code)]` kuralı projenin kendi yazdığı kodlar için katı bir şekilde uygulanır.
    *   **Kuantum Sonrası Hazırlık:** Kuantum Sonrası Kriptografi (PQC) algoritmalarının entegrasyonunu kolaylaştırmak için tasarımsal düzeyde kriptografik çeviklik (crypto-agility) altyapısı planlanmaktadır. Bu, gelecekteki algoritma geçişlerini ve potansiyel hibrit (klasik + PQC) modları desteklemeyi hedefler.

*   📊 **Proaktif Gizlilik (Metadata Koruması):**
    *   Metadata'nın (paket boyutu, zamanlama, iletişim örüntüleri vb.) hassasiyetini kabul ederek, sızıntıları en aza indirmek için protokol seviyesinde aktif mekanizmalar hedeflenmektedir.
    *   İlk odak noktaları arasında giden trafik için **deterministik padding** (örn. paket boyutlarını önceden belirlenmiş ayrık değerlere yuvarlama) ve yapılandırılabilir **zamanlama karartması** (timing obfuscation) gibi teknikler bulunmaktadır (bu mekanizmaların spesifik detayları ve ödünleşimleri aktif geliştirme altındadır).

*   🛡️ **Güvenli API ("Misuse Resistance"):**
    *   Kütüphaneyi kullanan geliştiricilerin istemeden güvenlik hataları yapma olasılığını en aza indirecek bir API tasarımı kritik bir hedeftir.
    *   Bunun için Rust'ın güçlü tip sistemi, durum makinelerini modelleme, builder pattern kullanımı ve API çağrılarının mantıksal sıralamasını zorunlu kılma gibi tekniklerden faydalanılması planlanmaktadır.

*   🌐 **Ağdan Bağımsızlık:**
    *   Çekirdek protokol mantığı, alttaki ağ taşıma katmanından (TCP, UDP, WebSockets vb.) ve potansiyel anonimlik katmanlarından (Tor, I2P vb.) bağımsız olacak şekilde tasarlanmaktadır.

*   📖 **Açıklık ve Denetlenebilirlik Felsefesi:**
    *   Nihai hedef, tamamen açık kaynaklı (FOSS - Apache 2.0 VEYA MIT Lisansı altında), şeffaf ve bağımsız denetimlere açık bir kod tabanı sunmaktır. Kod yayınlandıktan sonra topluluk incelemesi teşvik edilecektir.

---

## 2. Geliştirme İlerlemesi (Mevcut Tahmini Durum: ~%60-70)

Şu ana kadar aşağıdaki temel bileşenler ve yetenekler büyük ölçüde tamamlanmış ve yerel olarak test edilmiştir (ancak henüz yayınlanmamıştır):

*   **Çekirdek Kriptografik Akış:**
    *   Noise Protocol Framework konseptlerine dayalı (şu anda X25519/Ed25519 kullanan XX örüntüsü temel alınarak) el sıkışma mantığının ilk implementasyonu.
    *   Double Ratchet prensiplerinden ilham alan güvenli oturum yönetimi (anahtar türetme, durum yönetimi, mesaj numaralandırma).
    *   Mesajlar için AEAD şifreleme (şu anda ChaCha20-Poly1305).
*   **Temel Protokol Yapısı:**
    *   Protokolün ana durumlarını ve geçişlerini modelleyen, Rust'ın tip sistemiyle desteklenmesi hedeflenen bir durum makinesinin ilk uygulaması.
    *   Temel mesaj türleri için serileştirme/deserileştirme (şu anda `serde` + `bincode`).
*   **İlk Metadata Koruması:**
    *   Giden paketler için temel deterministik padding mekanizması.
    *   Yapılandırılabilir temel zamanlama karartması için ilk fonksiyonellik iskeleti.
*   **API İskeleti:**
    *   Protokolün temel yaşam döngüsünü (başlatma, mesaj gönderme/alma, sonlandırma) yönetmek için temel `async/await` tabanlı Rust API fonksiyonları oluşturulmuştur.

---

## 3. Kalan Çalışmalar ve Sonraki Adımlar (Yayın Öncesi Öncelikler)

Projenin bu repository'ye kod ve detaylı dokümantasyon ile yüklenmeye hazır hale gelmesi için öncelikli olarak aşağıdaki adımlar üzerinde yoğunlaşılmaktadır:

*   **Protokol Spesifikasyonu ve Detaylandırma:** Protokolün tüm yönlerini (durum makinesi, mesaj formatları, kriptografik operasyonlar, hata kodları, güvenlik varsayımları vb.) kapsayan resmi bir spesifikasyon dokümanının hazırlanması ve netleştirilmesi. "Noise/DR ilhamlı" olmanın ötesinde kesin tanımlar yapılması.
*   **Kapsamlı Test Süitleri:** Mevcut kod için Unit ve Entegrasyon testlerinin önemli ölçüde artırılması. Kriptografik işlemler, durum geçişleri, eş zamanlılık ve uç durumlar için sağlam Fuzzing (`cargo-fuzz` vb.) ve Property-Based Testing (`proptest` vb.) altyapısının kurulması. Bilinen protokol saldırı sınıflarına karşı test vektörlerinin geliştirilmesi.
*   **API Olgunlaştırma ve Misuse Resistance:** Mevcut API'nin stabilize edilmesi, ergonomisinin iyileştirilmesi ve özellikle "misuse-resistance" hedefine yönelik (tip durumları, zorunlu adımlar vb. ile) güçlendirilmesi. Geliştirici deneyiminin iyileştirilmesi.
*   **Gelişmiş Tasarım Kararlarının Sonuçlandırılması:** Kriptografik çeviklik mekanizmasının (PQC entegrasyonu, anlaşma protokolü, potansiyel hibrit modlar) ve gelişmiş metadata koruma tekniklerinin (padding stratejileri, zamanlama karartma algoritmaları ve bunların performans/gizlilik ödünleşimleri) nihai tasarımlarının belirlenmesi.
*   **Performans Analizi ve Optimizasyon:** İlk performans profilleme çalışmaları ve potansiyel darboğazların tespiti. Güvenlik/gizlilik özelliklerinin pratik performansla dengelenmesi.
*   **Temel Dokümantasyon:** Kapsamlı API referansı (`rustdoc`) ve protokolün ana hatlarını, kullanımını açıklayan kılavuz doküman taslaklarının hazırlanması.
*   **Kod İnceleme ve Refactoring:** Mevcut kod tabanının kapsamlı bir şekilde gözden geçirilmesi, temizlenmesi ve iyileştirilmesi.
*   **Güvenlik Denetimi Planlaması:** Kod tabanı belirli bir olgunluğa ulaştıktan sonra bağımsız güvenlik denetimleri için bir yol haritası oluşturulması (ilk yayınlar denetimsiz olacaktır).

---

## 4. ⚠️ Önemli Uyarılar (Mevcut Durum İçin) ⚠️

*   **Kod Henüz Yayınlanmadı:** Bu repository şu anda projenin vizyonunu ve ilerlemesini belgeleyen bir yer tutucudur. Gerçek kod ve detaylı dokümantasyon yukarıdaki adımlar tamamlandıkça yüklenecektir.
*   **Deneysel Çalışma:** Proje yayınlandığında bile, başlangıçta **deneysel** olarak kabul edilecektir. Geri bildirim toplamak ve tasarımı doğrulamak ana amaç olacaktır.
*   **Güvenlik Garantisi Yok:** Kapsamlı testler ve **bağımsız güvenlik denetimi** yapılana kadar protokolün veya implementasyonun güvenliği konusunda **hiçbir garanti verilmemektedir**.
*   **Üretim İçin Kesinlikle Uygun Değil:** Proje şu anki veya ilk yayınlanacak haliyle **üretim ortamlarında kullanılmamalıdır**. Ciddi güvenlik açıkları içerebilir.

---

## 5. Lisans

Yayınlanacak kod, geliştiricilere esneklik sağlamak amacıyla aşağıdaki lisanslardan biri (veya her ikisi) altında sunulacaktır:

*   Apache Lisansı, Sürüm 2.0 ([LICENSE-APACHE](LICENSE-APACHE) veya http://www.apache.org/licenses/LICENSE-2.0)
*   MIT Lisansı ([LICENSE-MIT](LICENSE-MIT) veya http://opensource.org/licenses/MIT)

Sizin tercihinize göre.

---

WCP-Core: Güvenli ve özel iletişim için iddialı hedefleri olan, özenle yürütülen ve devam eden bir geliştirme süreci. Kod tabanı ve detaylı dokümantasyon yakında bu alanda yerini alacak. Gelişmeler için takipte kalın!
