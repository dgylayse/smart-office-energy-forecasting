# Akıllı Ofis Enerji Planlama ve Tüketim Tahmini

**Python ve Jupyter Notebook ile günlük enerji tüketiminin tahmini, zaman serisi doğrulaması ve model hata analizi.**

Bu proje, [UCI Appliances Energy Prediction](https://archive.ics.uci.edu/dataset/374/appliances%2Benergy%2Bprediction) veri setindeki 10 dakikalık cihaz enerjisi, sıcaklık, nem ve aydınlatma ölçümlerini kullanarak **ertesi günün cihaz enerji tüketimini (kWh)** tahmin eder. Tüketim analizi, veri kalitesi değerlendirmesi, üç tahmin yaklaşımının karşılaştırılması ve tesis yöneticisine yönelik açıklayıcı raporlama içerir.

> **Kapsam notu:** Veri seti gerçek bir **konut** binasına aittir. “Akıllı ofis” projenin uygulama senaryosudur; model gerçek ofis verileri üzerinde doğrulanmamıştır. Sistem otomatik ekipman kontrolü yapmaz. AI agent, çalışır bir ürün olarak değil, raporda **gelecekteki geçiş planı** olarak ele alınmıştır.

## Öne çıkan sonuçlar

| Gösterge | Sonuç |
|---|---:|
| Ham ölçüm sayısı | 19.735 (10 dakikalık kayıt) |
| Geçerli tam gün | 136 |
| Modellemede kullanılan gün | 129 |
| Üretilen özellik | 20 |
| Eğitim / doğrulama / test | 90 / 19 / 20 gün |
| Seçilen model | Ridge Regression (α=100) |
| Final test MAE | **3,842 kWh** |
| Final test RMSE | **4,589 kWh** |
| Final test WAPE | **%28,08** |
| Naive baseline'a göre MAE iyileşmesi | **%8,54** |
| Naive baseline'a göre RMSE iyileşmesi | **%23,08** |

**Değerlendirme:** Ridge modeli, doğrulama döneminde Naive Baseline'dan daha düşük MAE üretemese de daha düşük RMSE ve yüksek tüketimli günlerde daha düşük hata nedeniyle seçilmiştir. Seçimden sonra 7–26 Mayıs 2016 dönemindeki 20 günlük final testte baseline'a göre iyileşme sağlamıştır. Buna karşın özellikle yüksek tüketimli günlerde düşük tahmin hataları devam ettiği için kritik işletme kararları insan kontrolü gerektirir.

## Yöntem

- 10 dakikalık `Appliances` ölçümlerinin günlük toplamını alıp Wh değerlerini kWh'ye dönüştürme
- Ölçüm kapsamı %100 olmayan ilk ve son günü çıkarma; eksik günleri sıfırla doldurmama
- Takvim, geçmiş tüketim (`lag_1`, `lag_7`, hareketli ortalamalar) ve **bir önceki güne ait** hava/aydınlatma özelliklerini üretme
- Verileri rastgele karıştırmadan kronolojik olarak eğitim, doğrulama ve final test dönemlerine ayırma
- Naive Baseline, Ridge Regression ve Random Forest karşılaştırması; Ridge için sınırlı hiperparametre araması
- MAE, RMSE, WAPE, yüksek/düşük tüketim analizi, özellik katsayıları ve dört günlük vaka incelemesi

## Dosya yapısı

```text
smart-office-energy-forecasting/
├── README.md
├── requirements.txt
├── .gitignore
├── Enerji_Tahmin_Analizi.ipynb
├── energydata_complete.csv
├── rapor/
│   └── Akilli_Ofis_Enerji_Tahmin_Nihai_Rapor.pdf
└── rapor_ciktilari/
    ├── agent_gecis_plani.md
    ├── operasyonel_rapor.md
    ├── final_test_sonuclari.csv
    ├── model_karsilastirma.csv
    ├── ozellik_etkileri.csv
    ├── ozellik_grubu_karsilastirmasi.csv
    ├── ozellik_grubu_karsilastirmasi.png
    ├── gunluk_enerji_verileri.csv
    ├── vaka_analizi.csv
    ├── veri_sozlugu.csv
    ├── tarih_araliklari.csv
    └── teknik_bilgiler.txt
```

## Kurulum ve çalıştırma

**Önerilen ortam:** Windows, Python 3.11, Jupyter Notebook. Aşağıdaki komutları proje ana klasöründe çalıştırın.

```powershell
python -m venv .venv
.venv\Scripts\activate
python -m pip install -r requirements.txt
python -m notebook
```

Jupyter üzerinden `Enerji_Tahmin_Analizi.ipynb` dosyasını açın ve hücreleri **üstten alta** çalıştırın. Ham veri dosyası (`energydata_complete.csv`) Notebook ile **aynı klasörde** bulunmalıdır. İşlemler `rapor_ciktilari/` klasöründeki analiz tablolarını ve rapor metinlerini oluşturur.

Özgün deney ortamı: **Python 3.11.9**, pandas 3.1.1, NumPy 2.4.6, Matplotlib 3.11.2, seaborn 0.13.2, scikit-learn 1.9.1, Notebook 7.6.5. Kayıtlı hücre çıktıları ile yeni çalıştırmalardaki süreler ve görseller arasında küçük farklılıklar oluşabilir.

## Rapor

Ayrıntılı metodoloji, grafikler, veri sözlüğü, deney tablosu, hata analizi, operasyonel değerlendirme ve AI agent'a geçiş planı için [**17 sayfalık proje raporunu**](rapor/Akilli_Ofis_Enerji_Tahmin_Nihai_Rapor.pdf) inceleyebilirsiniz.

## Veri kaynağı ve atıf

- **Kaynak:** Candanedo, L. (2017). *Appliances Energy Prediction* [Dataset]. UCI Machine Learning Repository.
- **DOI:** https://doi.org/10.24432/C5VC8G
- **Kaynak sayfası:** https://archive.ics.uci.edu/dataset/374/appliances%2Benergy%2Bprediction
- **Veri lisansı:** [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Veri seti, kaynak gösterilerek yeniden dağıtılmaktadır.

**Sınırlılık:** Kaynak verinin konut binasından gelmesi ve yüksek tüketim dönemlerinde daha büyük hata oluşması nedeniyle proje, doğrulanmış bir üretim/ofis enerji yönetim ürünü değildir. Otomatik karar veya ekipman kontrolü gerçekleştirmez.
