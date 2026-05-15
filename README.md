# sozler-app-meta

Sözler Nesriyat mobile app için public meta veri.

## Dosyalar

### `released-versions.json`

Mağazalarda **live** olan sürümleri tutar. Mobile app (cold-start'ta) bu dosyayı okuyup mevcut sürümle karşılaştırır, gerekiyorsa "update var" ikonu gösterir.

```json
{
  "android": "2.5.5",   // Play Store live
  "huawei": "2.5.5",    // Huawei AppGallery live
  "ios": "2.5.5"        // (referans amaçlı — mobile iOS için iTunes Lookup kullanır)
}
```

## Otomatik güncelleme

Ana repo'daki ([`sozlernesriyat/sozler_nesriyat`](https://github.com/sozlernesriyat/sozler_nesriyat) — private) `released-versions.json` değiştiğinde, bir GitHub Actions workflow burayı sync eder.

- **Play Store**: `poll-stores-live.yml` (cron saatte bir, Google Play Developer API)
- **Huawei**: `mark-huawei-live.yml` (workflow_dispatch, manuel — Huawei AppGallery Connect API 403 nedeniyle)
- **iOS**: bu dosyada referans olarak tutulur ama mobile iOS path'i iTunes Lookup public API kullanır

## Neden ayrı public repo?

Ana repo private; mobile app `raw.githubusercontent.com` üzerinden private repo'yu anonim okuyamaz (404). Backend endpoint katmanını eklememek için bu küçük public repo seçildi.

## Manuel düzenleme

Olağanüstü durumda (workflow başarısız vs.) `released-versions.json`'u doğrudan UI'dan da düzenleyebilirsiniz; mobile sonraki cold-start'ta yeni değeri alır.
