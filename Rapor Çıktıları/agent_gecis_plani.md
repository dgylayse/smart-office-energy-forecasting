
# Enerji Tahmin Sisteminden AI Agent Sistemine Geçiş

## 1. Agent Görevleri

Agent; yeni sensör verilerini düzenli toplama,
ölçüm kalitesini denetleme, günlük tüketimi
hesaplama, tahmin modelini çalıştırma ve
olağandışı tüketim değişikliklerini inceleme
görevlerini üstlenecektir.

Tahmin sonuçlarına ve geçmiş ölçümlere dayanarak
tesis yöneticisine gerekçeli uyarılar sunacaktır.

## 2. İnsan Onayı Gerektiren Kararlar

Enerji bütçesinin değiştirilmesi, cihazların
açılıp kapatılması, klima ve aydınlatma
ayarlarının değiştirilmesi gibi kritik işlemler
insan onayında kalacaktır.

Agent bu işlemleri kendiliğinden yapmayacaktır.

## 3. Veri Kaynakları ve Araçlar

Enerji sayaçları, sıcaklık ve nem sensörleri,
aydınlatma ölçümleri, takvim verileri ve
varsa güvenilir hava tahminleri kullanılacaktır.

Python, pandas, scikit-learn ve zamanlanmış
veri işleme görevleri temel yazılım araçlarıdır.

## 4. Tahmin Modelinin Rolü

Ridge Regression modeli, agent içindeki
tahmin bileşeni olarak görev yapacaktır.

Modelin çıktısı kesin karar değil, yardımcı
bir tüketim tahminidir. Anomali tespiti
ayrı kurallarla veya ayrıca doğrulanmış
bir anomali modeliyle gerçekleştirilecektir.

## 5. Veri Kalitesi ve Performans İzleme

Agent eksik ölçümleri, tekrarlı kayıtları,
beklenmeyen sensör değerlerini ve güncel
olmayan verileri izleyecektir.

Gerçek tüketim verileri geldikçe MAE,
RMSE ve yüksek tüketimli gün hataları
hesaplanacaktır. Veri dağılımındaki
değişimler ayrıca takip edilecektir.

## 6. Güvenlik Önlemleri

Yanlış önerileri azaltmak için veri
doğrulama, açıklanabilir sonuçlar,
yetkilendirme, işlem kayıtları ve insan
onayı mekanizmaları kullanılacaktır.

## 7. Öneri Üretilmemesi Gereken Durumlar

Eksik veya güvenilmez ölçümler, güncel
olmayan veri, kritik sensör arızası,
modelin geçerli kullanım alanı dışındaki
koşullar ya da ciddi performans bozulması
durumunda agent öneri üretmeyi durduracak
ve insan incelemesi isteyecektir.

## 8. Üretim Sistemine Geçiş

İlk aşamada mevcut Notebook modeli
tekrarlanabilir bir tahmin servisine
dönüştürülecektir.

İkinci aşamada veri toplama, kalite kontrolü,
izleme ve anomali uyarıları eklenecektir.

Üçüncü aşamada gerçek ofis verileriyle
pilot uygulama gerçekleştirilecektir.

Son aşamada güvenlik ve performans
testlerinden sonra kontrollü üretim
ortamına geçilecektir. Kritik kararların
insan onayında kalması korunacaktır.
