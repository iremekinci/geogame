# 🗺️ GeoGuessr: Türkiye İl Tahmini (Web GIS Projesi)

Bu proje, GMT 458 - Web GIS dersi kapsamında geliştirilmiş bir GeoGame'dir. Oyuncunun hedefi, sınırlı can ve süre kısıtlaması altında coğrafi ve mekansal ilişkileri kullanarak gizli Türkiye ilini bulmaktır.

***

### 🎯 Proje Amaçları ve Kritik Bileşenler

| Component | Requirement Fulfillment | Description |
| :--- | :--- | :--- |
| **Geo-Component** | Province-based GeoJSON Data | Türkiye il sınırları kullanılarak mekansal veri tabanı oluşturulmuştur. Tahminler harita üzerinde renklendirilir. |
| **Temporal & High-Score** | Yes (60 saniye süre limiti) | Oyun, 60 saniyelik zaman kısıtlaması içerir. Local Storage ile kalıcı skor takibi sağlanır. |
| **Advanced Visualization** | Consistent Red-to-Green Color Scale | Uzaklığa dayalı **ters** renk skalası kullanılır. (Koyu Yeşil: En Yakın Risk / Kırmızı: En Uzak Risk) |
| **Interaction Stability** | Can Sistemi ve Skor Takibi | Oyun, Can/Tahmin hakkı kısıtlamasıyla oyuncunun etkileşimini yönetir. |

***

### II. Görsel Tasarım ve Kullanıcı Deneyimi (UX)

Oyun, harita etkileşimini ve geri bildirimi önceliklendiren, duyarlı (responsive) iki sütunlu bir düzene sahiptir.

#### A. Ön Uç (Frontend) Düzeni ve Yerleşim

| Bölge | Konum | İşlevsellik ve Estetik |
| :--- | :--- | :--- |
| **Harita** | Sol Taraf (Geniş Alan) | Leaflet ile iller çizilir. Harita, oyunun ana odağıdır ve tahminlere göre renk değiştirir. |
| **Kontrol Paneli** | Sağ Taraf (Sabit Genişlik) | Tüm kritik **UX** (Kullanıcı Adı, Skor Tablosu, İpucu, İstatistikler) elemanlarını barındırır. Mobil cihazlarda haritanın altına kaydırılır. |
| **Can Sayacı** | Harita Üzeri Sağ Üst | Kalan can, **büyük, kırmızı kalpler** (❤️) ile görselleştirilmiştir. Bu, anlık risk algısını artırır. |
| **Başlangıç Modalı** | Harita Üzeri Merkez | Oyun Kuralları, Can Kuralı ve Süre bilgisini oyun başlamadan önce sunar. |

#### B. Geri Bildirim ve İpucu Mekanizması

* **Renk Skalası:** Mesafenin azalması pozitif bir sinyal olarak algılanır; bu nedenle, yakınlık arttıkça renk **koyu yeşile** döner. Skala 7 farklı mesafeyi görsel olarak ayırır.
* **İlçe İpucu:** Tahmin kolaylığı sağlamak için gizli ilin **temsilci bir ilçesi** ipucu olarak verilir. Bu, sadece mesafeye değil, coğrafi bilgiye de dayalı bir zorluk katmanı ekler.

***

### III. Oynanış Senaryoları ve Kural Detayları

#### A. Oynanış Mekanizması

| Senaryo | Kural | Puanlama |
| :--- | :--- | :--- |
| **Zaman Kısıtlaması** | Süre 60 saniyedir. | Süre biterse oyuncu kaybeder. |
| **Can Sistemi Kuralı** | Başlangıçta **3 can** ile başlanır. Her **5 yanlış tahminde** 1 can kaybedilir. | Oyuncunun tahmin hakkı 15 ile kısıtlanmıştır (3 can x 5 tahmin). |
| **Yüksek Skor** | En az tahminde gizli ili bulmak. | Kazanma skoru (en az tahmin ve en hızlı süre) Local Storage'a kaydedilerek rekabet tablosu oluşturulur. |

#### B. Teknik Gereksinimler

* **Frontend Mimarisi:** HTML, CSS (Duyarlı Tasarım) ve JavaScript kullanılmıştır.
* **JS Kütüphanesi:** **Leaflet.js** harita görselleştirmesi için ana kütüphanedir.
* **Bonus Kriteri:** Proje, kalıcı skor takibi için **Local Storage** kullanmış ve can sistemi eklenerek karmaşıklık artırılmıştır.