🌠 Göktaşı Zaman Serisi Tahmini & ARIMA Analizi
1. Veri Hazırlama ve Ön İşleme 📦🔎
Kodda ilk olarak meteorite-landings.csv dosyası okunuyor.

Yıl sütunu sayıya çevriliyor, eksik veya hatalı yıllar atılıyor.

Sadece 1900 sonrası ve “Fell” (düşen) olarak kaydedilmiş meteorlar filtreleniyor.

Sonuçta, her yıl kaç göktaşı düştüğü yıllık olarak hesaplanıp bir zaman serisine dönüştürülüyor.

Neden önemli?
ARIMA gibi zaman serisi modelleri, düzenli aralıklı ve düzgün ön işlenmiş verilere ihtiyaç duyar. Eksik ya da düzensiz veri ciddi tahmin hatalarına yol açar. ⚠️

2. Durağanlık Testi (ADF Testi) 🧪
adfuller testiyle serinin durağan olup olmadığına bakılıyor.

Durağanlık demek, serinin ortalaması ve varyansının zaman içinde sabit kalmasıdır.
ARIMA modelleri, sadece durağan serilerle sağlıklı çalışır.
Eğer seri durağan değilse, birinci fark (difference) alınıp tekrar deneniyor.

Neden önemli?
Göktaşı düşüş sayısı gibi doğal olaylar çoğunlukla durağan değildir. Her yıl ani dalgalanmalar olabilir. Fark alarak seriyi durağanlaştırmak gerekebilir, ancak bu da bazen bilgi kaybı yaratır. ℹ️

3. Model Kurulumu ve Tahmin 🔢🔮
ARIMA(1,1,1) modeli kuruluyor.

Parametreler rastgele veya ön araştırma ile seçilmiş olabilir, ancak asıl amaç basit bir zaman serisi tahmini yapmak.

Model tüm (train/test ayrımı olmadan) yıllar üstünden eğitilip, son yıldan 2025’e kadar (veya 5 yıl ileri) tahmin üretiyor.

Tahminler gerçek ve tahmini yıllar birleştirilerek grafik üzerinde gösteriliyor.
Ayrıca, get_forecast() fonksiyonuyla güven aralığı (%95) da çiziliyor.

Neden önemli?
ARIMA, geçmiş veriye bakıp “trend” ve “pattern” yakalasa da, göktaşı düşüşü gibi “random” olaylarda patinaj çeker.
Model trend yakalayamazsa (örneğin, veri aşırı dalgalı ve noise yoğunsa) tahminler dümdüz veya mantıksız olabilir.

Güven aralığı geniş çıkarsa, bu modelin gelecekteki tahmini konusunda çok da emin olmadığı anlamına gelir. 🤔

4. Modelin Sınırları ve Tahminin Tutarsızlığı 🚧
Neden tahminler çok tutarlı değil veya “kötü” görünüyor?

Veri Doğası:
Göktaşı düşüşü yıldan yıla çok değişken, çoğu zaman “random noise” içeriyor.
Gerçekten trend/örüntü yoksa, ARIMA gibi istatistiksel modeller abuk sabuk “ortalama etrafında” sallamaya başlar.

Ani Dalgalanmalar:
Bazı yıllar ani artış/azalış (outlier) varsa, model bu uç değerleri genelleyemez, hatalar büyür.

Veri Miktarı:
Özellikle yıllık veri sayısı az ise (örneğin, 120 yıl x yılda birkaç olay), model öğrenme için yetersiz kalır.

Mevsimsellik/Trend Yokluğu:
ARIMA mevsimsel, trendli veride daha iyi çalışır. Burada ise belirgin bir trend yok.

Model Seçimi:
SARIMA/ARIMA, özellikle finans, hava durumu, enerji talebi gibi daha düzenli serilerde kullanılır.
Doğal afet, göktaşı gibi olaylarda çoğunlukla “count model” veya başka istatistiksel yöntemler (Poisson, Negative Binomial vs.) tercih edilir.

5. Kodun Teknik Akışı ve Bloklar 🛠️
Veri Okuma ve Temizlik
CSV okunur, yıl ve “fall” filtrelenir.

Zaman Serisi Oluşturma
Her yıl için toplam göktaşı sayısı çıkarılır, zaman serisi haline getirilir.

Durağanlık Testi
ADF testi, gerekiyorsa fark alma.

Model Kurulumu ve Tahmin
ARIMA modeli fit edilir, ileri yıllar için tahmin ve güven aralığı üretilir.

Görselleştirme
Gerçek ve tahmini değerler çizilir, güven aralığı eklenir.

Raporlama
Son yıllar ve tahminler konsola basılır.

6. Özet ve Eleştirel Yorum 💬🔍
Kodun genel akışı doğru ve istatistiksel modelleme mantığına uygun.

Tahminlerin düşük doğruluğu modelin değil, verinin doğası ve uygun model seçiminin bir sonucu.

Projenin en önemli mesajı:
"Her zaman serisi modeli, her veri setinde iyi sonuç vermez.
Modelin tahmin başarısı, veri setinin doğasına ve uygun yöntem seçimine doğrudan bağlıdır."

ARIMA/SARIMA’nın burada kullanılmasının temel amacı, zaman serisi tahmin sürecini ve modelin sınırlarını göstermek.
Özellikle “random” olaylarda klasik modellerin limitlerini fark etmek ve açıklayabilmek mühendislik açısından kıymetli bir yaklaşımdır.

🎯 Sonuç Olarak:
Bu proje, ARIMA/SARIMA gibi zaman serisi modellerinin limitlerini ve doğru veri/model seçiminin önemini göstermektedir.
Göktaşı gibi az ve rastgele verilerde, tahminlerin güven aralığı geniş çıkar ve modelin isabeti düşer.
Bunu objektif şekilde göstermek de önemli bir sonuçtur. 🚀✨

Anahtar Kelimeler:
- ARIMA
- Zaman Serisi Analizi
- Time Series Forecasting
- Meteorite Landings
- Göktaşı Düşüşü
- Python
- pandas
- statsmodels
- Veri Ön İşleme
- Stationarity
- ADF Test
- Forecasting
- Outlier Detection
- Güven Aralığı (Confidence Interval)
- Model Sınırları
- Tahmin Hataları
- Data Science
- İstatistiksel Modelleme
- Random Events
- Signal Processing
- Veri Bilimi


