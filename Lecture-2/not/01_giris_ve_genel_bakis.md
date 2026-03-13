# 1. Kisitsiz Optimizasyona Giris

## Bu Ders Neyi Kapsiyor?

Lecture 1'de optimizasyonun genel cercevesini gorduk: minimizasyon, maksimizasyon, kisitli, kisitsiz, lineer, nonlineer...

Bu derste **kisitsiz optimizasyon** (unconstrained optimization) konusuna daliyoruz. Yani:

$$\min_{x \in \mathbb{R}^n} f(x)$$

Burada x uzerinde **hicbir kisit yok** — istedigimiz degeri secebiliriz. Tek amacimiz f(x)'i mumkun oldugunca kucuk yapan x'i bulmak.

---

## Neden Kisitsiz ile Basliyoruz?

1. **Daha basit:** Kisit yoksa sadece fonksiyonun kendisine odaklanabiliriz
2. **Temel olusturuyor:** Kisitli problemler de genellikle kisitsiz alt-problemlere donusturuluyor
3. **Pratik:** Makine ogrenmesi, derin ogrenme gibi alanlarda cogu problem kisitsiz formda

---

## Cozum Nedir? — Global ve Lokal Minimum

### Global Minimizer (Global Minimum Noktasi)

x* noktasi **global minimizer** ise:

$$f(x^*) \leq f(x) \quad \text{tum } x \in \mathbb{R}^n \text{ icin}$$

Yani butun evrende bundan daha iyi bir deger yok.

### Lokal Minimizer (Yerel Minimum Noktasi)

x* noktasi **lokal minimizer** ise, **yakininda** daha iyi bir deger yok:

$$f(x^*) \leq f(x) \quad \text{tum } x \in N \text{ icin (N bir komsuluk)}$$

Komsuluk ne demek? x*'in etrafindaki kucuk bir top gibi dusun. O topun icindeki tum noktalarda f degeri, f(x*)'dan buyuk veya esit.

### Sezgisel Anlama

Bir dagi dusun:
- **Global minimum:** Tum vadilerin en derini
- **Lokal minimum:** Bulundugun vadinin en derin noktasi (ama baska daha derin vadiler olabilir)

Gercek hayat problemi: Dagda gozlerin kapali, sadece ayaginin altindaki egimi hissedebiliyorsun. Lokal minimumu bulmak kolay (egim sifir olana kadar asagi yuru), ama global minimumu bulmak zor!

---

## Konveks Fonksiyonlarin Ozel Durumu

Konveks fonksiyonlarda isler cok basitlesiyor:

> **Teorem:** f konveks ise, her lokal minimum ayni zamanda **global minimumdur**.

> **Teorem:** f konveks ve turevlenebilir ise, her **duragan nokta** (∇f(x*) = 0) global minimumdur.

Bu neden onemli? Cunku konveks problemlerde "yanlis vadiye dusme" riski yok. Herhangi bir minimumu bulduysaniz, en iyisini buldunuz demektir.

**Ornek:** f(x) = x² konveks → x = 0'daki minimum kesinlikle global.

**Karsi ornek:** f(x) = x⁴ - 2x² konveks degil → birden fazla lokal minimum var.

---

## Duragan Nokta (Stationary Point)

Bir x* noktasi **duragan nokta** ise:

$$\nabla f(x^*) = 0$$

Yani tum kismi turevler sifir. Bu noktada fonksiyon "duz" — ne artiyor ne azaliyor.

**Dikkat:** Her duragan nokta minimum degildir! Uc olasililik var:
1. **Lokal minimum** (cukur)
2. **Lokal maksimum** (tepe)
3. **Eyer noktasi (saddle point)** — bir yonde minimum, baska yonde maksimum

Hangisi oldugunu anlamak icin 2. turev bilgisine (Hessian) ihtiyacimiz var. Bunu bir sonraki notta gorecegiz.

---

## Optimizasyon Algoritmalari Ne Yapar?

Hemen hemen tum algoritmalar su sekilde calisir:

1. Bir baslangic noktasi x₀ sec
2. Su adimi tekrarla:
   - Mevcut x_k noktasinda bilgi topla (gradient, Hessian vs.)
   - Bir sonraki x_{k+1} noktasini hesapla
   - Yeterince iyi bir cozum bulduysan dur

Bu bir **iteratif** surec. Her adimda biraz daha iyiye gidiyoruz.

Durdurma kriteri genellikle: ||∇f(x_k)|| < ε (gradient yeterince kucuk, yani neredeyse duragan noktadayiz)

---

## Iki Ana Strateji

Optimizasyon algoritmalari iki buyuk aileye ayriliyor:

### 1. Line Search (Dogru Arama)

Fikir: "Hangi yone gideyim, ve ne kadar gideyim?"

$$x_{k+1} = x_k + \alpha_k p_k$$

- **p_k:** Arama yonu (descent direction) — "hangi yone?"
- **α_k:** Adim uzunlugu (step length) — "ne kadar?"

Oncelikle yonu belirlersin, sonra o yonde ne kadar yurumeyi bir alt-problem olarak cozersin.

### 2. Trust Region (Guven Bolgesi)

Fikir: "Etrafimda bir bolge tanimlayayim, o bolge icinde modeli minimumla."

$$\min_p m_k(x_k + p) \quad \text{oyle ki } \|p\| \leq \Delta_k$$

- **m_k:** Fonksiyonun yerel modeli (yaklasimi)
- **Δ_k:** Guven bolgesi yaricapi — "ne kadar uzaga guveniyorum?"

Oncelikle ne kadar uzaga guvendigini belirlersin, sonra o bolge icinde en iyi noktayi bulmaya calisirsin.

### Farklari

| Ozellik | Line Search | Trust Region |
|---------|------------|--------------|
| Once ne belirlenir? | Yon (p_k) | Yaricap (Δ_k) |
| Sonra ne belirlenir? | Adim boyu (α_k) | Yon + mesafe (p) |
| Esneklik | Tek bir dogrultuda arar | Butun bolgeyi tariyabilir |
| Isleyis | Yon sec → o yonde yuru | Bolge tanimla → icinde minimumla |

---

## Bu Derste Ogreneceklerimiz

1. **Optimallik kosullari:** Bir noktanin minimum oldugunu nasil anlariz?
2. **Arama yonleri:** Steepest descent, Newton yontemi, Conjugate gradient
3. **Adim uzunlugu hesaplama:** Exact ve inexact line search
4. **Trust region yontemleri:** Model fonksiyonu ve guven bolgesi
5. **Quasi-Newton yontemleri:** BFGS, SR1

Tum bunlarin temeli: **Taylor acilimi** ve **lineer cebir** (gradient, Hessian, ozdegerler).
