# Bobrek-Tasi-Tespit-Sistemi
# Yapay Zeka Destekli Bilgisayarlı Tomografi Görüntülerinde Böbrek Taşı Teşhisi ve Milimetrik Boyut Analizi

Bu proje, Bilgisayarlı Tomografi (BT) kesit görüntülerinde otonom olarak böbrek taşı tespiti gerçekleştirmek ve tespit edilen patolojilerin milimetrik boyut analizini yapmak amacıyla geliştirilmiş tıbbi karar destek sistemi prototipidir. 

##  Proje Hakkında
Proje kapsamında en güncel nesne tespiti mimarileri karşılaştırmalı olarak analiz edilmiş, elde edilen en optimum model ağırlıkları hekimlerin kullanabileceği web tabanlı bir arayüze entegre edilmiştir.

* **Kullanılan Modeller:** YOLOv8, YOLOv9, YOLOv10 ve YOLOv11
* **Arayüz Teknolojisi:** Streamlit
* **Temel Dil ve Kütüphaneler:** Python, PyTorch, Ultralytics, OpenCV (cv2), NumPy, Pandas
* **Eğitim Ortamı:** Google Colab (GPU Destekli)

##  Deneysel Sonuçlar (50 Epok)
Eğitim süreçleri sonunda bağımsız test veri setinde elde edilen en optimum model metrikleri aşağıda sunulmuştur:

| Model Mimarisi | Precision (Keskinlik) | Recall (Duyarlılık) | mAP50 |
| :--- | :---: | :---: | :---: |
| **YOLOv8** | %74.2 | %66.1 | %71.3 |
| **YOLOv9 (Önerilen)** | **%76.8** | **%72.4** | **%74.1** |
| **YOLOv10** | %73.1 | %63.4 | %68.5 |
| **YOLOv11** | %78.4 | %70.2 | %75.2 |

> **Klinik Değerlendirme:** Tıbbi teşhiste yanlış negatif (hastalığı gözden kaçırma) oranını en aza indiren en kritik metrik **Recall (Duyarlılık)** değeridir. Bu doğrultuda **%72.4** başarı oranı sunan **YOLOv9** mimarisi sistemin merkezine entegre edilmiştir.

##  Temel Özellikler
* **Otonom Teşhis:** BT kesitleri üzerindeki böbrek taşları yüksek güven skoruyla tespit edilir ve sınır kutusu (bounding box) içerisine alınır.
* **Milimetrik Boyut Analizi:** Tespit edilen sınır kutularının piksel cinsinden boyutları, medikal görüntü kalibrasyon parametreleri kullanılarak programatik olarak gerçek hayattaki milimetrik (mm) boyutlarına dönüştürülür.
* **Klinik Karar Desteği:** Hesaplanan milimetrik boyutlar üzerinden 5 mm kritik eşiği analiz edilerek hastanın tedavi planlamasına (taşın kendiliğinden düşme olasılığı veya cerrahi müdahale ihtiyacı) katkı sağlanır.

##  Eğitilmiş Model Ağırlıkları
Proje kapsamında eğitilen en optimum model ağırlıklarına (`best_model.pt`) ve test çıktısı grafiklerine depo içerisinden ulaşabilirsiniz.

##  Kurulum ve Çalıştırma
Projeyi yerel bilgisayarınızda çalıştırmak için:

```bash
# Depoyu klonlayın
git clone [https://github.com/rabiaylmn4/Bobrek-Tasi-Teşhit-Sistemi-YOLOv8.git](https://github.com/rabiaylmn4/Bobrek-Tasi-Teşhit-Sistemi-YOLOv8.git)

# Gerekli kütüphaneleri yükleyin
pip install -r requirements.txt

# Streamlit arayüzünü başlatın
streamlit run app.py
