# screen-real-size

## Proje Ozeti
Kredi karti referansiyla (ISO 7810: 85.6x53.98mm) PC ekraninin gercek pixel/mm oranini hesaplayan kalibrasyon araci. Kullanici kredi kartini ekrana koyar, slider ile cerceve boyutunu ayarlar, onaylar ve Claude Code'a yapistirmak icin otomatik prompt olusturulur.

## Repo
- GitHub: https://github.com/umitkosa/screen-real-size
- GitHub Pages: https://umitkosa.github.io/screen-real-size/
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

## Yapilacaklar (Sonraki Oturum)
### Ekran Katalogu Ozelligi
Kullanicinin fiziksel ekranini secip PC'de gercek boyutunda onizleme gormesi icin:
1. Marka > Model dropdown sistemi (4 marka ile baslayacak)
2. Desteklenecek markalar: Waveshare, Nextion, Adafruit, Raspberry Pi Foundation
3. Her ekran icin: model adi, cozunurluk, aktif alan mm (datasheet'ten dogrulanmis)
4. ~30-40 populer ekran modeli
5. Manuel giris secenegi (kullanici kendi mm degerlerini girer)
6. Gercek boyutlu onizleme cercevesi: kalibrasyon verisi x aktif alan mm = PC'de gercek boyut
7. index.html ve calibration.html her zaman senkron tutulmali (ayni dosya)

### Demo Animasyonu
- demo.html baslandi ama tamamlanmadi
- Sanal mouse ile tiklama, slider kaydirma animasyonu
- README'ye veya siteye eklenecek
