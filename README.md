# Energy-consumption-forecasting-based-on-hourly-data
![image](https://user-images.githubusercontent.com/64266044/235432661-3f700be0-a961-4ccf-9177-6130a5246710.png)

Merhaba.

Bu repository `Kaggle`'da katıldığım `Gdz Elektrik Datathon 2023 ` yarışması çözümümü içerir.Problemmimiz İzmir ve Manisa bölgesindeki  Gdz Elektrik sorumluluğundaki şebeke merkezlerine yönelik "enerji dağıtım" tahminlenmesi. Train verisi `2018-08-01` den `2022-07-31` kadar saatlik bazda bizden 2022 8. ayın saatlik olarak tahminlenmesi istenmektedir.Dikkate alacağımız değerlendirme metriği MAPE( Ortalama mutlak yüzde hatasını ölçer.Özellikle yüksek yüzde hataları olan ölçümler için hassas olabilir, bu da outlier'ları yanıltıcı bir şekilde vurgulayabilir.) 

#### Veri Görselleştirmeleri için [`data-firs-look.ipynp`](https://github.com/arukemre/Energy-consumption-based-on-hourly-data/blob/main/data-first-look.ipynb) bakabilirsiniz.

#### Veri ön işleme ve Feature engineering tarafında kullanılan fonksiyonlar [`modules.ipynp`](https://github.com/arukemre/Energy-consumption-based-on-hourly-data/blob/main/modules.ipynb) bakabilirsiniz.


>MAPE:

![image](https://user-images.githubusercontent.com/64266044/235359267-bc8e5138-5551-47f8-bfcc-6ef374b67b1c.png)

Probleme genel olarak modele zamansallığı nasıl daha iyi anlamasına yardımcı olurum şeklinde yaklaşıp bu doğrultuda feature lar yaratttım.İlk olarak `Tarih` feature'nu   `timeseries_features` fonksiyonu ile extract ederek.Zamansallıgı yakalayabilmesi için kategorik değişkenler oluşturdum.
Sonrasında Dış kaynaktan veriler import edildi bu verilere lag edilerek kullanildi.

### Kullanılan dış kaynak verileri:
* IZMIR için `get_meteostat_data` fonksiyonu ile hava durumu verileri çekildi.Shift edilerek lag feature lar oluşturuldu.
* Türkiyenin toplam enerji üretimi saatlik veri.Shift edilip öyle kullanildi.Lag feature oluşturuldu
* Türkiyenin toplam enerji tüketimi.Shift edilip öyle kullanildi.Lag feature oluşturuldu.
* [`wwo`](https://www.worldweatheronline.com/) sitesinden yine izmir için hava durumu verileri çekildi.Shift edilip öyle kullanildi.Lag feature oluşturuldu.

> Modelleme aşamasında `XGboost` kullandım.Modeli tune etmek için Optuna kütüphanesinden yararlandım.Olayın daha çok feature engineering tarafında döndüğüne inanan biri olarak farklı algoritmalar deneme zahmetine girmedim:)



