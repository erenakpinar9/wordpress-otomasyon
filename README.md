# WordPress Blog Otomasyonu

WordPress tabanlı çok dilli blog içeriklerini DOCX'ten otomatik olarak yayınlayan web uygulaması. Polylang ile dil yönetimi, Azure/DeepL/Gemini/Groq/OpenAI ile otomatik çeviri destekler.

> **Not:** Azure dışındaki servislerin kullanımı v2 sürümünde yayınlanacaktır.

---

## Özellikler

- **DOCX Yükleme** — H1 başlık, H2/H3 alt başlıklar otomatik algılanır
- **Otomatik Çeviri** — Azure
- **Manuel Yükleme** — Her dil için ayrı DOCX yüklenebilir
- **Polylang Entegrasyonu** — Dil sürümleri otomatik birbirine bağlanır
- **Kategori Seçimi** — Polylang'dan dil bazlı kategoriler çekilir
- **Öne Çıkarılan Görsel** — Medya kütüphanesine otomatik yüklenir
- **SEO Slug** — Kiril dahil tüm dillerde otomatik temiz URL üretimi
- **Yoast SEO** — Primary category otomatik set edilir
- **Proje Profilleri** — Birden fazla WordPress sitesi için profil yönetimi
- **Geriye Dönük Yayın** — Geçmiş tarihli içerik yayınlama

---

## Kurulum

### 1. Uygulamayı Yayına Alma

`index.html` dosyasını herhangi bir statik hosting'e yükleyin:

**Vercel:**
1. [vercel.com](https://vercel.com) → New Project
2. `index.html` dosyasını sürükle-bırak

**Netlify:**
1. [app.netlify.com/drop](https://app.netlify.com/drop)
2. `index.html` dosyasını sürükle-bırak

### 2. Polylang REST Link Eklentisini Kurma

Polylang kullanan her WordPress sitesine kurulması gerekir.

1. `polylang-rest-link.zip` dosyasını indirin
2. WordPress Admin → Eklentiler → Yeni Ekle → Eklenti Yükle
3. ZIP'i seçin → Şimdi Yükle → Etkinleştir

> **Not:** Tek dil kullanan sitelerde bu eklentiye gerek yoktur.

### 3. WordPress Uygulama Şifresi Oluşturma

1. WordPress Admin → Kullanıcılar → Profil
2. **Uygulama Şifreleri** bölümüne gidin
3. Yeni bir şifre oluşturun ve kopyalayın

---

## Kullanım

### Otomatik Çeviri Modu

1. **Başlangıç** ekranında **Otomatik Çeviri** seçin
2. **Proje Profili** oluşturun veya mevcut profili seçin
3. Çeviri servisi seçin ve API anahtarını girin
4. WordPress bağlantı bilgilerini girin
5. **Kategorileri Getir** ve **Dilleri Getir** butonlarına tıklayın
6. DOCX dosyanızı yükleyin
7. **Kontrol Et** ekranını onaylayın
8. Kategori, görsel, çevrilecek diller ve tarih seçin → **Yayınla**

### Manuel Yükleme Modu

1. **Başlangıç** ekranında **Manuel Yükleme** seçin
2. WordPress bağlantı bilgilerini girin
3. Her dil için ayrı DOCX dosyası yükleyin
4. Tarih seçin → **Yayınla**

---

## DOCX Formatı

DOCX dosyanızı şu kurallara göre hazırlayın:

| Word Stili | WordPress'te |
|---|---|
| **Heading 1** | Yazı başlığı |
| **Heading 2** | `<h2>` bloğu |
| **Heading 3** | `<h3>` bloğu |
| Normal | Paragraf |

> Başlığınızı Word'de **Heading 1** olarak işaretleyin. İlk H1 başlık otomatik olarak yazı başlığı olur, içerik bu başlıktan sonra başlar.

---

## Desteklenen Çeviri Servisleri

| Servis | Ücretsiz Limit | Notlar |
|---|---|---|
| **Azure Translator** | 2M karakter/ay | Önerilen — HTML desteği mükemmel |
| **DeepL** | 500k karakter/ay | En iyi çeviri kalitesi (kart gerekli) |  > **v2 sürümünde!**
| **Google Gemini** | 1M TPM | Ücretsiz, yüksek limit | > **v2 sürümünde!**
| **Groq** | 1k istek/gün | Ücretsiz ama limit düşük | > **v2 sürümünde!**
| **OpenAI** | Ücretli | gpt-4o-mini kullanır | > **v2 sürümünde!**

---

## Teknik Gereksinimler

- **WordPress** 5.8+
- **Polylang** (çok dilli projeler için)
- **Yoast SEO** (opsiyonel — breadcrumb için)
- Modern tarayıcı (Chrome, Firefox, Safari, Edge)

---

## Polylang REST Link Eklentisi

Bu eklenti iki REST API endpoint'i sağlar:

**`POST /wp-json/pll/v1/link`**
Polylang çeviri bağlantısını kurar ve tema şablonlarını düzeltir.

```json
{ "translations": { "tr": 100, "en": 101, "ru": 102, "de": 103 } }
```

**`POST /wp-json/pll/v1/resave`**
Tek bir postu şablon düzeltmesi için yeniden kaydeder.

```json
{ "post_id": 100 }
```

