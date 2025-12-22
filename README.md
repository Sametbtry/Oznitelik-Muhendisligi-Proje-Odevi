# German Credit Risk - Öznitelik Mühendisliği Projesi

## 📋 Proje Hakkında

Bu proje, **Öznitelik Mühendisliği** dersi kapsamında hazırlanmış bir ödevdir. German Credit Data veri seti kullanılarak kredi risk analizi yapılmakta ve farklı öznitelik seçim yöntemlerinin model performansına etkisi incelenmektedir.

Proje, veri ön işlemeden model karşılaştırmasına kadar tüm makine öğrenmesi sürecini kapsamaktadır.

## 🎯 Proje Amacı

- Keşifsel Veri Analizi (EDA) ve veri ön işleme adımlarının uygulanması
- Üç farklı öznitelik seçim yönteminin (Filter, Wrapper, Embedded) karşılaştırılması
- Seçilen özniteliklerle eğitilen modellerin performanslarının değerlendirilmesi
- Öznitelik mühendisliğinin model performansına etkisinin analiz edilmesi

## 📂 Proje Yapısı

```
German Credit Risk - With Target/
│
├── data/
│   ├── raw/                          # Ham veri dosyaları
│   │   └── german_credit_data.csv    # Orijinal veri seti
│   │
│   └── processed/                    # İşlenmiş veri dosyaları
│       ├── X_train.csv               # Eğitim verisi (öznitelikler)
│       ├── X_test.csv                # Test verisi (öznitelikler)
│       ├── y_train.csv               # Eğitim verisi (hedef değişken)
│       └── y_test.csv                # Test verisi (hedef değişken)
│
├── notebooks/                        # Jupyter Notebook dosyaları
│   ├── EDA_and_Preprocessing.ipynb   # 1. Notebook: Veri analizi ve ön işleme
│   ├── Feature_Selection.ipynb       # 2. Notebook: Öznitelik seçimi
│   └── Model_Comparison.ipynb        # 3. Notebook: Model karşılaştırması
│
├── models/                           # Eğitilmiş model dosyaları
│
├── reports/                          # Raporlar ve görselleştirmeler
│   └── figures/                      # Grafikler ve şekiller
│       ├── EDA_and_Preprocessing/
│       ├── Feature_Selection/
│       └── Model_Comparison/
│
├── requirements.txt                  # Gerekli Python kütüphaneleri
└── README.md                         # Bu dosya
```

## 🚀 Kurulum ve Çalıştırma

### 1. Gerekli Kütüphanelerin Kurulumu

Projeyi çalıştırmadan önce gerekli Python kütüphanelerini yüklemeniz gerekmektedir. Terminal veya komut satırında aşağıdaki komutu çalıştırın:

```bash
pip install -r requirements.txt
```

Bu komut, `requirements.txt` dosyasında belirtilen tüm kütüphaneleri otomatik olarak yükleyecektir. İçerdiği temel kütüphaneler:
- **pandas**: Veri manipülasyonu
- **numpy**: Sayısal hesaplamalar
- **scikit-learn**: Makine öğrenmesi algoritmaları ve öznitelik seçimi
- **plotly**: İnteraktif görselleştirmeler
- **ipykernel**: Jupyter Notebook desteği

### 2. Notebook'ların Çalıştırılması

⚠️ **UYARI:** Notebook'lar aşağıda belirtilen sırada çalıştırılmalıdır. Her notebook bir öncekinin çıktılarını kullandığı için sıralama kritik öneme sahiptir.

---

#### 📝 Notebook 1: `EDA_and_Preprocessing.ipynb`
**Keşifsel Veri Analizi ve Ön İşleme**

**Amaç:** Ham veriyi analiz etmek, temizlemek ve makine öğrenmesi için hazır hale getirmek.

**Yapılan İşlemler:**
1. **Veri Yükleme ve Genel İnceleme**
   - Veri seti boyutu, veri tipleri ve istatistiksel özet çıkarma
   - İlk gözlemlere bakış

2. **Keşifsel Veri Analizi (EDA)**
   - Hedef değişken (Risk) dağılımının incelenmesi
   - Sayısal değişkenlerin (Age, Credit amount, Duration) dağılım analizi
   - Kategorik değişkenlerin (Sex, Job, Housing, Purpose) frekans analizi
   - Risk kategorilerine göre değişkenlerin karşılaştırmalı analizi

3. **Eksik Veri Yönetimi**
   - Eksik veri oranlarının belirlenmesi
   - Saving accounts ve Checking account değişkenlerindeki eksik verilerin incelenmesi
   - Eksik verilerin uygun şekilde kodlanması

4. **Veri Ön İşleme**
   - Kategorik değişkenlerin sayısal formata dönüştürülmesi (Ordinal Encoding)
   - Sayısal değişkenlerin ölçeklendirilmesi (Robust Scaler)
   - Hedef değişkenin ikili kodlama (Good=0, Bad=1)

5. **Veri Setinin Bölünmesi**
   - Train-Test split (%80 eğitim, %20 test)
   - Stratified sampling ile sınıf dengesinin korunması

**Girdiler:**
- `data/raw/german_credit_data.csv`

**Çıktılar:**
- `data/processed/X_train.csv` → Eğitim seti öznitelikleri
- `data/processed/X_test.csv` → Test seti öznitelikleri
- `data/processed/y_train.csv` → Eğitim seti hedef değişkeni
- `data/processed/y_test.csv` → Test seti hedef değişkeni
- `reports/figures/EDA_and_Preprocessing/` → Görselleştirmeler (histogram, box plot, bar chart)

---

#### 🎯 Notebook 2: `Feature_Selection.ipynb`
**Öznitelik Seçimi ve Karşılaştırma**

**Amaç:** Farklı öznitelik seçim yöntemlerini uygulamak ve en etkili öznitelikleri belirlemek.

**Yapılan İşlemler:**
1. **Filter Method - SelectKBest**
   - ANOVA F-test skorlarına dayalı öznitelik seçimi
   - k={5, 10, 15} için cross-validation ile performans karşılaştırması
   - En iyi k değerinin belirlenmesi
   - Seçilen özniteliklerin listelenmesi

2. **Wrapper Method - Recursive Feature Elimination (RFE)**
   - Logistic Regression modeli ile iteratif öznitelik elemesi
   - Farklı öznitelik sayıları için model performansının değerlendirilmesi
   - Optimal öznitelik sayısının belirlenmesi
   - RFE skorlarının görselleştirilmesi

3. **Embedded Method - Random Forest Feature Importance**
   - Random Forest algoritması ile öznitelik önem skorlarının hesaplanması
   - Önem eşik değerine göre öznitelik filtreleme
   - Feature importance grafiğinin oluşturulması
   - En önemli özniteliklerin sıralanması

4. **Yöntemlerin Karşılaştırılması**
   - Her yöntemle seçilen öznitelik sayılarının karşılaştırılması
   - Ortak ve farklı özniteliklerin analizi (Venn diagram)
   - Cross-validation AUC skorlarının karşılaştırılması

**Girdiler:**
- `data/processed/X_train.csv`
- `data/processed/X_test.csv`
- `data/processed/y_train.csv`
- `data/processed/y_test.csv`

**Çıktılar:**
- `data/processed/selected_features.pkl` → Pickle dosyası (dictionary formatında):
  - `'all_features'`: Tüm öznitelik listesi
  - `'filter'`: Filter method ile seçilen öznitelikler
  - `'rfe'`: RFE ile seçilen öznitelikler
  - `'embedded'`: Random Forest importance ile seçilen öznitelikler
- `reports/figures/Feature_Selection/` → Karşılaştırma grafikleri

---

#### 🏆 Notebook 3: `Model_Comparison.ipynb`
**Model Eğitimi ve Performans Karşılaştırması**

**Amaç:** Farklı öznitelik setleriyle eğitilen modellerin performanslarını karşılaştırmak ve en iyi yaklaşımı belirlemek.

**Yapılan İşlemler:**
1. **Veri Setlerinin Hazırlanması**
   - **Baseline:** Tüm öznitelikler (feature engineering sonrası)
   - **Filter Model:** SelectKBest ile seçilen öznitelikler
   - **RFE Model:** Recursive Feature Elimination ile seçilen öznitelikler
   - **Embedded Model:** Random Forest importance ile seçilen öznitelikler

2. **Model Eğitimi**
   - Her veri seti için Random Forest Classifier eğitimi
   - 5-Fold Stratified Cross-Validation uygulaması
   - Hiperparametreler: `n_estimators=100`, `random_state=42`

3. **Performans Değerlendirmesi**
   - **ROC-AUC Score:** Ana metrik (sınıf dengesizliği için uygun)
   - **Accuracy:** Genel doğruluk oranı
   - **Precision:** Pozitif tahminlerin doğruluk oranı
   - **Recall:** Gerçek pozitiflerin yakalanma oranı
   - **F1-Score:** Precision ve Recall'un harmonik ortalaması
   - **Eğitim Süresi:** Her modelin eğitim süresi (saniye)

4. **Karşılaştırmalı Analiz**
   - Model performanslarının tablo halinde sunumu
   - ROC-AUC skorlarının bar grafiği
   - Tüm metriklerin radar (spider) grafiği
   - Öznitelik sayısı vs. Performans scatter plot
   - Eğitim süresi karşılaştırması

5. **Sonuç ve Yorumlama**
   - En iyi performans gösteren yöntemin belirlenmesi
   - Öznitelik azaltmanın etkisinin analizi
   - Hesaplama verimliliği vs. Model performansı trade-off'u

**Girdiler:**
- `data/processed/X_train.csv`
- `data/processed/X_test.csv`
- `data/processed/y_train.csv`
- `data/processed/y_test.csv`
- `data/processed/selected_features.pkl`

**Çıktılar:**
- `models/base_model.pkl` → Baseline model
- `models/filter_model.pkl` → Filter method modeli
- `models/rfe_model.pkl` → RFE modeli
- `models/embedded_model.pkl` → Embedded method modeli
- `reports/figures/Model_Comparison/` → Karşılaştırma grafikleri ve tablolar

---

### 3. İş Akışı Özeti

```
1️⃣ EDA_and_Preprocessing.ipynb
   └─> İşlenmiş veri setleri oluşturur (X_train, X_test, y_train, y_test)
   
2️⃣ Feature_Selection.ipynb
   └─> İşlenmiş veriyi okur
   └─> Üç yöntemle öznitelik seçimi yapar
   └─> Seçilen öznitelikleri kaydeder (selected_features.pkl)
   
3️⃣ Model_Comparison.ipynb
   └─> İşlenmiş veriyi ve seçilen öznitelikleri okur
   └─> Dört farklı model eğitir ve karşılaştırır
   └─> Sonuçları raporlar ve görselleştirir
```

---

## 📊 Veri Seti Hakkında

**German Credit Data** veri seti, kredi başvurularının risk durumunu tahmin etmek için kullanılır. 

- **Toplam Kayıt:** 1000 gözlem
- **Öznitelik Sayısı:** 9 (+ 1 hedef değişken)
- **Hedef Değişken:** Risk (Good/Bad)

**Öznitelikler:**
- Age (Yaş)
- Sex (Cinsiyet)
- Job (İş Durumu)
- Housing (Konut Durumu)
- Saving accounts (Tasarruf Hesabı)
- Checking account (Çek Hesabı)
- Credit amount (Kredi Miktarı)
- Duration (Kredi Süresi - ay)
- Purpose (Kredi Amacı)

## 📈 Öznitelik Seçim Yöntemleri

### 1. Filter Method (Filtre Yöntemi)
- **Algoritma:** SelectKBest (f_classif)
- **Mantık:** Her özniteliğin hedef değişkenle olan istatistiksel ilişkisini (F-testi) hesaplar
- **Avantaj:** Hızlı ve model bağımsız
- **Dezavantaj:** Öznitelikler arası etkileşimi göz ardı eder

### 2. Wrapper Method (Sarmalama Yöntemi)
- **Algoritma:** RFE (Recursive Feature Elimination)
- **Mantık:** Model performansına göre iteratif olarak en az önemli öznitelikleri eler
- **Avantaj:** Model performansını doğrudan optimize eder
- **Dezavantaj:** Hesaplama maliyeti yüksek

### 3. Embedded Method (Gömülü Yöntem)
- **Algoritma:** Random Forest Feature Importance
- **Mantık:** Model eğitimi sırasında öznitelik önem skorlarını hesaplar
- **Avantaj:** Hem hızlı hem de model ile entegre
- **Dezavantaj:** Belirli model türlerine özgü

## 📝 Notlar

- Her adım bir öncekinin çıktılarını kullanır, bu yüzden sıralama önemlidir
- Görselleştirmeler Plotly ile yapılmıştır ve interaktiftir
- Cross-validation için `random_state=42` kullanılarak sonuçlar tekrarlanabilirdir

## 👨‍💻 Geliştirici

Bu proje, Öznitelik Mühendisliği dersi kapsamında hazırlanmıştır.

---