# 🛡️ DRP Scanner Pro - Proje Dokümantasyonu

## 📋 Proje Özeti

**DRP Scanner Pro**, SOCRadar platformundaki Digital Risk Protection (DRP) asset'lerini kullanarak Google Groups üzerinde potansiyel veri sızıntılarını tespit etmeye yarayan bir araçtır.

### Amaç
Şirketlerin brand keyword'leri, VIP hesapları ve domain'lerinin Google Groups'ta sızdırılıp sızdırılmadığını hızlıca taramak.

---

## 🏗️ Proje Mimarisi

```
┌─────────────────────────────────────────────────────────────────┐
│                    DRP Scanner Pro v5                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐      │
│  │   SOCRadar   │───▶│   Scanner    │───▶│   Google     │      │
│  │   API/Manuel │    │   Engine     │    │   Groups     │      │
│  └──────────────┘    └──────────────┘    └──────────────┘      │
│         │                   │                   │               │
│         ▼                   ▼                   ▼               │
│  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐      │
│  │ Asset Types: │    │ Features:    │    │ Output:      │      │
│  │ • Company    │    │ • Tek tek aç │    │ • Tarama     │      │
│  │ • Brand KW   │    │ • Yavaş aç   │    │ • Raporlama  │      │
│  │ • VIP Account│    │ • Hızlı aç   │    │ • HTML/TXT   │      │
│  │ • Domain     │    │ • Progress   │    │   export     │      │
│  └──────────────┘    └──────────────┘    └──────────────┘      │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 📁 Dosya Yapısı

```
DRP Scanner Pro/
│
├── drp_scanner_pro_v5.html      # Ana uygulama (SOCRadar API entegrasyonlu)
├── drp_scanner_generator_v4.html # Manuel veri girişli versiyon
├── drp_scanner_generator_v3.html # Hassas keyword kombinasyonları eklendi
├── drp_scanner_generator_v2.html # Temel scanner
│
├── Önceki Şirket Taramaları/
│   ├── sallybeauty_scanner.html
│   ├── sallybeauty_dorks.txt
│   ├── bitvavo_scanner.html
│   ├── bitvavo_dorks.txt
│   ├── repsol_dorks.txt
│   ├── circor_scanner_v2.html
│   ├── mtr_dorks.txt
│   ├── examworks_scanner.html
│   └── dat_dorks.txt
│
└── README.md (bu dosya)
```

---

## 🔧 Teknik Detaylar

### SOCRadar API Entegrasyonu

**Base URL:** `https://platform.socradar.com/api`

**Kullanılan Endpoint:**
```
GET /company/{company_id}/drp-configuration/assets
```

**Headers:**
```
API-Key: YOUR_API_KEY
Content-Type: application/json
```

**Query Parameters:**
| Parametre | Zorunlu | Açıklama |
|-----------|---------|----------|
| assetType | Evet | "main", "suggested", "submission" |
| email | Evet | Kullanıcı email adresi |
| sortBy | Evet | "asset", "monitor", "approveDate" |
| limit | Hayır | 1-500 (default: 100) |
| offset | Hayır | Pagination için |

**Çekilen Asset Türleri:**
- `Company Name` - Şirket adları
- `Brand Keyword` - Marka keyword'leri
- `VIP Account` - VIP email hesapları

---

### Google Groups Tarama Yöntemleri

**1. Direkt Google Groups Arama:**
```
https://groups.google.com/search?q=KEYWORD&inOrg=false
```

**2. Google Dork ile Arama:**
```
site:groups.google.com "KEYWORD"
site:groups.google.com "KEYWORD" password
site:groups.google.com "KEYWORD" credential
site:groups.google.com "@domain.com" internal
```

---

### Hassas Keyword Kombinasyonları

Scanner otomatik olarak şu kombinasyonları oluşturur:

| Keyword | Risk Seviyesi | Açıklama |
|---------|---------------|----------|
| password | 🔴 Kritik | Şifre sızıntısı |
| credential | 🔴 Kritik | Kimlik bilgisi |
| token | 🔴 Kritik | API/Auth token |
| api_key | 🔴 Kritik | API anahtarı |
| secret | 🔴 Kritik | Gizli bilgi |
| login | 🟠 Yüksek | Giriş bilgisi |
| internal | 🟠 Yüksek | İç döküman |
| vpn | 🟠 Yüksek | VPN bilgisi |
| admin | 🟡 Orta | Admin erişimi |
| ssh | 🟡 Orta | SSH bilgisi |
| ftp | 🟡 Orta | FTP bilgisi |
| database | 🟡 Orta | Veritabanı bilgisi |

---

## 🎨 UI/UX Tasarımı

### Renk Paleti (SOCRadar Brand)

| Renk | HEX | Kullanım |
|------|-----|----------|
| Energetic Coral | #FF4562 | CTA butonlar, vurgular |
| Deep Night Blue | #1B1B3C | Ana arka plan |
| Night Dark | #15152F | Kart arka planları |
| Night Light | #54546F | Border, secondary |
| Success Green | #4ADE80 | Başarılı durumlar |
| Pure White | #FFFFFF | Metin, içerik |

### 60-30-10 Kuralı
- **%60** Deep Night Blue - Arka plan
- **%30** White/Light - İçerik alanları
- **%10** Energetic Coral - CTA, vurgular

---

## 🚀 Kullanım Kılavuzu

### Yöntem 1: API ile Otomatik Çekme

1. HTML dosyasını tarayıcıda aç
2. **API Key** gir
3. **Company ID** gir (SOCRadar URL'den: `platform.socradar.com/company/XXXXX/`)
4. **Email** gir
5. "Asset'leri Çek" butonuna tıkla
6. Scanner otomatik oluşturulur

### Yöntem 2: Manuel Veri Girişi

1. "📝 Manuel Giriş" butonuna tıkla
2. **Şirket Adı** gir
3. SOCRadar'dan veriyi kopyala-yapıştır:
   ```
   keyword1
   Brand Keyword
   user@company.com2025-01-01
   vip@company.com
   VIP Account
   admin@company.com2025-01-01
   ```
4. "Parse Et & Scanner Oluştur" tıkla

### Tarama Kontrolleri

| Buton | Kısayol | Açıklama |
|-------|---------|----------|
| ▶️ Sonrakini Aç | Space/Enter | Tek link aç |
| 🐢 Yavaş Aç | - | Slider hızında otomatik |
| ⚡ Hızlı Aç | - | Tümünü anında aç |
| ⏹️ Durdur | - | Otomatik açmayı durdur |
| 🔄 Sıfırla | - | Başa dön |

---

## 📊 Çıktı Formatları

### HTML Export
- Standalone scanner dosyası
- Offline kullanılabilir
- Tüm kontroller dahil

### TXT Export (Dork Listesi)
```
# Company Name - Google Groups Dorks
# Generated: 2025-01-01T00:00:00.000Z

# COMPANY NAME
site:groups.google.com "Company Inc"

# BRAND KEYWORDS
site:groups.google.com "brandname"

# VIP ACCOUNTS
site:groups.google.com "ceo@company.com"

# DOMAINS
site:groups.google.com "@company.com"

# HASSAS KOMBİNASYONLAR
site:groups.google.com "company" password
site:groups.google.com "@company.com" credential
```

---

## 📝 Rapor Şablonu

Tarama sonuçları için standart rapor formatı:

### Kritik Bulgu Varsa:
```
CRITICAL FINDING DETECTED

Company: [Şirket Adı]
Date: [Tarih]
Source: Google Groups

Finding Details:
- URL: [Google Groups URL]
- Type: [Credential Leak / Internal Document / VIP Exposure]
- Affected Asset: [Email/Keyword/Domain]
- Severity: Critical/High/Medium
- Description: [Detaylı açıklama]

Recommendation:
- Immediate password reset required
- Review exposed credentials
- Monitor for unauthorized access
```

### Kritik Bulgu Yoksa:
```
No critical findings identified. Brand keywords and VIP account 
email addresses were searched on Google Groups. Search results 
returned only unrelated public content such as [news articles / 
spam posts / promotional content]. No internal documents, 
corporate communications, leaked credentials, or any other 
sensitive data exposure was detected.
```

---

## ⚠️ Bilinen Sorunlar

### CORS Hatası
**Problem:** Tarayıcı güvenlik politikası nedeniyle SOCRadar API'sine doğrudan erişilemiyor.

**Çözümler:**
1. Manuel veri girişi kullan
2. n8n workflow ile proxy oluştur
3. Chrome extension olarak geliştir
4. Backend proxy server kur

### Rate Limiting
**Problem:** Çok hızlı tarama Google tarafından engellenebilir.

**Çözüm:** Yavaş mod kullan (2-3 saniye aralık)

---

## 🔮 Gelecek Geliştirmeler

- [ ] n8n workflow entegrasyonu
- [ ] Chrome extension versiyonu
- [ ] Otomatik rapor oluşturma
- [ ] Dark web tarama entegrasyonu
- [ ] Slack/Teams bildirim entegrasyonu
- [ ] Bulk şirket tarama
- [ ] Sonuç önbelleğe alma

---

## 👨‍💻 Geliştirici Notları

### Yeni Şirket Ekleme
1. Company ID'yi bul
2. API'den asset'leri çek veya manuel gir
3. Scanner oluştur
4. Taramayı yap
5. Sonuçları değerlendir
6. Raporu hazırla

### Sonuç Değerlendirme Kriterleri

**Kritik DEĞİL:**
- Genel haber/basın bültenleri
- Spam/reklam postları
- Public ürün bilgileri
- Alakasız isim eşleşmeleri (false positive)
- Eski tarihli (5+ yıl) içerikler

**Kritik OLABILIR:**
- Email + password kombinasyonu
- Internal/confidential dökümanlar
- VPN/SSH/admin bilgileri
- API key/token sızıntıları
- Güncel tarihli içerikler

---

## 📞 Destek

Bu proje SOCRadar CTI/DRP araştırmaları için geliştirilmiştir.

**Versiyon:** 5.0
**Son Güncelleme:** Aralık 2025
**Geliştirici:** Claude AI Assistant

---

*Bu dokümantasyon, projenin mevcut durumunu ve kullanımını açıklamaktadır. Herhangi bir sorunuz için konuşma geçmişine bakabilirsiniz.*
