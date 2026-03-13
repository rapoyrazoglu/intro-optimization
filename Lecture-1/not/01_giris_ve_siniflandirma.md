# 1. Optimizasyon Nedir?

## En Basit Tanimiyla

Optimizasyon = **en iyi degeri bulmak**.

Bir fonksiyonun **minimum** (en kucuk) veya **maximum** (en buyuk) degerini veren x'i ariyoruz.

$$\min_{x} f(x)$$

Ornek: f(x) = x² - 4x + 5 fonksiyonunun minimumunu bul.

Bildigin turevi alip sifira esitle:
- f'(x) = 2x - 4 = 0 → x = 2
- f(2) = 4 - 8 + 5 = 1

x = 2'de minimum deger 1'dir. Iste optimizasyon bu kadar basit basliyor!

---

## Optimizasyon Probleminin Genel Formu

$$\min_{x} f(x) \quad \text{oyle ki (subject to)} \quad x \in \Omega$$

- **f(x):** Amac fonksiyonu (objective function) - minimize etmek istedigimiz sey
- **x:** Karar degiskeni (decision variable) - degistirebildigimiz deger
- **$\Omega$:** Uygun bolge (feasible region) - x'in alabilecegi degerler kumesi

---

## Siniflandirma

### 1. Minimizasyon vs Maksimizasyon
- min f(x) = -max(-f(x))
- Yani birini cozebildin mi, digerini de cozersin. Hep **minimizasyon** uzerinden gideriz.

### 2. Surekli (Continuous) vs Ayrik (Discrete)
- **Surekli:** x herhangi bir reel sayi olabilir (x = 3.14159...)
- **Ayrik:** x sadece tam sayi olabilir (x = 1, 2, 3, ...)
- Ornek: "Kac kg seker alayim?" → surekli, "Kac araba ureteyim?" → ayrik

### 3. Kisitli (Constrained) vs Kisitsiz (Unconstrained)
- **Kisitsiz:** x'e hicbir sinir yok, istedigini sec
- **Kisitli:** x bazi kosullari saglamali (ornegin x >= 0, veya x₁ + x₂ = 10)

### 4. Lineer vs Nonlineer
- **Lineer:** f(x) = 3x₁ + 2x₂ gibi (tum terimlerin derecesi 1)
- **Nonlineer:** f(x) = x₁² + sin(x₂) gibi (kareli, trigonometrik vs.)

### 5. Konveks (Convex) vs Non-Convex
- **Konveks:** Fonksiyonun tek bir "cukuru" var → minimum bulduysan, o **global** minimumdur
- **Non-convex:** Birden fazla cukur olabilir → buldugun minimum sadece **lokal** olabilir

### 6. Global vs Lokal Cozum
- **Global minimum:** Tum x'ler icinde en kucuk f(x) degeri
- **Lokal minimum:** Yakinindaki x'ler icinde en kucuk f(x) degeri

**Ornek:** f(x) = x⁴ - 2x² + 1
- x = -1 ve x = 1'de lokal (ve global) minimum var
- x = 0'da lokal maksimum var

---

## Optimization Tree (Agac Yapisi)

```
                    Optimization
                   /            \
            Continuous         Discrete
            /        \              \
    Unconstrained  Constrained   Integer Programming
         |          /    |    \
     (Line search, Linear  Network  Stochastic
      Trust region) Prog.  Prog.    Prog.
```

Bu derste ogrencegimiz yontemler:
1. **Kisitsiz optimizasyon:** Line search, Trust region, Conjugate gradient, Quasi-Newton
2. **Lineer programlama:** Simplex, Interior point
3. **Kisitli optimizasyon:** Quadratic programming, Penalty methods, Active set
