# 2. Modifiye Newton Yontemleri

## Problem

Newton yonteminde arama yonu soyle hesaplaniyordu:

**p_k = -H_k^{-1} * g_k**

Ama bu formul **her zaman calismaz**. Uc sorun olabilir:

| Sorun | Ne Oluyor? |
|-------|-----------|
| **Hessian indefinit** | Bazi ozdegerler pozitif, bazi negatif. Newton yonu inis yonu olmayabilir — yukari cikabilirsin. |
| **Hessian tekil (singular)** | En az bir ozdeger sifir. Matrisin tersi alinamaz — formul patlar. |
| **Hessian kotu kosullu (ill-conditioned)** | Ozdegerler arasinda cok buyuk fark var. Sayisal hatalar cok buyur. |

---

## Cozum Fikri

Hessian'i dogrudan kullanmak yerine, ona bir **duzeltme matrisi E** ekle:

**p_k = -(H + E)^{-1} * grad f(x_k)**

Burada:

| Sembol | Anlami |
|--------|--------|
| **H** | Orijinal Hessian (sorunlu olabilir) |
| **E** | Duzeltme matrisi (H'yi pozitif definit yapmak icin eklenen sey) |
| **H + E** | Duzeltilmis Hessian — artik pozitif definit, tersi alinabilir |

Amac: `H + E` pozitif definit olsun, boylece `-(H+E)^{-1} * grad f` kesinlikle **inis yonu** olsun.

---

## Yontem 1: Ozdeger Modifikasyonu (Eigenvalue Modification)

### Fikir

Hessian'in **ozdeger ayrisimini** (spectral decomposition) yap:

**H = Q * Lambda * Q^T**

Bu formulde:

| Sembol | Anlami |
|--------|--------|
| **Q** | Ozvektorlerden olusan matris. Sutunlari Hessian'in ozvektorleri. |
| **Lambda** | Kosegen matris. Kosegen elemanlari ozdegerler: l_1, l_2, ..., l_n |
| **Q^T** | Q'nun transpozu. Q ortogonal matris oldugu icin Q^T = Q^{-1}. |

Ozdeger ayrisimi sana der ki: "Bu matris su yonlerde su kadar esneme yapiyor." Her ozdeger bir yondeki "sertligi" gosterir.

### Ne Yapiyoruz?

Negatif veya sifir olan ozdegerleri **pozitif yap**:

Diyelim ozdegerler: l_1 = 5, l_2 = -3, l_3 = 0

- l_1 = 5 → tamam, dokunma
- l_2 = -3 → sorunlu! Bunu pozitif yap, mesela 3 ekle → 0... yetmez, biraz daha ekle
- l_3 = 0 → sorunlu! Buna da bir pozitif deger ekle

Duzeltme matrisi:

**DeltaLambda = diag(0, Delta_l_2, Delta_l_3)**

oyle ki **Lambda + DeltaLambda** tamamen pozitif olsun.

Sonra:

**E = Q * DeltaLambda * Q^T**

### Sorun

Ozdeger ayrisimi **cok pahali** bir islem (O(n^3)). Buyuk problemlerde pratikte yapilmaz. Bu yuzden daha ucuz alternatifler lazim.

---

## Yontem 2: Kosegen Kaydirma (Diagonal Shift)

### Fikir

En basit duzeltme: **Hessian'a tau * I ekle** (birim matrisin bir kati).

**E = tau * I**

yani **H + E = H + tau * I**

Bu formulde:

| Sembol | Anlami |
|--------|--------|
| **tau** | Pozitif bir sayi. "Ne kadar kaydirma yapayim?" |
| **I** | Birim matris (kosegenleri 1, geri kalani 0) |
| **tau * I** | Kosegen elemanlara tau eklenmis birim matris |

### Neden Calisiyor?

Eger H'nin ozdegerleri l_1, l_2, ..., l_n ise, `H + tau * I`'nin ozdegerleri:

**l_1 + tau, l_2 + tau, ..., l_n + tau**

Yani tum ozdegerlere tau ekleniyor. Eger tau'yu en negatif ozdegerin mutlak degerinden buyuk secersen, tum ozdegerler pozitif olur.

**Ornek:** Ozdegerler: 5, -3, 1.

- En negatif ozdeger: -3, mutlak degeri 3.
- tau > 3 sec, mesela tau = 4.
- Yeni ozdegerler: 9, 1, 5 — hepsi pozitif!

### Pratikte tau Nasil Secilir?

Ozdegerleri hesaplamak pahali. Onun yerine su yontem kullanilir:

1. Bir tau degeri tahmin et
2. **H + tau * I** matrisine **Cholesky ayrisinimi** dene
3. Cholesky basarili olursa → matris pozitif definit, tau yeterli
4. Cholesky basarisiz olursa → tau'yu artir ve tekrar dene

Cholesky ayrisinimi, bir matrisin pozitif definit olup olmadigini test etmenin ucuz bir yoludur. Basarili olursa matris pozitif definit demektir.

### Sezgisel Anlam

Hessian'in kosegen elemanlarini buyutuveriyorsun. Bu, fonksiyonun her yonde biraz daha "kase seklinde" gorunmesini sagliyor. Boylece Newton adimi guvenli bir inis yonu veriyor.

---

## Yontem 3: Modifiye Cholesky Faktorlestirmesi

### Kisa Aciklama

Pozitif definit bir matris **H = L * D * L^T** seklinde ayristirilabilir:

| Sembol | Anlami |
|--------|--------|
| **L** | Alt ucgensel matris (kosegenleri 1) |
| **D** | Kosegen matris (pozitif elemanlari var) |

Eger H pozitif definit **degilse**, ayrisim sirasinda D'nin bazi elemanlari negatif veya sifir cikar. Bu elemanlari **ayrisim sirasinda duzelt** — en az bir delta > 0 olacak sekilde zorla.

Boylece ozdeger ayrisimi gibi pahali bir islem yapmadan, H'yi Cholesky ayrisimi sirasinda "tamirlemis" oluyorsun.

**Not:** Bu yontem derste detayli islenmemistir.

---

## Yontem 4: Modifiye Simetrik Indefinit Faktorlestirme

### Kisa Aciklama

Hessian'i su sekilde ayristir:

**P^T * H * P = L * B * L^T**

| Sembol | Anlami |
|--------|--------|
| **P** | Permutasyon matrisi (satirlarin siralamasini degistirir) |
| **L** | Alt ucgensel matris |
| **B** | Blok kosegen matris (1x1 veya 2x2 bloklar) |

Bu ayrisimin avantaji: B **blok kosegen** oldugu icin ozdeger ayrisimi ucuz. B'yi pozitif definit yapmak icin bir duzeltme F eklenir:

**E = P^T * L * (B + F) * L^T * P - P^T * L * B * L^T * P**

Bu Cholesky'den daha **sayisal olarak kararli** (stabil).

**Not:** Bu yontem de derste detayli islenmemistir.

---

## Ozet: Hangi Yontemi Ne Zaman Kullan?

```
Hessian pozitif definit mi?
├── Evet → Normal Newton kullan, sorun yok
└── Hayir → Modifiye Newton gerekiyor
    ├── Kucuk problem → Ozdeger modifikasyonu (tam kontrol)
    ├── Orta problem → Modifiye Cholesky (verimli)
    └── Buyuk problem → Kosegen kaydirma (en basit)
        (tau sec, Cholesky dene, tutarsa devam et)
```

Pratikte en yaygin kullanilan: **Kosegen kaydirma** (diagonal shift). Basit, ucuz, cogu zaman ise yariyor.
