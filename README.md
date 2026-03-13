# Optimizasyona Giris — Ders Notlari

Numerik optimizasyon dersinin Turkce notlari. Her kavram sifirdan, sezgisel olarak, sadece temel turev ve integral bilgisiyle anlasilabilecek sekilde aciklanmistir.

---

## Icerik

### Lecture 1 — Optimizasyonun Temelleri

| # | Konu | Not |
|---|------|-----|
| 01 | Giris ve Siniflandirma | [01_giris_ve_siniflandirma.md](Lecture-1/not/01_giris_ve_siniflandirma.md) |
| 02 | Konveks Kavramlar | [02_konveks_kavramlar.md](Lecture-1/not/02_konveks_kavramlar.md) |
| 03 | Kalkulus | [03_kalkulus.md](Lecture-1/not/03_kalkulus.md) |
| 04 | Lineer Cebir | [04_lineer_cebir.md](Lecture-1/not/04_lineer_cebir.md) |
| 05 | Cozulmus Ornekler | [05_cozulmus_ornekler.md](Lecture-1/not/05_cozulmus_ornekler.md) |

### Lecture 2 — Kisitsiz Optimizasyonun Temelleri

| # | Konu | Not |
|---|------|-----|
| 01 | Giris ve Genel Bakis | [01_giris_ve_genel_bakis.md](Lecture-2/not/01_giris_ve_genel_bakis.md) |
| 02 | Optimallik Kosullari | [02_optimallik_kosullari.md](Lecture-2/not/02_optimallik_kosullari.md) |
| 03 | Algoritmalar ve Stratejiler | [03_algoritmalar_ve_stratejiler.md](Lecture-2/not/03_algoritmalar_ve_stratejiler.md) |
| 04 | Arama Yonleri | [04_arama_yonleri.md](Lecture-2/not/04_arama_yonleri.md) |
| 05 | Cozulmus Ornekler | [05_cozulmus_ornekler.md](Lecture-2/not/05_cozulmus_ornekler.md) |

---

## Klasor Yapisi

```
intro-optimization/
├── README.md
├── Lecture-1/
│   ├── ders/          # Orijinal ders PDF'leri
│   └── not/           # Turkce notlar (markdown)
├── Lecture-2/
│   ├── ders/          # Orijinal ders PDF'leri
│   └── not/           # Turkce notlar (markdown)
└── ...
```

---

## Yeni Ders Notu Olusturma

Yeni bir lecture icin not olusturmak istiyorsan asagidaki promptu kopyala, `X` yerine ders numarasini yaz (ornegin `3`) ve Claude'a gonder:

```
Lecture-X/ders/ klasorundeki PDF'i oku (gorselleri cikarip tek tek oku).
Icerigi sadece temel turev ve integral bilen birine anlatacak sekilde
Turkce notlar cikar. Her kavrami sifirdan, sezgisel olarak acikla.
Son dosyada en az 10 cozulmus ornek soru olsun.

Notlari Lecture-X/not/ altina markdown olarak kaydet:
01 - Giris ve siniflandirma
02 - Temel kavramlar
03 - Kalkulus
04 - Lineer cebir
05 - Cozulmus ornekler

(Konu basliklari PDF icerigine gore degisebilir, uygun sekilde ayarla)

Bitince README.md dosyasini guncelle:
- Icerik bolumune yeni lecture'in tablosunu ekle
- Klasor yapisina yeni lecture'i ekle
```
