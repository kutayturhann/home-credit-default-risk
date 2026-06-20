# 🏦 Home Credit Default Risk — End-to-End Data Analytics Project

## Proje Özeti
Home Credit'in 307.511 kredi başvurusunu analiz ederek,
temerrüt riskini etkileyen faktörleri tespit ettim ve
müşteri temerrüdünü tahmin eden bir model geliştirdim.

---

## İş Problemi
Home Credit, kredi geçmişi yetersiz müşterilere hizmet vermektedir.
Bu müşterilerin temerrüde düşüp düşmeyeceğini önceden tahmin etmek,
hem finansal kayıpları azaltır hem de kredi erişimini genişletir.

---

## Kullanılan Teknolojiler
- **Python** (Pandas, NumPy, Scikit-learn, Matplotlib, Seaborn)
- **SQL** (Google BigQuery)
- **Dashboard** (Looker Studio)
- **Ortam** (Google Colab + Google Drive)

---

## Proje Aşamaları

### Aşama 1 — Keşifsel Veri Analizi (EDA)
- 307.511 satır, 122 sütun incelendi
- Hedef değişken (TARGET) dağılımı: **%8.07 temerrüt** (class imbalance tespit edildi)
- Sütunlar veri tipine göre gruplandı: 106 sayısal, 16 kategorik

### Aşama 2 — Veri Temizleme
- %40 üzeri eksik sütunlar silindi: **122 → 75 sütun**
- Sayısal eksikler medyan ile, kategorik eksikler "Unknown" ile dolduruldu
- DAYS_EMPLOYED sütunundaki 365.243 aykırı değer (1000 yıl) tespit edildi ve düzeltildi
- Y/N kategorik değerler 0/1'e dönüştürüldü

### Aşama 3 — SQL Analizi (BigQuery)
Temel bulgular:
- **Yaş:** Genç müşteriler (%11.46) yaşlılara (%4.92) göre 2.3x daha riskli
- **Meslek:** Low-skill Laborers (%17.15) en riskli, Accountants (%4.83) en güvenilir
- **Eğitim:** Akademik derece sahipleri (%1.83) ile lise mezunları (%10.93) arasında 6x fark
- **EXT_SOURCE:** 3 kaynak da düşük olan müşterilerin temerrüt oranı **%32.29**

### Aşama 4 — Dashboard (Looker Studio)
- 11 sayfalık interaktif dashboard oluşturuldu
- Her iş sorusu için ayrı sayfa tasarlandı
- BigQuery tablolarına direkt bağlantı kuruldu

### Aşama 5 — Machine Learning
| Model | ROC-AUC | Recall (Temerrüt) |
|---|---|---|
| Logistic Regression | 0.7484 | %68 |
| Random Forest | 0.7263 | %5 |

**En önemli değişkenler:** EXT_SOURCE_3, EXT_SOURCE_2, DAYS_BIRTH

---

## 💡 Temel Bulgular

1. **EXT_SOURCE skorları** temerrüdü en güçlü açıklayan değişkenler
2. **Yaş** kritik bir risk faktörü — genç müşteriler sistematik olarak daha riskli
3. **Eğitim seviyesi** arttıkça risk belirgin şekilde azalıyor
4. **Tek metrik yanıltıcı** — kredi/gelir oranı tek başına temerrüdü açıklamıyor
5. **Class imbalance** göz ardı edilmemeli — accuracy değil AUC ve Recall önemli
