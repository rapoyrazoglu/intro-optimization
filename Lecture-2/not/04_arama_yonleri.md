# 4. Arama Yonleri (Search Directions)

## Genel Bakis

Line search yonteminde en kritik karar: **hangi yone yuruyecegiz?**

$$x_{k+1} = x_k + \alpha_k p_k$$

p_k'yi secmenin farkli yollari var. Her birinin guc ve zayfliklerini gorecegiz:

| Yontem | Taylor Derecesi | Yakinsaklik | Maliyet |
|--------|----------------|-------------|---------|
| Steepest Descent | 1. derece | Lineer (yavas) | Dusuk |
| Newton | 2. derece | Kuadratik (hizli) | Yuksek |
| Conjugate Gradient | 1. derece + gecmis bilgisi | Superlineer | Orta |
| Quasi-Newton (BFGS) | Yaklasik 2. derece | Superlineer | Orta |

---

## Yontem 1: Steepest Descent (En Dik Inis)

### Fikir

Fonksiyonun **en hizli azaldigi** yone git. Bu yon nedir? **Negatif gradient!**

$$p_k = -\nabla f(x_k)$$

### Neden Negatif Gradient?

Taylor acilimindan:

$$f(x_k + \alpha p) \approx f(x_k) + \alpha \nabla f(x_k)^T p$$

f'nin en cok azalmasi icin ∇f(x_k)^T p **en negatif** olmali.

||p|| = 1 kisiti altinda (birim adim), ic carpimi en kucuk yapan p:

$$p = -\frac{\nabla f(x_k)}{\|\nabla f(x_k)\|}$$

Cunku ∇f^T p = ||∇f|| ||p|| cos θ, bu θ = π (yani p, gradientin tam tersi) oldugunda minimum.

### Inis Yonu Kontrolu

p_k = -∇f(x_k) gercekten inis yonu mu?

$$p_k^T \nabla f(x_k) = -\nabla f(x_k)^T \nabla f(x_k) = -\|\nabla f(x_k)\|^2 < 0 \quad ✓$$

(∇f ≠ 0 oldugu surece)

### Kuadratik Fonksiyonlarda Exact Line Search

f(x) = (1/2)x^T Q x - b^T x seklinde kuadratik fonksiyonlarda (Q simetrik pozitif definit), adim boyu icin kapali formul var:

$$\alpha_k = \frac{p_k^T \nabla f(x_k)}{p_k^T Q \, p_k} = \frac{\nabla f(x_k)^T \nabla f(x_k)}{\nabla f(x_k)^T Q \, \nabla f(x_k)}$$

Bu formul, turevi alip sifira esitlemekten gelir.

### Avantajlar
- **Basit:** Sadece gradient hesaplamak yeter
- **Global yakinsama:** Her zaman (yeterince kucuk adimla) ilerler
- **Az bellek:** n boyutlu gradient saklamak yeterli

### Dezavantajlar
- **Yavas:** Lineer yakinsaklik — ozellikle kotu kosullu problemlerde cok yavas
- **Zigzag hareketi:** Uzun dar vadilerde gradient surekli yon degistirir, ileri-geri gider

### Zigzag Problemi

Dusun: Dar bir vadi var (elips seklinde kontorler). Gradient her zaman konturlara dik, ama vadinin ekseni boyunca degil. Sonuc olarak:

```
Iterasyon 1: sag-asagi git
Iterasyon 2: sol-asagi git
Iterasyon 3: sag-asagi git
...
```

Her adim bir oncekine neredeyse dik! Cok yavas ilerliyor.

---

## Yontem 2: Newton Yontemi

### Fikir

2. derece Taylor acilimini kullan — sadece egimi degil, **egriligi** de hesaba kat:

$$f(x_k + p) \approx f(x_k) + \nabla f(x_k)^T p + \frac{1}{2} p^T \nabla^2 f(x_k) \, p$$

Bu kuadratik modeli p'ye gore minimize et:

$$\nabla_p m(p) = \nabla f(x_k) + \nabla^2 f(x_k) \, p = 0$$

$$\boxed{p_k^N = -[\nabla^2 f(x_k)]^{-1} \nabla f(x_k)}$$

### Sezgisel Anlam

Steepest descent fonksiyona bir **duz yuzey** olarak bakip en dik yone gider. Newton yontemi fonksiyona bir **kase (paraboloid)** olarak bakip dogrudan kasenin dibine atlar.

Eger fonksiyon gercekten kuadratik ise, Newton yontemi **tek adimda** cozumu bulur!

### Newton Yonu Inis Yonu mu?

Eger ∇²f(x_k) **pozitif definit** ise:

$$p_k^T \nabla f(x_k) = -\nabla f(x_k)^T [\nabla^2 f(x_k)]^{-1} \nabla f(x_k) < 0 \quad ✓$$

Cunku pozitif definit matrisin tersi de pozitif definit → kuadratik form negatif.

**Dikkat:** Hessian pozitif definit degilse, Newton yonu inis yonu olmayabilir!

### Avantajlar
- **Cok hizli:** Kuadratik yakinsaklik (cozume yakin)
- **Olceklemeye duyarsiz:** Hessian, degiskenlerin olcegini otomatik duzeltir
- **Kuadratik fonksiyonlarda 1 adim:** f kuadratikse, ilk adimda cozumu bulur

### Dezavantajlar
- **Pahali:** Her adimda Hessian hesaplamak ve n×n lineer sistem cozmek gerekir
- **Hessian gerekli:** 2. turevlerin hesabi karmasik ve pahali olabilir
- **Her zaman calismaz:** Hessian indefinit veya tekil olabilir → yon yanlis olabilir
- **Lokal yakinsama:** Baslangic noktasi cozume yakin olmalidir

### Newton Adimini Fonksiyona Yerlestirelim

p^N = -(∇²f)⁻¹ ∇f'yi Taylor acilimina koyalim:

$$f(x_k + p^N) \approx f(x_k) - \frac{1}{2} \nabla f(x_k)^T [\nabla^2 f(x_k)]^{-1} \nabla f(x_k)$$

Bu her zaman f(x_k)'dan kucuk (∇²f pozitif definit oldugu surece). Yani Newton adimi fonksiyonu kesinlikle azaltir.

---

## Newton Yonteminin Varyasyonlari

Newton yonteminin dezavantajlarini gidermek icin cesitli varyasyonlar gelistirilmistir:

### Modifiye Newton (Modified Newton)

Hessian indefinit veya tekil olabilir. Cozum: Hessian'a bir miktar birim matris ekle:

$$B_k = \nabla^2 f(x_k) + \tau I$$

τ yeterince buyuk secilirse B_k pozitif definit olur.

### Inexact Newton

Newton denklemini ∇²f · p = -∇f tam olarak cozmek yerine, **yaklasik** coz. Buyuk problemlerde gerekli.

---

## Yontem 3: Quasi-Newton Yontemleri

### Motivasyon

Newton yontemi hizli ama Hessian hesaplamak pahali. Ya Hessian'i **yaklasik** olarak olusturabilirsek?

### Ana Fikir

Her iterasyonda Hessian'in bir **yaklasimini** B_k guncelle. Gercek Hessian'i hesaplama — gradientlerdeki degisimden tahmin et.

### Secant Denklemi

B_{k+1}, su denklemi **saglamali**:

$$B_{k+1} s_k = y_k$$

Burada:
- s_k = x_{k+1} - x_k (atilan adim)
- y_k = ∇f_{k+1} - ∇f_k (gradientteki degisim)

Bu denkleme **secant denklemi** denir. n×n bilinmeyen icin n denklem oldugu icin sonsuz cozum var. Ek kosullar gerekiyor.

### BFGS Yontemi

Broyden-Fletcher-Goldfarb-Shanno. En populer quasi-Newton yontemi.

Guncelleme formulu:

$$B_{k+1} = B_k - \frac{B_k s_k s_k^T B_k}{s_k^T B_k s_k} + \frac{y_k y_k^T}{y_k^T s_k}$$

- Secant denklemini saglar ✓
- Simetriyi korur ✓
- s_k^T y_k > 0 ise pozitif definitligi korur ✓

**Pratik:** Genelde B_k degil, B_k⁻¹ (ters Hessian yaklasimi H_k) dogrudan guncellenir. Boylece her adimda lineer sistem cozmek yerine sadece matris-vektor carpimi yapilir.

Arama yonu:

$$p_k = -H_k \nabla f_k \quad (H_k \approx [\nabla^2 f_k]^{-1})$$

### SR1 (Symmetric Rank-1) Yontemi

Daha basit bir guncelleme:

$$B_{k+1} = B_k + \frac{(y_k - B_k s_k)(y_k - B_k s_k)^T}{(y_k - B_k s_k)^T s_k}$$

- Rank-1 guncelleme (BFGS rank-2)
- Pozitif definitligi **garanti etmez** — trust region ile kullanilir
- Bazi durumlarda BFGS'den daha iyi Hessian yaklasimi verir

### Quasi-Newton Ozet

| Ozellik | BFGS | SR1 |
|---------|------|-----|
| Rank | 2 | 1 |
| Pozitif definitlik | Korur | Korumaz |
| Kullanim | Line search | Trust region |
| Yakinsaklik | Superlineer | Superlineer |
| Popülerlik | Cok yaygin | Daha az yaygin |

---

## Yontem 4: Conjugate Gradient (Eslenk Gradient)

### Motivasyon

Steepest descent zigzag yapiyor cunku her adim bir oncekine dik. Ya onceki arama yonunun bilgisini de kullansak?

### Formul

$$p_k = -\nabla f(x_k) + \beta_k p_{k-1}$$

- İlk adim steepest descent: p₀ = -∇f(x₀)
- Sonraki adimlar: gradient + onceki yonun bir miktari

β_k skaleri p_k ile p_{k-1}'in **eslenk (conjugate)** olmasini saglar.

### Eslenk Ne Demek?

Iki vektor p ve q, Q matrisine gore **eslenk** ise:

$$p^T Q q = 0$$

Normal diklik p^T q = 0 iken, Q-eslenkligi Q'nun "baktigi" perspektiften diklik.

### Neden Guclu?

Kuadratik fonksiyonda (n degisken):
- Steepest descent: cozum icin potansiyel olarak **sonsuz** iterasyon
- Conjugate gradient: **en fazla n** iterasyonda tam cozum!

### Avantajlar
- Steepest descent'ten cok daha hizli
- Newton gibi Hessian saklamak gerektirmez (bellek tasarrufu)
- Buyuk olcekli problemler icin ideal

### Dezavantajlar
- Nonlineer fonksiyonlarda "sifirlanma" (restart) gerekebilir
- Newton kadar hizli degil

---

## Yontemlerin Buyuk Karsilastirmasi

Bir fonksiyonu minimum yapmak istiyorsun. Hangi yontemi sec?

### Kucuk Problem (n < 1000)
→ **Newton yontemi** veya **BFGS**: Kuadratik yakinsaklik / superlineer yakinsaklik. Hessian hesaplanabilir boyutta.

### Orta Problem (1000 < n < 100000)
→ **L-BFGS** (limited-memory BFGS): BFGS'nin bellek tasarruflu versiyonu. Son m iterasyonun bilgisini saklar.

### Buyuk Problem (n > 100000, mesela derin ogrenme)
→ **Steepest descent** (SGD varyantlari): Basit, her adim ucuz. Adam, RMSprop gibi adaptif yontemler gradient'i olcekleyerek zigzag problemini hafifletir.

### Ozet Akis Semasi

```
Problem boyutu kucuk mu?
├── Evet → Hessian hesaplanabilir mi?
│   ├── Evet → NEWTON YONTEMI
│   └── Hayir → BFGS
└── Hayir → Bellek yeterli mi?
    ├── Evet → L-BFGS
    └── Hayir → CONJUGATE GRADIENT veya SGD
```
