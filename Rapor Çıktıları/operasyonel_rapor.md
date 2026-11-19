
# Tesis Yöneticisi İçin Operasyonel Değerlendirme

## Sistemin Amacı

Geliştirilen sistem, geçmiş cihaz enerji tüketimi,
takvim bilgileri ve geçmiş çevresel ölçümlerden
yararlanarak ertesi günün enerji tüketimini kWh
cinsinden tahmin etmektedir.

Model, otomatik ekipman kontrolü yapmaz ve
tesis yöneticisinin kararının yerine geçmez.

## Tahmin Performansı

7-26 Mayıs 2016 dönemindeki 20 günlük
bağımsız test sonuçları:

- Seçilen model: Ridge Regression (alpha=100)
- MAE: 3.842 kWh
- RMSE: 4.589 kWh
- WAPE: %28.08
- Ortalama işaretli hata: -1.317 kWh
- Baseline'a göre MAE iyileşmesi: %8.54
- Baseline'a göre RMSE iyileşmesi: %23.08

MAE, test dönemindeki günlük mutlak tahmin hatasının
ortalamasıdır. Tek tek günler için garanti edilen
bir hata sınırı değildir.

## Yüksek Tüketim Riski

Eğitim döneminin üst çeyrek eşiği
16.45 kWh olarak hesaplanmıştır.

Test döneminde yüksek tüketimli 3 günde modelin
ortalama mutlak hatası 7.695 kWh olmuştur.
Bu günlerde model tüketimi düşük tahmin etmiştir.

Tahmini tüketimin yüksek olması veya geçmiş
ölçümlerde olağandışı değişiklik bulunması
halinde tesis yöneticisi ek kontrol yapmalıdır.

## Tahminin Yayınlanmaması Gereken Durumlar

- Gerekli geçmiş günlük ölçümler eksikse
- Günlük 144 ölçüm koşulu sağlanmıyorsa
- Tekrarlı veya güvenilmez zaman kayıtları varsa
- Kritik sensör değerleri fiziksel olarak şüpheliyse
- Modelin uygulanacağı bina, eğitim verisindeki
  koşullardan önemli ölçüde farklıysa
- Veri toplama veya tahmin sürecinde teknik hata varsa

Bu koşullarda otomatik tahmin yayınlanmamalı,
veriler insan tarafından incelenmelidir.

## Modelin İzlenmesi

Tahminler yeni gerçek ölçümlerle karşılaştırılmalı;
MAE, RMSE ve yüksek tüketimli gün hataları
düzenli olarak izlenmelidir.

Başlangıçta aylık performans incelemesi önerilir.
Veri dağılımı veya hata düzeyi belirgin değişirse
model yeniden değerlendirilmelidir.

## Operasyonel Sınırlılıklar

Kaynak veri bir konut binasından toplanmıştır.
Bu nedenle modelin ofis ortamındaki başarısı
ayrıca gerçek ofis verileriyle doğrulanmalıdır.

Modelin mevcut hata düzeyi, kritik enerji
planlamasında tek başına kullanılmasına uygun
olduğunu göstermemektedir.
