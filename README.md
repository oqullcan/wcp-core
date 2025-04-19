# WCP (White Cat Protocol) - Çekirdek Protokol Kütüphanesi (`wcp-core`) 🐾

---

## Özet

Bu belge, `wcp-core` adlı Rust protokol kütüphanesinin geliştirme sürecini ve teknik hedeflerini özetlemektedir. Proje, dijital iletişimde kullanıcı **özerkliği**, mahremiyeti ve güvenliğini temelden ele alan, modern kriptografi ve proaktif gizlilik tekniklerine odaklanan bir altyapı oluşturmayı amaçlamaktadır. Geliştirme, "Beyaz Kedi"ye **ithafen** büyük bir titizlikle yürütülmektedir.

**Not:** Bu repository şu anda boştur. Kod tabanı ve detaylı dokümantasyon, proje belirli bir olgunluğa ulaştığında buraya yüklenecektir. Bu README, o zamana kadar projenin mevcut durumunu ve vizyonunu belgelemektedir.

---

## 1. Projenin Felsefesi ve Teknik Motivasyon

WCP-Core, mevcut iletişim sistemlerinin potansiyel zayıflıklarına ve gelişen tehditlere yanıt olarak, aşağıdaki temel ilkelerle geliştirilmektedir:

*   **🔒 Güvenlik Temeli:** Kanıtlanmış kriptografik modeller (Noise/Double Ratchet ilhamlı) ve yalnızca denetlenmiş, güvenilir Rust kütüphaneleri (`ring`, `libsodium-sys` vb.) kullanılır. **`#![forbid(unsafe_code)]`** katı bir şekilde uygulanmaktadır. Kuantum Sonrası Kriptografi (PQC) için **kriptografik çeviklik** altyapısı tasarlanmaktadır.
*   **📊 Proaktif Gizlilik:** Metadata'nın (paket boyutu, zamanlama vb.) hassasiyeti kabul edilerek, sızıntıları en aza indirmek için **protokol seviyesinde aktif mekanizmalar** (deterministik padding, zamanlama karartması) geliştirilmektedir.
*   **🛡️ Güvenli API ("Misuse Resistance"):** Geliştiricilerin kütüphaneyi kullanırken güvenlik hataları yapma olasılığını en aza indirecek bir API tasarımı hedeflenmektedir.
*   🌐 **Ağdan Bağımsızlık:** Farklı ağ taşıma protokolleri ve anonimlik ağları (Tor/I2P vb.) ile uyumluluk gözetilmektedir.
*   📖 **Açıklık Felsefesi:** Nihai hedef, tamamen açık kaynaklı (FOSS), şeffaf ve denetlenebilir bir kod tabanı sunmaktır.

## 2. Geliştirme İlerlemesi (Mevcut Durum: ~%60-70)

Şu ana kadar aşağıdaki temel bileşenler ve yetenekler büyük ölçüde tamamlanmış ve yerel olarak test edilmiştir:

*   **Çekirdek Kriptografik Akış:**
    *   Noise Protocol (`XX`) tabanlı el sıkışma mantığının ilk implementasyonu (X25519/Ed25519 ile).
    *   Double Ratchet prensiplerine dayalı güvenli oturum yönetimi (anahtar türetme, state yönetimi).
    *   Mesajlar için AEAD şifreleme (ChaCha20-Poly1305).
*   **Temel Protokol Yapısı:**
    *   Açıkça tanımlanmış bir durum makinesinin Rust tip sistemiyle desteklenen ilk uygulaması.
    *   Temel mesaj türleri için serileştirme/deserileştirme (`serde` + `bincode`).
*   **İlk Metadata Koruması:**
    *   Giden paketler için **deterministik padding** (belirli boyutlara tamamlama) mekanizması.
    *   Yapılandırılabilir **temel zamanlama karartması** fonksiyonelliği.
*   **API İskeleti:** Protokolü yönetmek için temel `async`/`await` tabanlı Rust API'ları oluşturulmuştur.

## 3. Kalan Çalışmalar ve Sonraki Adımlar

Projenin bu repository'ye yüklenmeye hazır hale gelmesi için öncelikli olarak aşağıdaki adımlar üzerinde çalışılmaktadır:

*   **Kapsamlı Test Süitleri:** Mevcut kod için **Unit ve Entegrasyon testlerinin** önemli ölçüde artırılması. **Fuzzing** ve **Property-Based Testing** altyapısının kurulması.
*   **API Olgunlaştırma:** Mevcut API'nin **stabilize edilmesi**, ergonomisinin iyileştirilmesi ve "misuse-resistance" hedefine yönelik güçlendirilmesi.
*   **Protokol Detaylarının Netleştirilmesi:** Kriptografik çeviklik, gelişmiş metadata teknikleri ve PQC entegrasyon stratejileri gibi konularda tasarımın son haline getirilmesi.
*   **Performans Analizi ve Optimizasyon:** İlk performans profilleme ve darboğaz analizleri.
*   **Temel Dokümantasyon:** API referansı (`rustdoc`) ve protokolün ana hatlarını açıklayan bir spesifikasyon taslağının hazırlanması.
*   **Kod İnceleme ve Refactoring:** Mevcut kod tabanının temizlenmesi ve iyileştirilmesi.

## 4. ⚠️ Önemli Uyarılar (Mevcut Durum İçin) ⚠️

*   **Kod Henüz Yayınlanmadı:** Bu repository şu anda yer tutucudur. Gerçek kod ve detaylı dokümantasyon geliştirme tamamlandıkça yüklenecektir.
*   **Deneysel Çalışma:** Tamamlandığında ve yayınlandığında bile, proje başlangıçta **deneysel** kabul edilecektir.
*   **Güvenlik Garantisi Yok:** Kapsamlı bağımsız güvenlik denetimi yapılana kadar **güvenlik açısından garanti verilmemektedir.**
*   **Üretim İçin Değil:** Proje şu anki veya ilk yayınlanacak haliyle **üretim ortamları için uygun olmayacaktır.**

## 5. Lisans

<p style="font-size: 90%;">
<a href="LICENSE-APACHE">Apache Lisansı 2.0</a> VEYA 
<a href="LICENSE-MIT">MIT Lisansı</a> altında çift lisanslıdır.
</p>

---

*WCP-Core: Güvenli ve özel iletişim için devam eden, özenle yürütülen bir geliştirme süreci. Kod tabanı yakında bu alanda yerini alacak.*
