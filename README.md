# WordPress Blog Otomasyonu - v2

WordPress tabanlı çok dilli blog içeriklerini DOCX'ten otomatik yayınlayan web uygulaması.

---

## v2'deki Yenilikler

- **5 Çeviri Servisi** - Azure, DeepL, Gemini, Groq, OpenAI arasından seçim
- **Karşılama Ekranı** - Mod seçimi için yeni başlangıç ekranı
- **Gelişmiş Proje Profilleri** - Tüm servis API key'leri profille birlikte kaydedilir
- **SEO Slug** - Kiril dahil tüm dillerde otomatik temiz URL
- **Yoast SEO** - Primary category otomatik set edilir
- **Varsayılan Dil Algılama** - Polylang'dan default dil çekilir, içerik her zaman Türkçe yüklenir
- **Adım Geri** - Tüm adımlarda önceki ekrana dönülebilir
- **UI** - Yeniden tasarlanmış açık tema arayüz

---

## Özellikler

- DOCX yükleme - H1 başlık, H2/H3 alt başlıklar otomatik algılanır
- Otomatik çeviri - 5 farklı servis seçeneği
- Manuel yükleme - Her dil için ayrı DOCX yüklenebilir
- Polylang entegrasyonu - Dil sürümleri otomatik bağlanır
- Kategori seçimi - Polylang'dan dil bazlı kategoriler çekilir
- Öne çıkarılan görsel - Medya kütüphanesine otomatik yüklenir, sürükle-bırak destekli
- Geriye dönük yayın - Geçmiş tarihli içerik yayınlama
- İlerleme göstergesi - Yayın adımları canlı takip

---

## Kurulum

### 1. Uygulamayı Yayına Alma

**Vercel:**
1. [vercel.com](https://vercel.com) → New Project
2. `index.html` dosyasını sürükle-bırak

**Netlify:**
1. [app.netlify.com/drop](https://app.netlify.com/drop)
2. `index.html` dosyasını sürükle-bırak

### 2. Polylang REST Link Eklentisi

Polylang kullanan her WordPress sitesine kurulması gerekir.

1. `polylang-rest-link.zip` dosyasını indirin
2. WordPress Admin → Eklentiler → Yeni Ekle → Eklenti Yükle
3. ZIP'i seçin → Şimdi Yükle → Etkinleştir

> Tek dil kullanan sitelerde bu eklentiye gerek yoktur.

### 3. WordPress Uygulama Şifresi

1. WordPress Admin → Kullanıcılar → Profil
2. **Uygulama Şifreleri** bölümüne gidin
3. Yeni şifre oluşturun ve kopyalayın

---

## Kullanım

### Otomatik Çeviri Modu

1. **Otomatik Çeviri** seçin
2. Proje profili oluşturun veya seçin
3. Çeviri servisi seçin, API key girin
4. WordPress bilgilerini girin
5. **Kategorileri Getir** ve **Dilleri Getir** butonlarına tıklayın
6. DOCX dosyasını yükleyin → **Devam Et**
7. Kontrol ekranını onaylayın
8. Kategori, görsel, diller, tarih seçin → **Yayınla**

### Manuel Yükleme Modu

1. **Manuel Yükleme** seçin
2. WordPress bilgilerini girin
3. Her dil sekmesine ayrı DOCX yükleyin
4. Tarih seçin → **Yayınla**

---

## DOCX Formatı

| Word Stili | WordPress |
|---|---|
| Heading 1 | Yazı başlığı |
| Heading 2 | `<h2>` bloğu |
| Heading 3 | `<h3>` bloğu |
| Normal | Paragraf |

> Başlığı Word'de **Heading 1** olarak işaretleyin. İlk H1 otomatik yazı başlığı olur.

---

## Desteklenen Çeviri Servisleri

| Servis | Ücretsiz Limit | Notlar |
|---|---|---|
| **Azure Translator** | 2M karakter/ay | HTML desteği mükemmel |
| **DeepL** | 500k karakter/ay | En iyi kalite (kart gerekli). `:fx` ile biten key = ücretsiz plan |
| **Google Gemini** | 1M TPM | Ücretsiz, yüksek limit |
| **Groq** | 1k istek/gün | Ücretsiz, rate limit düşük |
| **OpenAI** | Ücretli | gpt-4o-mini kullanır |

---

## Teknik Gereksinimler

- WordPress 5.8+
- Polylang (çok dilli projeler için)
- Yoast SEO (opsiyonel — breadcrumb için)
- Modern tarayıcı

---

## Polylang REST Link Eklentisi (v2.3)

İki REST endpoint sağlar:

**`POST /wp-json/pll/v1/link`**
Dil bağlantısı kurar, tema şablonunu düzeltir.
```json
{ "translations": { "tr": 100, "en": 101, "ru": 102 } }
```

**`POST /wp-json/pll/v1/resave`**
Tek postu şablon düzeltmesi için yeniden kaydeder.
```json
{ "post_id": 100 }
```

---

**Geliştiren:** Eren Akpınar
