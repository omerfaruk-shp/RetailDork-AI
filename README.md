# 🚀 Ultimate Price & Link Scraper

Gelişmiş web kazıma (scraping) teknikleri ve yerel yapay zeka entegrasyonu ile e-ticaret platformları ve Google Shopping üzerinde otomatik ürün/fiyat araması yapan, sonuçları filtrelenmiş ve biçimlendirilmiş bir Excel dosyasına dönüştüren otomasyon sistemidir.

---

## ✨ Özellikler

* 🔍 **Çoklu Platform Taraması:** Akakçe, Cimri, Trendyol, Hepsiburada, Amazon TR, N11, PttAVM, Teknosa, Vatan Bilgisayar ve daha birçok platformda Google Dork altyapısı ile arama yapar.
* 🛒 **Google Shopping Akışı:** `udm=28` parametresiyle doğrudan Google Shopping sekmesinden güncel mağaza fiyatlarını toplar.
* 🧹 **Akıllı Gürültü Filtresi:** Sonuçlar arasındaki kılıf, yedek parça, ekran koruyucu veya 2. el / teşhir ürünlerini otomatik olarak eler.
* 📊 **Raporlanmış Excel Çıktısı:** En ucuzdan pahalıya sıralı, canlı ürün bağlantılarına sahip (`Tıkla & Git`), sütun genişlikleri ve renkleri ayarlanmış `.xlsx` dosyası üretir.
* 🧠 **Yerel Yapay Zeka (Ollama) Analizi:** Çekilen fiyat verilerini yerel LLM (`gemma4:12b` veya `gemma2:9b`) modeline göndererek mağazalar arası fiyat farkı ve F/P tavsiyesi sunan analiz raporu oluşturur.
* 🛡️ **Evrensel Kurulum:** macOS (Brew) ve tüm ana Linux dağıtımlarında (Ubuntu, Debian, Fedora, Arch, openSUSE) tüm bağımlılıkları tek tıkla kurar.

---

## 📂 Proje Yapısı

├── retaildork.py     

├── install.sh     

├── run.sh         

└── README.md      

---

## ⚡ Hızlı Kurulum

Tüm gereksinimleri (Python sanal ortamı, Playwright Chromium motoru, Ollama ve Yapay Zeka Modeli) otomatik yüklemek için terminalinizde aşağıdaki komutları çalıştırmanız yeterlidir:

chmod +x Install.sh
./Install.sh

---

## 🚀 Kullanım

Kurulum tamamlandıktan sonra projeyi başlatmak için tek yapmanız gereken:

./run.sh

1. Sistem sizden aratmak istediğiniz **Ürün / Model** adını isteyecektir (Örn: `Sony PlayStation 5 Slim 1TB`).
2. Tarayıcı (Chromium) otomatik açılacaktır. Ekranda bot doğrulaması (reCAPTCHA) çıkarsa çözüp terminale gelerek **ENTER** tuşuna basın.
3. Tarama bittiğinde proje dizinine `[urun_adi]_ucuz_fiyat_listesi.xlsx` dosyası kaydedilecek ve terminalde **Yerel AI Mağaza Analiz Raporu** görüntülenecektir.

---

## 🛠️ Alternatif / Manuel Çalıştırma

`run.sh` kullanmak istemiyorsanız sanal ortamı manuel aktifleştirip Python dosyanızı doğrudan çalıştırabilirsiniz:

# 1. Sanal ortamı aktif edin
source venv/bin/activate

# 2. Scraper kodunuzu çalıştırın
python scraper.py

---

## ⚙️ Teknolojik Bağlam & Gereksinimler

* **Python 3.9+**
* **Playwright** (Web otomasyonu ve tarayıcı yönlendirmeleri)
* **BeautifulSoup4** (HTML parse işlemleri)
* **Pandas & OpenPyXL** (Veri manipülasyonu ve Excel biçimlendirme)
* **Ollama & OpenAI Client** (Yerel yapay zeka modeli erişimi)
