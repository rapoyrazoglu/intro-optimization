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

### Lecture 3 — Line Search Yontemleri

| # | Konu | Not |
|---|------|-----|
| 01 | Line Search'e Giris | [01_line_search_giris.md](Lecture-3/not/01_line_search_giris.md) |
| 02 | Modifiye Newton Yontemleri | [02_modifiye_newton.md](Lecture-3/not/02_modifiye_newton.md) |
| 03 | Adim Boyu Secimi ve Wolfe Kosullari | [03_adim_boyu_ve_wolfe.md](Lecture-3/not/03_adim_boyu_ve_wolfe.md) |
| 04 | Yakinsaklik Teorisi | [04_yakinsaklik_teorisi.md](Lecture-3/not/04_yakinsaklik_teorisi.md) |
| 05 | Cozulmus Ornekler | [05_cozulmus_ornekler.md](Lecture-3/not/05_cozulmus_ornekler.md) |
| 06 | Pratik Sorular (50 Soru) | [06_pratik_sorular.md](Lecture-3/not/06_pratik_sorular.md) |

### Lecture 4 — Trust Region Yontemleri

| # | Konu | Not |
|---|------|-----|
| 01 | Giris ve Motivasyon | [01_giris_ve_motivasyon.md](Lecture-4/not/01_giris_ve_motivasyon.md) |
| 02 | Trust Region Temel Formulasyonu | [02_trust_region_temel_formulasyon.md](Lecture-4/not/02_trust_region_temel_formulasyon.md) |
| 03 | Optimallik Kosullari ve Algoritma | [03_optimallik_kosullari_ve_algoritma.md](Lecture-4/not/03_optimallik_kosullari_ve_algoritma.md) |
| 04 | Yaklasik Cozum Yontemleri | [04_yaklasik_cozum_yontemleri.md](Lecture-4/not/04_yaklasik_cozum_yontemleri.md) |
| 05 | Cozulmus Ornekler | [05_cozulmus_ornekler.md](Lecture-4/not/05_cozulmus_ornekler.md) |
| 06 | Pratik Sorular (50 Soru) | [06_pratik_sorular.md](Lecture-4/not/06_pratik_sorular.md) |

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
├── Lecture-3/
│   ├── ders/          # Orijinal ders PDF'leri
│   └── not/           # Turkce notlar (markdown)
├── Lecture-4/
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
Turkce notlar cikar. Her kavrami sifirdan, sezgisel olarak acikla. Formullerde kullanlilan her elamni ve esitliklerin taraflarinda bulunan seyleri acikla mesela : f(xₖ + α·pₖ)  ≤  f(xₖ) + c₁ · α · ∇fₖᵀpₖ bunda sembolun sagi solu ne anlama geliyor burda neleri karsilatiriyoruz falan.

Son dosyada en az 10 cozulmus ornek soru olsun.

Notlari Lecture-X/not/ altina markdown olarak kaydet:
(Çeşitlendirilebilir)
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

---

## Pratik Soru Olusturma

Bir lecture icin pratik sorular olusturmak istiyorsan asagidaki promptu kopyala, `X` yerine ders numarasini yaz ve Claude'a gonder:

```
Lecture-X/not/ altindaki ders notlarini oku.
Bu notlardaki konulari kapsayan 50 pratik (matematiksel, teorik degil) soru hazirla:
- 10 kolay soru (temel hesaplamalar, tek adimlik islemler)
- 20 orta soru (birden fazla adim, kavramlari birlestirme)
- 20 zor soru (tam iterasyonlar, karmasik senaryolar, uc durumlar)

Her sorunun cozumu <details> etiketi icinde gizli olsun.
Sorular gercek sayilarla hesaplama gerektirsin, ispat veya tanimlama sorulmasi.

Dosyayi Lecture-X/not/06_pratik_sorular.md olarak kaydet.
```
