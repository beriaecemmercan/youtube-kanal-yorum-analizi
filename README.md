# youtube-kanal-yorum-analizi
YouTube yorumları üzerinden kanal başarısını değerlendiren duygu analizi projesi

# YouTube Kanal Yorum Analizi Projesi

# Proje Özeti

Bu projede, Python eğitimi veren 10 farklı YouTube kanalının en çok izlenen videolarına yapılan kullanıcı yorumları analiz edilmiştir.  
Amacımız, bu yorumlardan elde edilen **duygusal eğilimler (sentiment)** yoluyla her kanalın **kullanıcı algısına göre başarı düzeyini** ortaya koymaktır.

Yorumlar doğrudan bir "beğeni sayısı" gibi ölçülmeyen, fakat **kullanıcı deneyimini ve memnuniyetini en doğal haliyle yansıtan** değerli veri kaynaklarıdır.

# Kullanılan Yöntemler

# 1. Veri Toplama
- YouTube yorumları `youtube-comment-downloader` Python modülü ile video linklerinden web scraping yoluyla çekildi.
- Her kanal için en çok izlenen Python eğitimi videosunun yorumları alındı.
- Toplamda 45.000+ yorum analiz edildi.

# 2. Veri Ön İşleme
- URL, HTML tag, noktalama temizliği yapıldı.
- İngilizce olmayan yorumlar tespit edilip çıkarıldı (langdetect ile).
- Emoji içeren yorumlar **korundu** çünkü duygusal bilgi taşımaktaydı.
- Kısa ve anlamsız yorumlar (örneğin sadece "nice" gibi) filtrelendi.

# 3. Duygu Analizi
İki farklı yöntemle yorumlar otomatik olarak etiketlendi:

| Yöntem      | Açıklama |
|-------------|----------|
| **VADER**   | Rule-based, sözlük tabanlı analiz aracı. Her yoruma -1 (negatif) ile +1 (pozitif) arası **compound score** verir. |
| **TextBlob**| Polarity ve subjectivity değerlerine göre duygu sınıflandırması yapan lexicon-based yöntem. |

Her yorum şu etiketlerden biriyle sınıflandırıldı:
- `positive`
- `neutral`
- `negative`

---

# Sonuçların Karşılaştırılması

Her kanal için:
- Pozitif / Negatif / Nötr yorum oranları hesaplandı.
- Ortalama VADER ve TextBlob skoru çıkarıldı.
- En az 500 yorumu olan kanallar karşılaştırmaya dahil edildi.

# Spearman Korelasyonu:
- VADER ve TextBlob ortalama skor sıralamaları arasında korelasyon **1.0000** çıktı.  
→ Bu da iki yöntemin sıralamada **tam uyumlu** olduğunu gösteriyor.

# MAE (Ortalama Mutlak Fark):
- Yöntemler arası ortalama fark **0.1484**  
→ Skorlar benzer ama VADER genellikle daha yüksek pozitiflik atamış.

---

## 🥇 En Başarılı Kanallar (500+ yorumla)

| Sıra | Kanal             | Ortalama VADER Skoru |  Ortalama TextBlob Skoru  |
|------|------------------ |----------------------|---------------------------|
| 1    | CodeWithHarry     | 0.4614               | 0.2130                    |
| 2    | CSDOJO            | 0.3424               | 0.1795                    |
| 3    | BroCode           | 0.3047               | 0.1593                    |


# Görselleştirmeler

Projede aşağıdaki görsel analizler oluşturuldu:
- Bar chart: Pozitif / negatif yorum sayıları
- Radar chart: Yöntemler arası skor karşılaştırması
- Word Cloud: En sık geçen olumlu ve olumsuz kelimeler


# Dosya İçeriği

| Dosya Adı | Açıklama |
|-----------|----------|
| `proje_kodlari.ipynb` | Tüm veri işleme, analiz ve görselleştirme kodları |
| `with_textblob_sentiment.csv` | TextBlob ile etiketlenmiş yorumlar |
| `all_channels_with_sentiment.csv` | VADER ile etiketlenmiş tüm yorumlar |
| `sentiment_comparison_vader_vs_textblob.csv` | Ortalama skor karşılaştırmaları |
| `Zit_Etiketli_Yorumlar_Karsilastirma.xlsx` | Farklı etiketlenmiş yorum örnekleri |
| `grafikler/` | Radar, bar, wordcloud gibi görseller klasörü |


# Geliştiriciler
Bu proje, Eskişehir Teknik Üniversitesi'nde alınan **Veri Bilimine Giriş Dersi** kapsamında Beria Ecem Mercan ve Hasan Demirkoparan tarafından gerçekleştirilmiştir.
