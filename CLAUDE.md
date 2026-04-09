# real_screen_size

## Proje Ozeti
Kredi karti referansiyla (ISO 7810: 85.6x53.98mm) PC ekraninin gercek pixel/mm oranini hesaplayan kalibrasyon araci. Kullanici kredi kartini ekrana koyar, slider ile cerceve boyutunu ayarlar, onaylar ve Claude Code'a yapistirmak icin otomatik prompt olusturulur.

## Repo
- GitHub: https://github.com/umitkosa/real_screen_size
- GitHub Pages: https://umitkosa.github.io/real_screen_size/
- Yazar: Umit KOSA (@umitkosa)

## Dosya Yapisi
- `index.html` - GitHub Pages ana sayfa (calibration.html ile ayni)
- `calibration.html` - Kalibrasyon araci (tek dosya, bagimsiz, tum CSS/JS inline)
- `SKILL.md` - Claude Code skill tanimi (/real-size komutu)
- `README.md` - GitHub repo aciklamasi
- `LICENSE` - MIT lisansi
- `demo.html` - Animasyonlu demo sayfasi (henuz tamamlanmadi, .gitignore'da)

## Mevcut Ozellikler
- Kredi karti cercevesi: sol-ust koseden buyuyen, sari/beyaz ic kilavuz cizgi
- Slider: 1x ve 1/5x hassas ayar modu
- 2 tema: Koyu Mavi (#1a1a2e) ve Siyah (#000000) - her tema kendi accent rengiyle
- 5 cerceve rengi: Her tema icin farkli palet
- 5 dil: EN, US (inch), TR, DE, ES - tarayici diline gore otomatik algilama
- US modu: inch bazli prompt uretir (pixel/inch hesaplar)
- SVG bayrak ikonlari (pure CSS/SVG, emoji degil - Windows uyumlu)
- Sonuc ekrani: pixel/mm degeri, aciklama kutusu, code text preview + Copy butonu
- Otomatik Claude Code prompt olusturma
- Tema degistiginde tum accent renkler (slider, butonlar, sonuc ekrani) guncellenir
- CSS variables: --accent, --card-detail, --card-detail-bg, --explanation-border, --explanation-bg

## Teknik Detaylar
- Kredi karti: 85.6mm x 53.98mm, aspect ratio: 1.5857:1
- Frame border compensation: FRAME_TOTAL = 6px (2px border + 1px inset shadow, her taraf)
- Ic alan hesabi: innerWidth = elementWidth - 6, innerHeight = innerWidth / aspectRatio
- pixel/mm = innerWidth / 85.6
- Tipik degerler: 3.0-6.0 px/mm (96 DPI = 3.78, 120 DPI = 4.72, 144 DPI = 5.67)

## Tema Sistemi
```javascript
themes = {
  'dark-blue': { bg: '#1a1a2e', accent: '#00d4ff', outerBorder: '#1a6b8a', ... },
  'black': { bg: '#000000', accent: '#ffffff', outerBorder: '#333333', ... }
}
```
Tema degistiginde applyTheme() CSS variable'lari, inline style'lari ve renk secici dotlarini gunceller.

## Dil Sistemi
i18n objesi tum ceviri stringlerini icerir. Her dil icin:
- UI metinleri (title, subtitle, butonlar, labels)
- Dinamik fonksiyonlar: subtitle(color), guideText(name), explText(value), prompt(ppm, mpp, w, h, ex)
- Renk adlari: colors objesi (sari, beyaz, cyan, kirmizi, yesil her dilde)
- detectLang(): navigator.language ile otomatik dil algilama, en-US -> 'us'

## Yeni Ozellikler (v2)
### Yatay Slider Layout
- Slider artik yatay, kredi kartinin altinda
- 1x ve 1/5x butonlari slider'in saginda
- Default deger: 5.00 px/mm (slider 434px)

### Manuel pixel/mm Girisi
- Kalibrasyon ekraninda slider'in saginda "Degerimi zaten biliyorum" kutusu
- Text input (step 0.01) + pixel/mm birimi + ONAYLA butonu
- Slider kaydikca deger kutusu senkron guncellenir
- Deger kutusundaki oklar/yazi ile kart ve slider senkron hareket eder
- Kullanici kredi karti kalibrasyonunu atlayabilir

### Ekran Katalogu (TAMAMLANDI)
- Result screen'in altinda, kalibrasyon sonrasi gorunur
- 4 marka: Waveshare (10), Nextion (9), Adafruit (9), Raspberry Pi (6) = 34 ekran
- Marka > Model dropdown + Manuel giris (kendi mm boyutlari)
- Gercek boyutlu 1:1 onizleme cercevesi (ASLA kucultme yok)
- Ekrana sigmayan preview icin yatay scroll
- 6 dil destegi: TR, EN, US, DE, FR, ES

### Result Screen Scroll Fix
- body.result-mode class'i ile justify-content: flex-start, min-height: auto
- Uzun icerik (katalog dahil) sorunsuz scroll edilebilir

## Yapilacaklar (Sonraki Oturum)
### Demo Animasyonu
- demo.html baslandi ama tamamlanmadi
- Sanal mouse ile tiklama, slider kaydirma animasyonu
- README'ye veya siteye eklenecek
