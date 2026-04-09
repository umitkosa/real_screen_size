---
name: real-size
description: Ekran kalibrasyon araci - kredi karti referansiyla gercek pixel/mm oranini hesaplar
user_invocable: true
---

# /real-size - Ekran Gercek Boyut Kalibrasyon Araci

Bu skill, kullanicinin PC ekranindaki gercek pixel/mm oranini hesaplamak icin standart bir kredi kartini (ISO/IEC 7810 ID-1: 85.6mm x 53.98mm) referans olarak kullanir.

## Ne Zaman Kullanilir

- Kullanici `/real-size` yazdiginda
- Kullanici ekran kalibrasyonu, pixel/mm orani veya gercek boyut hesaplamasi istediginde
- Kucuk ekranlar (Nextion, Raspberry Pi vb.) icin arayuz gelistirirken dogru boyutlandirma gerektiginde

## Kalibrasyon Akisi

1. Bu skill'in bulundugu dizindeki `calibration.html` dosyasini tarayicida ac:
   - Windows: `start calibration.html`
   - macOS: `open calibration.html`
   - Linux: `xdg-open calibration.html`

2. Kullaniciya soyle:
   > Kalibrasyon sayfasi tarayicinizda acildi. Lutfen:
   > 1. Tarayici zoom seviyesinin %100 oldugundan emin olun (Ctrl+0)
   > 2. Kredi kartinizi ekrana koyun
   > 3. Slider ile ekrandaki dikdortgeni kartinizla birebir ayni boyuta getirin
   > 4. "ONAYLA" butonuna basin
   > 5. Gosterilen pixel/mm degerini bana bildirin (veya "Sonucu Kopyala" ile kopyalayip yapistin)

3. Kullanici degeri bildirdikten sonra:
   - Degeri `calibration-result.json` dosyasina kaydet (skill dizininde)
   - Degeri Claude Memory'e kaydet (gelecek konusmalar icin)

## Kayit Formati

### calibration-result.json
```json
{
  "pixelPerMm": 3.7383,
  "mmPerPixel": 0.2675,
  "cardWidthPx": 320,
  "cardHeightPx": 202,
  "calibratedAt": "2026-04-09T12:00:00Z",
  "browserZoom": "100%",
  "note": "ISO 7810 ID-1 kredi karti referansi (85.6mm x 53.98mm)"
}
```

### Memory Kaydi
Memory'e su bilgileri kaydet:
- pixel/mm orani
- mm/pixel orani
- kalibrasyon tarihi
- Tip: `user` (kullanicinin ekran ozelligi)

## Kullanim Modu (Kalibrasyon Sonrasi)

Eger `calibration-result.json` zaten mevcutsa veya memory'de kalibrasyon verisi varsa:

1. Once mevcut kalibrasyon verisini oku
2. Kullaniciya mevcut degeri bildir ve yeni kalibrasyon isteyip istemedigini sor
3. Eger kullanici yeni bir ekran boyutu hesaplamasi istiyorsa, kayitli pixel/mm oranini kullanarak hesapla:
   - `gercek_mm = pixel_degeri / pixelPerMm`
   - `gereken_pixel = istenen_mm * pixelPerMm`

## Ornek Kullanimlar

Kalibrasyon sonrasi kullanici sunlari sorabilir:
- "480x320 piksellik bir ekran gercekte kac mm?"
- "50mm genisliginde bir buton kac piksel olmali?"
- "4.3 inch Nextion ekrani icin tam boyutlu bir onizleme goster"

Bu durumlarda kayitli pixel/mm oranini kullanarak hassas donusumler yap.

## Referans Bilgileri

- ISO/IEC 7810 ID-1 (Kredi Karti): 85.6mm x 53.98mm
- En-boy orani: 1.5857:1
- Tipik PC ekran pixel/mm degerleri: 3.0 - 6.0 arasi
- 96 DPI ekran teorik degeri: 3.78 px/mm
- 120 DPI ekran teorik degeri: 4.72 px/mm
- 144 DPI ekran teorik degeri: 5.67 px/mm
