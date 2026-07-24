# 🚀 RetailDork-AI: AI-Powered E-Commerce Intelligence Engine

[![Python Version](https://img.shields.io/badge/python-3.9%2B-blue?logo=python)](https://www.python.org/)
[![Playwright](https://img.shields.io/badge/playwright-automation-green?logo=googlechrome)](https://playwright.dev/)
[![Gemma 4](https://img.shields.io/badge/AI_Model-Gemma_4-purple?logo=google)](https://ai.google.dev/)
[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**RetailDork-AI**, modern e-ticaret sitelerinin karmaşık yapısını aşmak, gizli indirimleri tespit etmek ve çoklu platformlardan (Akakçe, Cimri vb.) veri çekerek **Gemma 4** yapay zeka modeli ile analiz eden profesyonel bir fiyat karşılaştırma ve veri analizi aracıdır.

---

## 🏗️ Teknik Mimari & Teknoloji Yığını

RetailDork-AI, sadece basit bir "scraper" değil; gelişmiş otomasyon ve doğal dil işleme (NLP) tekniklerini birleştiren bir motor üzerine inşa edilmiştir:

### 1. Veri Kazıma Katmanı (Scraping Layer)
*   **Playwright Engine:** Dinamik içerikleri render etmek, JavaScript tabanlı siteleri (React/Next.js vb.) taramak ve bot korumalarını aşmak için tercih edildi.
*   **Google Dorking Strategy:** Sadece standart arama sonuçlarını değil, belirli parametreleri (`site:`, `inurl:`, `intitle:` gibi) kullanarak hedef platformlardaki derin linkleri otomatik olarak filtreler.

### 2. Veri İşleme ve Temizleme (Data Processing)
*   **Regex & NLP:** Ham metinden fiyatları ayıklarken, para birimi sembollerini temizler ve sayısal doğrulamalar yapar.
*   **De-duplication:** Farklı satıcılardan gelen mükerrer ilanları otomatik olarak tespit eder ve tekilleştirir.

### 3. Yapay Zeka Analiz Katmanı (AI Insight)
*   **Gemma 4 Integration:** Toplanan veriler **Gemma 4** modeline beslenir. Model şu görevleri üstlenir:
    *   Fiyat/Performans oranlarını hesaplama.
    *   Ürün açıklamalarındaki "gizli" özellikleri öne çıkarma.
    *   Satıcı güvenilirliği ve öneri metinleri oluşturma.

---

## 🛠️ Kurulum ve Başlatma

### Sistem Gereksinimleri
- Python 3.9 veya üzeri
- Node.js (Playwright bağımlılıkları için)
- Ollama (Yerel Gemma 4 çalıştırımı için önerilir)

### Hızlı Kurulum Adımları
1. **Depoyu Klonlayın:**
   ```bash
   git clone https://github.com/omerfaruk-shp/RetailDork-AI.git
   cd RetailDork-AI
Bağımlılıkları Yükleyin:

python -m pip install --upgrade pip
pip install -r requirements.txt
Tarayıcı Motorlarını Hazırlayın:

playwright install chromium
Yerel AI Modelini Başlatın (Opsiyonel): Kullanıcıların kendi makinelerinde çalışması için Ollama kurulumu önerilir.

ollama pull gemma4:12b
📖 Kullanım Kılavuzu
Programı çalıştırmak ve analiz süreci başlatmak için şu adımları izleyin:

Terminal Üzerinden Çalıştırma
python retaildork.py
Uygulama Akışı (Workflow)
Hedef Girişi: Program çalıştığında sizden bir ürün adı veya anahtar kelime ister (Örn: "Logitech G Pro X Superlight").
Dorking Aşaması: Sistem, Google ve partner platformlarda özel "dork" sorguları gönderir.
Derin Tarama: Playwrighter'lar belirlenen linklere girer, sayfa içeriğini indirler ve dinamik elementleri işler.
AI İşleme: Toplanan ham veri temizlenir ve Gemma 4 modeline gönderilir. Model, veriyi şu formatta analiz eder:
En Uygun Seçenek
Fiyat Trendi Analizi
Satıcı Farklılıkları
Raporlama: İşlem bittiğinde outputs/ klasörü altına otomatik olarak bir .xlsx dosyası üretilir.
📁 Proje Dosya Yapısı
RetailDork-AI/
├── install.sh             
└── retaildork.py   
