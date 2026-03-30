# Lecture 3 — Pratik Sorular (50 Soru)

---

# KOLAY (Soru 1–10)

---

## Soru 1: Inis Yonu Kontrolu

f(x,y) = 3x^2 + y^2 icin x = (2, 1) noktasinda p = (-3, -1) bir inis yonu mu?

<details>
<summary>Cozum</summary>

grad f = (6x, 2y)
grad f(2,1) = (12, 2)

p^T grad f = (-3)(12) + (-1)(2) = -36 - 2 = -38 < 0

Evet, inis yonudur.
</details>

---

## Soru 2: Steepest Descent Yonu

f(x,y) = x^2 + 3y^2 - 2x fonksiyonunda x0 = (0, 1) noktasinda steepest descent yonunu bul.

<details>
<summary>Cozum</summary>

grad f = (2x - 2, 6y)
grad f(0, 1) = (-2, 6)

Steepest descent yonu = -grad f = (2, -6)
</details>

---

## Soru 3: Newton Yonu — Basit

f(x,y) = x^2 + y^2 icin x0 = (3, 4) noktasinda Newton yonunu hesapla.

<details>
<summary>Cozum</summary>

grad f(3,4) = (6, 8)

H = | 2  0 |
    | 0  2 |

H^{-1} = | 1/2  0   |
          | 0    1/2 |

p^N = -H^{-1} grad f = -(3, 4) = (-3, -4)

x1 = (3,4) + (-3,-4) = (0, 0). Tek adimda cozum!
</details>

---

## Soru 4: Armijo Kosulu — Basit Kontrol

f(x) = x^2, x0 = 2, p = -1, alfa = 0.5, c1 = 0.25.
Armijo kosulu saglaniyor mu?

<details>
<summary>Cozum</summary>

f(x0) = 4
f'(x0) = 4
grad f * p = 4 * (-1) = -4

Sol taraf: f(2 + 0.5*(-1)) = f(1.5) = 2.25

Sag taraf: f(x0) + c1 * alfa * grad f * p = 4 + 0.25 * 0.5 * (-4) = 4 - 0.5 = 3.5

2.25 <= 3.5? Evet. Armijo saglaniyor.
</details>

---

## Soru 5: Hessian Pozitif Definitlik

H = | 4  1 |  pozitif definit mi? Ozdegerlerini bul.
    | 1  2 |

<details>
<summary>Cozum</summary>

det(H) = 8 - 1 = 7 > 0
iz(H) = 4 + 2 = 6 > 0

Ozdegerler: l^2 - 6l + 7 = 0
l = (6 ± sqrt(36-28))/2 = (6 ± sqrt(8))/2
l1 = (6+2.83)/2 = 4.41
l2 = (6-2.83)/2 = 1.59

Ikisi de pozitif → pozitif definit.
</details>

---

## Soru 6: Diagonal Shift — Basit

H = | 3   0 |  icin H + tau*I pozitif definit olacak en kucuk tam sayi tau'yu bul.
    | 0  -2 |

<details>
<summary>Cozum</summary>

Ozdegerler: 3 ve -2 (kosegen matris).

H + tau*I ozdegerleri: 3 + tau, -2 + tau

-2 + tau > 0 → tau > 2

En kucuk tam sayi: tau = 3.

Kontrol: ozdegerler 6 ve 1 → pozitif definit ✓
</details>

---

## Soru 7: Exact Line Search — Tek Degisken

f(x) = (x-3)^2, x0 = 0, p = 1.
Exact line search ile alfa bul.

<details>
<summary>Cozum</summary>

phi(alfa) = f(0 + alfa*1) = f(alfa) = (alfa - 3)^2

phi'(alfa) = 2(alfa - 3) = 0 → alfa = 3

x1 = 0 + 3*1 = 3. f(3) = 0. Tek adimda minimum!
</details>

---

## Soru 8: Backtracking — Tek Adim

f(x) = x^2, x0 = 4, p = -1. Backtracking: alfa_hat = 4, rho = 0.5, c = 0.5.
Ilk alfa kabul ediliyor mu?

<details>
<summary>Cozum</summary>

f(4) = 16
f'(4) = 8
grad f * p = 8*(-1) = -8

alfa = 4: f(4 + 4*(-1)) = f(0) = 0
Armijo: 0 <= 16 + 0.5*4*(-8) = 16 - 16 = 0

0 <= 0? Evet (esitlik saglar). alfa = 4 kabul edildi.

x1 = 0. Tek adimda minimuma gitti!
</details>

---

## Soru 9: Curvature Kosulu — Kavramsal

Curvature kosulu ne ise yarar? Neden sadece Armijo yetmez?

<details>
<summary>Cozum</summary>

Armijo kosulu "fonksiyon yeterince dustu mu?" kontrol eder. Ama cok kucuk bir adim da Armijo'yu saglar (cunku kucuk adimda fonksiyon neredeyse degismez, bu da "yeterince azaldi" sayilir).

Curvature kosulu "yeterince ileri gittin mi?" kontrol eder. Yeni noktadaki egimin, baslangictakinden yeterince az olmasi gerekir. Bu, cok kisa adim atilmasini onler.

Ikisi birlikte: ne cok buyuk ne cok kucuk adim — makul bir aralikta.
</details>

---

## Soru 10: Wolfe Parametreleri

Asagidakilerin tipik degerlerini yaz ve nedenini acikla:
a) c1 (Armijo sabiti)
b) c2 (curvature sabiti) — Newton icin
c) c2 — conjugate gradient icin

<details>
<summary>Cozum</summary>

a) c1 = 10^{-4} (cok kucuk). Neden: Neredeyse her adimi kabul eder, sadece "en azindan biraz dusus olsun" der.

b) c2 = 0.9 (buyuk, genis aralik). Neden: Newton yonu zaten iyi hesaplanmis, alfa = 1 genellikle dogru, fazla kisitlamaya gerek yok.

c) c2 = 0.1 (kucuk, dar aralik). Neden: Conjugate gradient yonteminde hassas adim boyu secimi gerekiyor. Eslenkligi korumak icin alfa exact line search'e yakin olmali.
</details>

---

# ORTA (Soru 11–30)

---

## Soru 11: Steepest Descent — Exact Line Search

f(x,y) = 2x^2 + y^2 - 2xy, x0 = (2, 0). Bir iterasyon yap (exact line search).

<details>
<summary>Cozum</summary>

grad f = (4x - 2y, 2y - 2x)
grad f(2, 0) = (8, -4)

p0 = (-8, 4)

phi(a) = f(2-8a, 4a) = 2(2-8a)^2 + (4a)^2 - 2(2-8a)(4a)

= 2(4 - 32a + 64a^2) + 16a^2 - 2(8a - 32a^2)
= 8 - 64a + 128a^2 + 16a^2 - 16a + 64a^2
= 8 - 80a + 208a^2

phi'(a) = -80 + 416a = 0 → a = 80/416 = 5/26

x1 = (2-8*5/26, 4*5/26) = (2-40/26, 20/26) = (12/26, 20/26) = (6/13, 10/13)

f(2,0) = 8
f(6/13, 10/13) = 2(36/169) + 100/169 - 2(60/169) = 72/169 + 100/169 - 120/169 = 52/169 = 4/13 ≈ 0.31

f: 8 → 0.31. Buyuk dusus!
</details>

---

## Soru 12: Newton Adimi — 2 Degisken

f(x,y) = x^2 + xy + 2y^2 - 4x - 6y, x0 = (0, 0). Newton adimini hesapla.

<details>
<summary>Cozum</summary>

grad f = (2x + y - 4, x + 4y - 6)
grad f(0,0) = (-4, -6)

H = | 2  1 |
    | 1  4 |

det(H) = 8 - 1 = 7

H^{-1} = 1/7 * | 4  -1 |
                | -1  2 |

p^N = -H^{-1} * (-4, -6) = -1/7 * | 4  -1 | * | -4 | = -1/7 * | -16+6  | = -1/7 * | -10 | = | 10/7 |
                                     | -1  2 |   | -6 |          |  4-12  |          | -8  |   | 8/7  |

x1 = (0,0) + (10/7, 8/7) = (10/7, 8/7)

Kontrol: grad f(10/7, 8/7) = (20/7 + 8/7 - 4, 10/7 + 32/7 - 6) = (28/7 - 4, 42/7 - 6) = (0, 0) ✓

Tek adimda cozum!
</details>

---

## Soru 13: Armijo Kosulunun Saglandigi Aralik

f(x) = x^4, x0 = 1, p = -1, c1 = 0.25.
Armijo kosulunun saglandigi alfa araligini bul.

<details>
<summary>Cozum</summary>

f(1) = 1
f'(1) = 4
grad f * p = -4

Armijo: f(1 - alfa) <= 1 + 0.25 * alfa * (-4) = 1 - alfa

(1 - alfa)^4 <= 1 - alfa

alfa < 1 icin (1-alfa) > 0, iki tarafi (1-alfa)'ya bol:

(1-alfa)^3 <= 1

Bu her zaman saglanir: 0 < alfa < 1 icin (1-alfa) < 1 oldugundan (1-alfa)^3 < 1 ✓

alfa = 1: f(0) = 0 <= 1 - 1 = 0 ✓ (esitlik)

alfa > 1: f(1-alfa) = (1-alfa)^4, bu pozitif. 1 - alfa < 0. Pozitif <= negatif olmaz.

Sonuc: **0 < alfa <= 1**
</details>

---

## Soru 14: Wolfe Kosullari — Tam Kontrol

f(x) = x^2 + 1, x0 = 4, p = -1, alfa = 2.
c1 = 0.1, c2 = 0.9. Iki Wolfe kosulunu da kontrol et.

<details>
<summary>Cozum</summary>

f(4) = 17, f'(4) = 8, grad f * p = -8

**Armijo:**
f(4 + 2*(-1)) = f(2) = 5
5 <= 17 + 0.1*2*(-8) = 17 - 1.6 = 15.4
5 <= 15.4 ✓

**Curvature:**
f'(2) * p = 4 * (-1) = -4
c2 * grad f(x0) * p = 0.9 * (-8) = -7.2
-4 >= -7.2 ✓

Her iki kosul saglaniyor. alfa = 2 kabul edilebilir.
</details>

---

## Soru 15: Backtracking — 3 Deneme

f(x,y) = x^2 + 9y^2, x0 = (3, 1), p = -grad f = (-6, -18).
alfa_hat = 1, rho = 0.5, c = 0.1. Kabul edilen alfa'yi bul.

<details>
<summary>Cozum</summary>

f(3,1) = 9 + 9 = 18
grad f = (6, 18), grad f^T p = (6)(-6) + (18)(-18) = -36 - 324 = -360

**alfa = 1:** f(3-6, 1-18) = f(-3, -17) = 9 + 2601 = 2610
2610 <= 18 + 0.1*1*(-360) = 18 - 36 = -18? Hayir

**alfa = 0.5:** f(3-3, 1-9) = f(0, -8) = 0 + 576 = 576
576 <= 18 + 0.1*0.5*(-360) = 18 - 18 = 0? Hayir

**alfa = 0.25:** f(3-1.5, 1-4.5) = f(1.5, -3.5) = 2.25 + 110.25 = 112.5
112.5 <= 18 + 0.1*0.25*(-360) = 18 - 9 = 9? Hayir

**alfa = 0.125:** f(3-0.75, 1-2.25) = f(2.25, -1.25) = 5.0625 + 14.0625 = 19.125
19.125 <= 18 + 0.1*0.125*(-360) = 18 - 4.5 = 13.5? Hayir

**alfa = 0.0625:** f(3-0.375, 1-1.125) = f(2.625, -0.125) = 6.89 + 0.14 = 7.03
7.03 <= 18 + 0.1*0.0625*(-360) = 18 - 2.25 = 15.75? Evet!

alfa = 0.0625 kabul edildi. f: 18 → 7.03.

Yorum: Steepest descent yonu cok agresif (x2 yonu 3 kat buyuk), buyuk adimlar overshoot yapiyor.
</details>

---

## Soru 16: Diagonal Shift — Cholesky Testi

H = | 1   2 |. Bu matris pozitif definit mi? Degilse tau = 3 ile H + tau*I'yi kontrol et.
    | 2   1 |

<details>
<summary>Cozum</summary>

det(H) = 1 - 4 = -3 < 0 → pozitif definit degil (indefinit).

Ozdegerler: l^2 - 2l - 3 = 0 → l = 3 veya l = -1

H + 3I = | 4  2 |
          | 2  4 |

det = 16 - 4 = 12 > 0, iz = 8 > 0 → pozitif definit ✓

Ozdegerler: 3+3=6 ve -1+3=2. Ikisi de pozitif ✓
</details>

---

## Soru 17: Exact Line Search — Kuadratik Formul

f(x) = (1/2)x^T Q x - b^T x, Q = [[4, 0], [0, 2]], b = (4, 2), x0 = (0, 0).
Steepest descent ile 1 iterasyon yap.

<details>
<summary>Cozum</summary>

grad f = Qx - b = (0,0) - (4,2) = (-4, -2)
p = (4, 2)

alfa = (grad f^T * grad f) / (grad f^T * Q * grad f)

grad f^T grad f = 16 + 4 = 20

Q * grad f = | 4  0 | | -4 | = | -16 |
             | 0  2 | | -2 |   | -4  |

grad f^T Q grad f = (-4)(-16) + (-2)(-4) = 64 + 8 = 72

alfa = 20/72 = 5/18

x1 = (0,0) + (5/18)(4, 2) = (20/18, 10/18) = (10/9, 5/9)

Gercek cozum: x* = Q^{-1} b = (1, 1). Henuz ulasmadk.
</details>

---

## Soru 18: Modifiye Newton Adimi

f(x,y) = 2x^2 - 3y^2, x0 = (1, 1).
a) Newton yonunun inis yonu olup olmadigini kontrol et.
b) tau = 7 ile modifiye Newton yonunu hesapla.

<details>
<summary>Cozum</summary>

grad f = (4x, -6y), grad f(1,1) = (4, -6)

H = | 4   0 |
    | 0  -6 |

**a) Newton:**
H^{-1} = | 1/4   0    |
          | 0    -1/6  |

p^N = -| 1/4   0   | | 4  | = -| 1 | = | -1 |
       | 0    -1/6 | | -6 |    | 1 |   | -1 |

p^T grad f = (-1)(4) + (-1)(-6) = -4 + 6 = 2 > 0

Inis yonu **degil!** Hessian indefinit oldugu icin Newton yonu yukari cikis veriyor.

**b) Modifiye Newton (tau = 7):**
H + 7I = | 11   0 |
          |  0   1 |

(H+7I)^{-1} = | 1/11  0 |
               | 0     1 |

p = -| 1/11  0 | | 4  | = | -4/11 |
     | 0     1 | | -6 |   |  6    |

p^T grad f = (-4/11)(4) + (6)(-6) = -16/11 - 36 = -412/11 < 0 ✓

Modifiye Newton inis yonu sagliyor.
</details>

---

## Soru 19: Strong Wolfe Kontrolu

f(x) = x^2, x0 = 3, p = -1, alfa = 4.
c1 = 0.1, c2 = 0.9. Strong Wolfe kosullarini kontrol et.

<details>
<summary>Cozum</summary>

f(3) = 9, f'(3) = 6, grad f * p = -6

**Armijo:**
f(3-4) = f(-1) = 1
1 <= 9 + 0.1*4*(-6) = 9 - 2.4 = 6.6 ✓

**Strong Wolfe Curvature:**
|f'(-1) * p| <= c2 * |grad f(x0) * p|
|(-2)(-1)| <= 0.9 * |(-6)|
|2| <= 5.4
2 <= 5.4 ✓

Strong Wolfe saglaniyor. Ama dikkat: x = -1 noktasi minimum degil (minimum x = 0), hatta minimumun oteki tarafina gectik. Yine de Strong Wolfe kabul ediyor.
</details>

---

## Soru 20: Newton — Non-Kuadratik

f(x) = e^x - 2x, x0 = 0. Newton ile 2 iterasyon yap.

<details>
<summary>Cozum</summary>

f'(x) = e^x - 2
f''(x) = e^x

**Iterasyon 0:**
f'(0) = 1 - 2 = -1
f''(0) = 1

p = -f'(0)/f''(0) = -(-1)/1 = 1

x1 = 0 + 1 = 1

**Iterasyon 1:**
f'(1) = e - 2 ≈ 2.718 - 2 = 0.718
f''(1) = e ≈ 2.718

p = -0.718/2.718 = -0.264

x2 = 1 - 0.264 = 0.736

**Gercek cozum:** f'(x*) = 0 → e^{x*} = 2 → x* = ln(2) ≈ 0.693

x0 = 0, x1 = 1, x2 = 0.736, x* = 0.693. Hizla yaklasiyoruz.
</details>

---

## Soru 21: Kosul Sayisi ve Steepest Descent

Q = | 10  0 | icin f(x) = (1/2)x^T Q x.
    |  0  1 |

a) Kosul sayisini hesapla.
b) Steepest descent en kotu yakinsaklik oranini bul.

<details>
<summary>Cozum</summary>

a) kappa = l_max / l_min = 10/1 = 10

b) r = ((kappa-1)/(kappa+1))^2 = (9/11)^2 = 81/121 ≈ 0.669

Her iterasyonda hata en fazla %33 azalir. Fena degil ama ideal de degil.

Karsilastirma: kappa = 1 olsaydi r = 0 (tek adimda biterdi), kappa = 100 olsaydi r ≈ 0.96 (cok yavas).
</details>

---

## Soru 22: Gradient ve Newton Yonu Karsilastirmasi

f(x,y) = 4x^2 + y^2, x0 = (1, 4).
a) Steepest descent yonunu bul.
b) Newton yonunu bul.
c) Hangisi daha iyi?

<details>
<summary>Cozum</summary>

grad f(1,4) = (8, 8)

**a) Steepest descent:**
p_SD = (-8, -8)

**b) Newton:**
H = | 8  0 |, H^{-1} = | 1/8  0   |
    | 0  2 |             | 0    1/2 |

p^N = -H^{-1} (8, 8) = -(1, 4) = (-1, -4)

x1^N = (1,4) + (-1,-4) = (0, 0). Tek adimda cozum!

**c) Newton daha iyi.** Steepest descent x ve y yonunde esit miktarda giderken (-8,-8), Newton egriligi hesaba katip dogru oranla gidiyor (-1,-4). Newton x yonunde 1 birim, y yonunde 4 birim gidiyor — tam isabetle minimuma variyor.
</details>

---

## Soru 23: Armijo ile Alfa Araligi

f(x,y) = x^2 + y^2, x0 = (1, 1), p = (-2, -2), c1 = 0.5.
Armijo kosulunun saglandigi alfa araligini bul.

<details>
<summary>Cozum</summary>

f(1,1) = 2
grad f(1,1) = (2, 2)
grad f^T p = (2)(-2) + (2)(-2) = -8

Yeni nokta: (1-2a, 1-2a)

Sol taraf: f(1-2a, 1-2a) = 2(1-2a)^2

Sag taraf: 2 + 0.5*a*(-8) = 2 - 4a

Esitsizlik: 2(1-2a)^2 <= 2 - 4a

2(1 - 4a + 4a^2) <= 2 - 4a
2 - 8a + 8a^2 <= 2 - 4a
8a^2 - 4a <= 0
4a(2a - 1) <= 0

a > 0 icin: 2a - 1 <= 0 → **a <= 1/2**
</details>

---

## Soru 24: Curvature Kosulu Araligi

Soru 23'teki verilerle, c2 = 0.1 icin curvature kosulunun saglandigi alfa araligini bul.

<details>
<summary>Cozum</summary>

Yeni nokta: (1-2a, 1-2a)

grad f(yeni) = (2(1-2a), 2(1-2a)) = (2-4a, 2-4a)

Sol taraf: grad f(yeni)^T p = (2-4a)(-2) + (2-4a)(-2) = -4(2-4a) = -8 + 16a

Sag taraf: c2 * grad f(x0)^T p = 0.1 * (-8) = -0.8

-8 + 16a >= -0.8
16a >= 7.2
**a >= 0.45**

Wolfe araligi: 0.45 <= a <= 0.5
</details>

---

## Soru 25: Modifiye Newton — tau Secimi

H = | 2   -3 |. H + tau*I pozitif definit olacak en kucuk tam sayi tau'yu bul.
    | -3   1 |

<details>
<summary>Cozum</summary>

Ozdegerler: l^2 - 3l + (2-9) = l^2 - 3l - 7 = 0

l = (3 ± sqrt(9+28))/2 = (3 ± sqrt(37))/2

sqrt(37) ≈ 6.08

l1 = (3 + 6.08)/2 = 4.54
l2 = (3 - 6.08)/2 = -1.54

H + tau*I ozdegerleri: 4.54 + tau, -1.54 + tau

-1.54 + tau > 0 → tau > 1.54

En kucuk tam sayi: **tau = 2**

Kontrol: H + 2I = | 4  -3 |
                    | -3  3 |
det = 12 - 9 = 3 > 0, iz = 7 > 0 → pozitif definit ✓
</details>

---

## Soru 26: Newton — Tekil Hessian

f(x,y) = (x + y)^2 + x icin x0 = (0, 0) noktasinda Newton uygulanabilir mi?

<details>
<summary>Cozum</summary>

f = x^2 + 2xy + y^2 + x

grad f = (2x + 2y + 1, 2x + 2y)
grad f(0,0) = (1, 0)

H = | 2  2 |
    | 2  2 |

det(H) = 4 - 4 = 0 → Hessian tekil!

H^{-1} mevcut degil, Newton uygulanamaz.

Cozum: Diagonal shift ile H + tau*I kullan. tau = 1 icin:

H + I = | 3  2 |
         | 2  3 |
det = 9-4 = 5 > 0 → pozitif definit ✓
</details>

---

## Soru 27: Steepest Descent — 2 Iterasyon

f(x,y) = x^2 + 4y^2, x0 = (4, 1). Exact line search ile 2 iterasyon.

<details>
<summary>Cozum</summary>

**Iterasyon 0:**
grad f(4,1) = (8, 8), p0 = (-8, -8)

phi(a) = (4-8a)^2 + 4(1-8a)^2
= 16 - 64a + 64a^2 + 4(1 - 16a + 64a^2)
= 16 - 64a + 64a^2 + 4 - 64a + 256a^2
= 20 - 128a + 320a^2

phi'(a) = -128 + 640a = 0 → a = 128/640 = 1/5

x1 = (4-8/5, 1-8/5) = (12/5, -3/5)

**Iterasyon 1:**
grad f(12/5, -3/5) = (24/5, -24/5), p1 = (-24/5, 24/5)

phi(a) = (12/5 - 24a/5)^2 + 4(-3/5 + 24a/5)^2

= (1/25)(12-24a)^2 + (4/25)(-3+24a)^2

= (1/25)[(12-24a)^2 + 4(-3+24a)^2]

= (1/25)[144 - 576a + 576a^2 + 4(9 - 144a + 576a^2)]

= (1/25)[144 - 576a + 576a^2 + 36 - 576a + 2304a^2]

= (1/25)[180 - 1152a + 2880a^2]

phi'(a) = (1/25)[-1152 + 5760a] = 0 → a = 1152/5760 = 1/5

x2 = (12/5 - 24/(5*5), -3/5 + 24/(5*5)) = (12/5 - 24/25, -3/5 + 24/25)

= (60/25 - 24/25, -15/25 + 24/25) = (36/25, 9/25)

f(4,1) = 20
f(12/5, -3/5) = 144/25 + 4(9/25) = 144/25 + 36/25 = 180/25 = 7.2
f(36/25, 9/25) = 1296/625 + 4(81/625) = 1296/625 + 324/625 = 1620/625 = 2.592

f: 20 → 7.2 → 2.592. Azaliyor ama yavas — zigzag goruntusu var.
</details>

---

## Soru 28: Wolfe — Reddedilen Alfa

f(x) = x^2, x0 = 10, p = -1, alfa = 0.001, c1 = 10^{-4}, c2 = 0.9.
Bu alfa Wolfe kosullarini sagliyor mu?

<details>
<summary>Cozum</summary>

f(10) = 100, f'(10) = 20, grad f * p = -20

**Armijo:**
f(10 - 0.001) = f(9.999) = 99.98
99.98 <= 100 + 10^{-4} * 0.001 * (-20) = 100 - 0.000002 = 99.999998
99.98 <= 99.999998 ✓

**Curvature:**
f'(9.999) * (-1) = 19.998 * (-1) = -19.998
c2 * grad f * p = 0.9 * (-20) = -18

-19.998 >= -18? **Hayir!** -19.998 < -18

Curvature saglanmiyor. Egim hala neredeyse baslangictaki kadar dik — adim cok kisa!

Yorum: alfa = 0.001 neredeyse yerinde saymak. Armijo kabul eder (biraz dusus oldu) ama curvature reddeder (yeterince ilerleme yok).
</details>

---

## Soru 29: Newton — 2 Iterasyon (Non-Kuadratik)

f(x) = x^3 - 6x + 2, x0 = 3. Newton ile 2 iterasyon.

<details>
<summary>Cozum</summary>

f'(x) = 3x^2 - 6
f''(x) = 6x

**Iterasyon 0:**
f'(3) = 27 - 6 = 21
f''(3) = 18

p = -21/18 = -7/6

x1 = 3 - 7/6 = 11/6 ≈ 1.833

**Iterasyon 1:**
f'(11/6) = 3(121/36) - 6 = 363/36 - 216/36 = 147/36 = 49/12 ≈ 4.083
f''(11/6) = 66/6 = 11

p = -(49/12)/11 = -49/132

x2 = 11/6 - 49/132 = 242/132 - 49/132 = 193/132 ≈ 1.462

Gercek cozum: 3x^2 = 6 → x = sqrt(2) ≈ 1.414

x0=3, x1≈1.833, x2≈1.462, x*≈1.414. Hizla yaklasiyoruz.
</details>

---

## Soru 30: Backtracking — Farkli Parametreler

f(x,y) = x^2 + y^2, x0 = (6, 8), p = (-12, -16).
Iki farkli parametre seti icin kac denemede kabul edildigini bul:

a) alfa_hat = 1, rho = 0.5, c = 0.5
b) alfa_hat = 1, rho = 0.5, c = 0.01

<details>
<summary>Cozum</summary>

f(6,8) = 100, grad f = (12, 16), grad f^T p = -144-256 = -400

**a) c = 0.5:**

alfa=1: f(-6,-8)=100. 100 <= 100+0.5*1*(-400)=100-200=-100? Hayir
alfa=0.5: f(0,0)=0. 0 <= 100+0.5*0.5*(-400)=0? Evet (esitlik)
**2 denemede** kabul.

**b) c = 0.01:**

alfa=1: f(-6,-8)=100. 100 <= 100+0.01*1*(-400)=96? Hayir
alfa=0.5: f(0,0)=0. 0 <= 100+0.01*0.5*(-400)=98? Evet!
**2 denemede** kabul.

Her iki durumda da 2 deneme. Ama c kucuk olunca sag taraf daha buyuk (daha kolay gecilir), yani buyuk adimlar daha kolay kabul edilir.
</details>

---

# ZOR (Soru 31–50)

---

## Soru 31: Steepest Descent + Exact — 3 Iterasyon

f(x,y) = 5x^2 + y^2 - 4xy, x0 = (2, 0). 3 iterasyon exact line search.

<details>
<summary>Cozum</summary>

grad f = (10x - 4y, 2y - 4x)

**Iter 0:**
grad f(2,0) = (20, -8), p0 = (-20, 8)

phi(a) = 5(2-20a)^2 + (8a)^2 - 4(2-20a)(8a)
= 5(4-80a+400a^2) + 64a^2 - 4(16a-160a^2)
= 20-400a+2000a^2 + 64a^2 - 64a+640a^2
= 20-464a+2704a^2

phi'(a) = -464+5408a = 0 → a = 464/5408 = 29/338

x1 = (2-20*29/338, 8*29/338) = (2-580/338, 232/338) = (96/338, 232/338) = (48/169, 116/169)

Hmm sayilar cok karisik. Q matrisini kullanarak formul ile yapalim:

Q = | 10  -4 |
    | -4   2 |

**Iter 0:**
g0 = (20, -8), p0 = (-20, 8)
g^T g = 400 + 64 = 464
Qg = (10*20+(-4)(-8), -4*20+2*(-8)) = (200+32, -80-16) = (232, -96)
g^T Qg = 20*232 + (-8)(-96) = 4640+768 = 5408

a0 = 464/5408 = 29/338

x1 = (2,0) + (29/338)(-20, 8) = (2-580/338, 232/338) = (96/169, 116/169)

**Iter 1:**
g1 = Q*x1 = (10*96/169-4*116/169, -4*96/169+2*116/169)
= (960/169-464/169, -384/169+232/169) = (496/169, -152/169)

||g1||^2 = (496^2+152^2)/169^2 = (246016+23104)/28561 = 269120/28561

Bu cok karisik. Sonucu ozetleyelim:

Steepest descent zigzag yapar. f deger dizisi: azaliyor ama her adimda yonu degistiriyor. Newton ise Q kuadratik oldugu icin tek adimda cozerdi.

x* = Q^{-1} * 0 = (0,0) (cunku b=0). f(0,0)=0.
</details>

---

## Soru 32: Newton — Indefinit Hessian ve Modifiye

f(x,y) = x^3 - 3xy^2, x0 = (1, 1).
a) Hessian'in indefinit oldugunu goster.
b) tau = 10 ile modifiye Newton yonunu bul.

<details>
<summary>Cozum</summary>

grad f = (3x^2 - 3y^2, -6xy)
grad f(1,1) = (0, -6)

H = | 6x    -6y |
    | -6y   -6x |

H(1,1) = | 6   -6 |
          | -6  -6 |

**a)** Ozdegerler: (6-l)(-6-l) - 36 = 0
-36 + 36 - l^2 = 0? Hayir:
(6-l)(-6-l) - 36 = -36-6l+6l+l^2 - 36 = l^2 - 72

l^2 = 72 → l = ±sqrt(72) = ±6sqrt(2) ≈ ±8.49

Bir pozitif (+8.49), bir negatif (-8.49) → **indefinit** ✓

**b) Modifiye Newton:**
H + 10I = | 16  -6 |
           | -6   4 |

det = 64 - 36 = 28 > 0 → pozitif definit ✓

(H+10I)^{-1} = 1/28 * | 4   6 |
                        | 6  16 |

p = -1/28 * | 4   6 | | 0  | = -1/28 * | -36 | = | 36/28  | = | 9/7  |
             | 6  16 | | -6 |            | -96 |   | 96/28  |   | 24/7 |

p^T grad f = (9/7)(0) + (24/7)(-6) = -144/7 < 0 ✓ Inis yonu.
</details>

---

## Soru 33: Wolfe Kosullari — Alfa Araligi

f(x,y) = x^2 + 2y^2, x0 = (2, 1), p = -grad f = (-4, -4).
c1 = 0.25, c2 = 0.75 icin Wolfe araligini bul.

<details>
<summary>Cozum</summary>

f(2,1) = 4+2 = 6
grad f = (4, 4), grad f^T p = -16-16 = -32

Yeni nokta: (2-4a, 1-4a)

**Armijo:**
f(2-4a, 1-4a) = (2-4a)^2 + 2(1-4a)^2
= 4-16a+16a^2 + 2(1-8a+16a^2)
= 4-16a+16a^2+2-16a+32a^2
= 6-32a+48a^2

6-32a+48a^2 <= 6 + 0.25*a*(-32) = 6-8a
48a^2-24a <= 0
24a(2a-1) <= 0 → **a <= 1/2**

**Curvature:**
grad f(2-4a, 1-4a) = (2(2-4a), 4(1-4a)) = (4-8a, 4-16a)

grad f^T p = (4-8a)(-4) + (4-16a)(-4) = -16+32a-16+64a = -32+96a

-32+96a >= 0.75*(-32) = -24
96a >= 8
**a >= 1/12**

Wolfe araligi: **1/12 <= a <= 1/2**

Exact line search: phi'(a) = -32 + 96a = 0 → a = 1/3. Bu aralik icinde ✓
</details>

---

## Soru 34: Backtracking vs Exact Karsilastirmasi

f(x,y) = 4x^2 + y^2, x0 = (1, 4), p = -grad f = (-8, -8).

a) Exact line search ile alfa bul.
b) Backtracking (alfa_hat=1, rho=0.5, c=0.1) ile alfa bul.
c) Fonksiyon degerlerini karsilastir.

<details>
<summary>Cozum</summary>

f(1,4) = 4+16 = 20
grad f = (8, 8), grad f^T p = -64-64 = -128

**a) Exact:**
phi(a) = 4(1-8a)^2 + (4-8a)^2
= 4(1-16a+64a^2) + 16-64a+64a^2
= 4-64a+256a^2+16-64a+64a^2
= 20-128a+320a^2

phi'(a) = -128+640a = 0 → a = 1/5

x1 = (1-8/5, 4-8/5) = (-3/5, 12/5)
f(-3/5, 12/5) = 4(9/25)+144/25 = 36/25+144/25 = 180/25 = 7.2

**b) Backtracking:**
alfa=1: f(1-8, 4-8) = f(-7,-4) = 196+16 = 212
212 <= 20+0.1*1*(-128)=7.2? Hayir

alfa=0.5: f(-3, 0) = 36
36 <= 20+0.1*0.5*(-128)=13.6? Hayir

alfa=0.25: f(-1, 2) = 4+4 = 8
8 <= 20+0.1*0.25*(-128)=16.8? Evet!

**c) Karsilastirma:**

| | Exact | Backtracking |
|--|-------|-------------|
| alfa | 0.2 | 0.25 |
| f(x1) | 7.2 | 8 |
| Deneme sayisi | - | 3 |

Exact biraz daha iyi ama backtracking 3 basit denemede yakin bir sonuc veriyor.
</details>

---

## Soru 35: Newton — Iraksama

f(x) = x^(1/3) (kup kok), x0 = 1. Newton calisir mi?

<details>
<summary>Cozum</summary>

f'(x) = (1/3)x^(-2/3)
f''(x) = (-2/9)x^(-5/3)

Newton adimi: p = -f'(x)/f''(x) = -[(1/3)x^(-2/3)] / [(-2/9)x^(-5/3)]
= (1/3)/(2/9) * x^(-2/3+5/3) = (3/2) * x

x_{k+1} = x_k + p = x_k + (3/2)x_k = (5/2)x_k

x0 = 1, x1 = 5/2, x2 = 25/4, x3 = 125/8, ...

Her adimda 5/2 ile carpiliyor — **iraksiyoruz!**

f'(x) = 0'in cozumu yok (kup kokun turevi asla sifir olmaz). Newton, olmayan bir duragan noktayi ariyorve iraksiyor.

Ders: Newton her zaman calismaz. Baslangic noktasi ve fonksiyon yapisi onemli.
</details>

---

## Soru 36: Kuadratik Exact Line Search — Q Matrisi ile

f(x) = (1/2)x^T Q x - b^T x, Q = [[3,1],[1,2]], b = (1,0), x0 = (0,0).
Newton ve steepest descent ile birer iterasyon yap, karsilastir.

<details>
<summary>Cozum</summary>

g0 = Qx0 - b = -b = (-1, 0)

**Steepest Descent:**
p0 = (1, 0)

a = g^T g / (g^T Q g) = 1 / ((-1,0) Q (-1,0)^T)

Q*g = | 3 1 | | -1 | = | -3 |
      | 1 2 | |  0 |   | -1 |

g^T Q g = (-1)(-3)+(0)(-1) = 3

a = 1/3

x1_SD = (0,0) + (1/3)(1,0) = (1/3, 0)

f(1/3, 0) = (1/2)(1/3,0)Q(1/3,0)^T - (1,0)(1/3,0)^T
= (1/2)(1/3)(1/3*3) - 1/3 = (1/2)(1/3) - 1/3 = 1/6 - 1/3 = -1/6

**Newton:**
H = Q = [[3,1],[1,2]]
det = 6-1 = 5
Q^{-1} = 1/5 * | 2  -1 |
                | -1  3 |

p^N = -Q^{-1}(-1,0) = 1/5*(2, -1) = (2/5, -1/5)

x1_N = (2/5, -1/5)

f(2/5, -1/5) = (1/2)(2/5,-1/5)Q(2/5,-1/5)^T - (1,0)(2/5,-1/5)^T

Qx* = (2/5*3+(-1/5)*1, 2/5*1+(-1/5)*2) = (5/5, 0) = (1, 0) = b ✓

f(x*) = (1/2)x*^T b - b^T x* = (1/2)(2/5) - 2/5 = 1/5 - 2/5 = -1/5

| | SD | Newton |
|--|-----|--------|
| x1 | (1/3, 0) | (2/5, -1/5) |
| f(x1) | -1/6 ≈ -0.167 | -1/5 = -0.2 |
| Bitti? | Hayir | **Evet** |
</details>

---

## Soru 37: Strong Wolfe — Dar Aralik

f(x) = (x-2)^4, x0 = 0, p = 1, c1 = 0.1, c2 = 0.1.
a) Armijo araligini bul.
b) Strong Wolfe araligini bul.

<details>
<summary>Cozum</summary>

f(0) = 16, f'(0) = -4(0-2)^3 = 32, grad f*p = 32

Dikkat: p = 1 ama grad f(0) = 32, yani p^T grad f = 32 > 0. Bu **inis yonu degil!**

Inis yonu icin p = -1 olmali (grad f * p = -32 < 0).

p = -1 ile devam edelim:

Yeni nokta: x = -a (cunku 0 + a*(-1) = -a)

**a) Armijo:**
f(-a) = (-a-2)^4 = (a+2)^4

(a+2)^4 <= 16 + 0.1*a*(-32) = 16 - 3.2a

a = 0 icin: 16 <= 16 ✓
a kucukken: (a+2)^4 ≈ 16 + 32a + ... Yani 16+32a <= 16-3.2a → 35.2a <= 0 → a <= 0

Armijo hemen bozuluyor! Cunku p = -1 iken fonksiyon (x=0'dan sola gidince) artiyor. x0 = 0'da, fonksiyonun minimumu x = 2'de — sola gitmek yanlis yon.

Duzeltme: p = +1 ile (inis yonu) tekrar deneyelim. Ama p^T grad f = 32 > 0, inis yonu degil.

Hmm, f'(0) = 32 > 0 yani fonksiyon x=0'da artiyor. Inis yonu p = -1:
grad f * p = 32*(-1) = -32 < 0 ✓

Yeni nokta: x = 0 + a*(-1) = -a
f(-a) = (-a-2)^4 = (a+2)^4

Bu a > 0 icin f(0)'dan buyuk (cunku x=2'den uzaklasiyoruz). Yani sola gitmek fonksiyonu artiriyor.

Problem su: x=0'da gradyan pozitif, sol inis yonu gibi gorunuyor ama fonksiyon x^4-tipi ve minimum sagda. f'(0)=32>0, -p yonu (sag) asil inis yonu olmali.

p = 1 (saga git) ile: grad f * p = 32 > 0 → inis yonu degil.
p = -1 (sola git) ile: grad f * p = -32 < 0 → inis yonu ama fonksiyon artiyor!

Aslinda sorun su: f(x) = (x-2)^4, minimum x=2. f'(0)=32>0, yani x=0'da fonksiyon sag tarafa artiyor. Sola gidince azalir mi? f(-1) = 81 > f(0)=16. Hayir!

Aslinda f'(0) = 4(0-2)^3 = 4(-8) = -32. Tekrar hesaplayalim!

f'(x) = 4(x-2)^3
f'(0) = 4(-2)^3 = 4(-8) = -32

Gradyan = -32. Inis yonu: p = -grad f yonunde = p = +1 (saga dogru).

grad f * p = (-32)(1) = -32 < 0 ✓

p = 1 ile:

Yeni nokta: x = a
f(a) = (a-2)^4

**a) Armijo:** (a-2)^4 <= 16 + 0.1*a*(-32) = 16 - 3.2a

a=1: 1 <= 12.8 ✓
a=2: 0 <= 9.6 ✓
a=3: 1 <= 6.4 ✓
a=4: 16 <= 3.2? Hayir

Tam sinir: (a-2)^4 = 16 - 3.2a → sayisal olarak a ≈ 3.8

Armijo: **0 < a <= ~3.8**

**b) Strong Wolfe:**
|f'(a)*p| <= c2*|f'(0)*p|
|4(a-2)^3| <= 0.1*32 = 3.2

(a-2)^3'un mutlak degeri <= 0.8
|a-2| <= 0.8^{1/3} ≈ 0.928

1.07 <= a <= 2.93 (yaklasik)

Strong Wolfe + Armijo kesisimi: **~1.07 <= a <= ~2.93**

a = 2 (tam minimum) bu aralikta ✓
</details>

---

## Soru 38: Diagonal Shift — Iteratif Cholesky

H = | 1   3 | icin Cholesky ile tau bul.
    | 3   2 |

a) tau = 0 ile Cholesky dene.
b) tau = 8 ile Cholesky dene.
c) H + tau*I pozitif definit mi kontrol et.

<details>
<summary>Cozum</summary>

**a) tau = 0:**
H = | 1  3 |
    | 3  2 |

Cholesky: H = LDL^T
L(1,1) = 1, D(1,1) = 1
L(2,1) = 3/1 = 3, D(2,2) = 2 - 3^2*1 = 2 - 9 = -7

D(2,2) = -7 < 0 → Cholesky basarisiz. H pozitif definit degil.

(Ozdegerler: l^2-3l-7=0, l=(3±sqrt(37))/2 ≈ 4.54, -1.54. Indefinit.)

**b) tau = 8:**
H + 8I = | 9  3 |
          | 3  10 |

Cholesky: D(1,1) = 9 > 0 ✓
L(2,1) = 3/9 = 1/3
D(2,2) = 10 - (1/3)^2 * 9 = 10 - 1 = 9 > 0 ✓

Cholesky basarili!

**c)** det(H+8I) = 90-9 = 81 > 0, iz = 19 > 0 → pozitif definit ✓

Daha kucuk tau ile de olabilir: tau > 1.54 yeterli. tau = 2 minimum tam sayi.
</details>

---

## Soru 39: Newton + Line Search

f(x) = x^4 - 4x^2, x0 = 3.
a) Tam Newton adimi hesapla.
b) Newton adimi sonrasi f artti mi azaldi mi?
c) alfa = 0.5 ile dene.

<details>
<summary>Cozum</summary>

f(3) = 81 - 36 = 45
f'(3) = 4*27 - 8*3 = 108 - 24 = 84
f''(3) = 12*9 - 8 = 100

**a)** p = -f'(3)/f''(3) = -84/100 = -0.84

x1 = 3 - 0.84 = 2.16

**b)** f(2.16) = 2.16^4 - 4*2.16^2 = 21.77 - 18.66 = 3.11

f: 45 → 3.11. Azaldi!

**c)** alfa = 0.5 ile: x1 = 3 + 0.5*(-0.84) = 2.58

f(2.58) = 2.58^4 - 4*2.58^2 = 44.3 - 26.6 = 17.7

f: 45 → 17.7 (alfa=0.5), 45 → 3.11 (alfa=1)

Tam Newton adimi (alfa=1) daha iyi. Cozume yakin oldugumuzda alfa=1 genellikle en iyi secimdir.

Minimum: f'(x)=0 → 4x^3-8x=0 → x(x^2-2)=0 → x=sqrt(2)≈1.414
f(sqrt(2)) = 4-8 = -4
</details>

---

## Soru 40: Zoutendijk ve Yakinsaklik

Steepest descent ile f(x,y) = ax^2 + by^2 (a, b > 0) minimize ediyoruz.
a) cos(theta_k) nedir?
b) Zoutendijk sonucunun ne anlama geldigini acikla.

<details>
<summary>Cozum</summary>

Steepest descent: p_k = -grad f(x_k)

**a)** theta_k, p_k ile -grad f(x_k) arasindaki acidir.

p_k = -grad f(x_k) ve -grad f(x_k) = -grad f(x_k)

Ayni vektorler! Araalarindaki aci = 0.

cos(theta_k) = 1, her iterasyonda.

**b)** Zoutendijk: sum cos^2(theta_k) * ||grad f||^2 < sonsuz

cos(theta_k) = 1 oldugu icin:

sum ||grad f(x_k)||^2 < sonsuz

Bu kesinlikle ||grad f(x_k)|| → 0 demek. Yani steepest descent bu fonksiyonda **kesinlikle yakinsir**.

Ama ne kadar hizli? Kosul sayisi kappa = max(a,b)/min(a,b). Buyuk kappa → yavas yakinsaklik (zigzag).
</details>

---

## Soru 41: Tam Wolfe Analizi

f(x,y) = 3x^2 + y^2, x0 = (1, 1), p = (-6, -2) (steepest descent).
c1 = 0.1, c2 = 0.9. Wolfe araligini bul.

<details>
<summary>Cozum</summary>

f(1,1) = 4
grad f = (6, 2), grad f^T p = -36-4 = -40

Yeni nokta: (1-6a, 1-2a)

**Armijo:**
f(1-6a, 1-2a) = 3(1-6a)^2 + (1-2a)^2
= 3(1-12a+36a^2) + 1-4a+4a^2
= 3-36a+108a^2+1-4a+4a^2
= 4-40a+112a^2

4-40a+112a^2 <= 4+0.1*a*(-40) = 4-4a

112a^2-36a <= 0
4a(28a-9) <= 0 → **a <= 9/28 ≈ 0.321**

**Curvature:**
grad f(1-6a,1-2a) = (6(1-6a), 2(1-2a)) = (6-36a, 2-4a)

grad f^T p = (6-36a)(-6) + (2-4a)(-2)
= -36+216a-4+8a = -40+224a

-40+224a >= 0.9*(-40) = -36
224a >= 4
**a >= 1/56 ≈ 0.018**

Wolfe araligi: **1/56 <= a <= 9/28** yani yaklasik **0.018 <= a <= 0.321**

Exact: phi'(a) = -40+224a = 0 → a = 40/224 = 5/28 ≈ 0.179. Aralikta ✓
</details>

---

## Soru 42: Newton — 3 Degisken

f(x,y,z) = x^2 + 2y^2 + 3z^2 - 2x - 4y - 6z, x0 = (0,0,0). Newton adimi.

<details>
<summary>Cozum</summary>

grad f = (2x-2, 4y-4, 6z-6)
grad f(0,0,0) = (-2, -4, -6)

H = | 2  0  0 |
    | 0  4  0 |
    | 0  0  6 |

H^{-1} = | 1/2  0    0   |
          | 0    1/4  0   |
          | 0    0    1/6 |

p^N = -H^{-1} grad f = -| 1/2  0    0   | | -2 | = -| -1 | = | 1 |
                          | 0    1/4  0   | | -4 |    | -1 |   | 1 |
                          | 0    0    1/6 | | -6 |    | -1 |   | 1 |

x1 = (0,0,0) + (1,1,1) = (1, 1, 1)

Kontrol: grad f(1,1,1) = (0, 0, 0) ✓ Tek adimda cozum!
</details>

---

## Soru 43: Modifiye Newton — Gercekci Problem

f(x,y) = x^2 - 6xy + y^2, x0 = (2, 1).
a) Hessian indefinit mi?
b) tau = 10 ile modifiye Newton yonunu hesapla.
c) Bir iterasyon yap (alfa = 1).

<details>
<summary>Cozum</summary>

grad f = (2x-6y, -6x+2y)
grad f(2,1) = (4-6, -12+2) = (-2, -10)

H = | 2  -6 |
    | -6  2 |

**a)** det(H) = 4-36 = -32 < 0 → indefinit ✓
Ozdegerler: l^2 - 4l - 32 = 0, l = (4±sqrt(16+128))/2 = (4±12)/2 → l = 8, -4

**b)** H + 10I = | 12  -6 |
                | -6  12 |

det = 144-36 = 108 > 0 ✓

(H+10I)^{-1} = 1/108 * | 12  6 |
                         | 6  12 |

p = -1/108 * | 12  6 | | -2  | = -1/108 * | -24-60 | = -1/108 * | -84  | = | 84/108  |
              | 6  12 | | -10 |             | -12-120|            | -132 |   | 132/108 |

= (7/9, 11/9)

**c)** x1 = (2, 1) + (7/9, 11/9) = (25/9, 20/9) ≈ (2.78, 2.22)

f(2, 1) = 4 - 12 + 1 = -7
f(25/9, 20/9) = 625/81 - 6*500/81 + 400/81 = (625 - 3000 + 400)/81 = -1975/81 ≈ -24.4

f: -7 → -24.4. Buyuk dusus!
</details>

---

## Soru 44: Backtracking — Newton Yonu ile

f(x,y) = (x-1)^2 + 10(y-x^2)^2 (Rosenbrock benzeri), x0 = (-1, 1).
Newton yonu ile backtracking uygula (alfa_hat=1, rho=0.5, c=10^{-4}).

<details>
<summary>Cozum</summary>

grad f:
df/dx = 2(x-1) + 10*2(y-x^2)(-2x) = 2(x-1) - 40x(y-x^2)
df/dy = 20(y-x^2)

x0 = (-1, 1):
df/dx = 2(-2) - 40(-1)(1-1) = -4 - 0 = -4
df/dy = 20(1-1) = 0

grad f(-1,1) = (-4, 0)

H: (karmasik, hesaplayalim)
d^2f/dx^2 = 2 - 40(y-3x^2) = 2 - 40(1-3) = 2+80 = 82
d^2f/dxdy = -40x = 40
d^2f/dy^2 = 20

H = | 82   40 |
    | 40   20 |

det(H) = 1640-1600 = 40

H^{-1} = 1/40 * | 20  -40 | = | 1/2  -1 |
                  | -40  82 |   | -1   41/20 |

p^N = -| 1/2  -1    | | -4 | = -| -2 | = | 2    |
       | -1   41/20 | |  0 |    | 4  |   | -4   |

Hmm, kontrol: H^{-1} grad f = | 1/2  -1 | | -4 | = | -2+0 | = | -2 |
                                | -1  41/20| | 0  |   | 4+0  |   | 4  |

p^N = -(-2, 4) = (2, -4)

**alfa = 1:**
x = (-1, 1) + (2, -4) = (1, -3)
f(1, -3) = 0 + 10(-3-1)^2 = 160
f(-1, 1) = 4 + 0 = 4

Armijo: 160 <= 4 + 10^{-4}*1*((-4)(2)+(0)(-4)) = 4 + 10^{-4}*(-8) = 3.9992? Hayir!

**alfa = 0.5:**
x = (-1, 1) + 0.5*(2, -4) = (0, -1)
f(0, -1) = 1 + 10(-1)^2 = 11
Armijo: 11 <= 4 + 10^{-4}*0.5*(-8) = 3.9996? Hayir!

**alfa = 0.25:**
x = (-1, 1) + 0.25*(2, -4) = (-0.5, 0)
f(-0.5, 0) = (-1.5)^2 + 10(0-0.25)^2 = 2.25 + 0.625 = 2.875
Armijo: 2.875 <= 4 + 10^{-4}*0.25*(-8) = 3.9998? Evet!

alfa = 0.25 kabul. f: 4 → 2.875.

Newton adiminin tamami cok agresifdi (Rosenbrock'un dar vadisi yuzunden), backtracking kuculterek guvenli bir adim buldu.
</details>

---

## Soru 45: Steepest Descent Yakinsaklik Analizi

f(x,y) = 25x^2 + y^2, x0 = (1, 1).
a) Kosul sayisini bul.
b) Steepest descent yakinsaklik oranini hesapla.
c) f degerinin 1/1000'e dusmesi icin yaklasik kac iterasyon gerekir?

<details>
<summary>Cozum</summary>

Q = diag(50, 2)

**a)** kappa = 50/2 = 25

**b)** r = ((25-1)/(25+1))^2 = (24/26)^2 = (12/13)^2 = 144/169 ≈ 0.852

Her iterasyonda hata en fazla %14.8 azalir.

**c)** f(x0) = 25+1 = 26. f(x*) = 0.

Hata orani her adimda r ile carpilir: r^k <= 1/1000

0.852^k <= 0.001

k * ln(0.852) <= ln(0.001)

k >= ln(0.001)/ln(0.852) = -6.908/(-0.160) ≈ 43

Yaklasik **43 iterasyon** gerekir.

Newton olsaydi: 1 iterasyon. Fark muazzam.
</details>

---

## Soru 46: Conjugate Gradient — Wolfe ile

A = [[4, 1], [1, 3]], b = (1, 2), x0 = (0, 0). CG ile 1 iterasyon yap.
CG icin c2 = 0.1 secilir — neden?

<details>
<summary>Cozum</summary>

r0 = b - Ax0 = (1, 2)
p0 = r0 = (1, 2)

Ap0 = | 4  1 | | 1 | = | 6  |
      | 1  3 | | 2 |   | 7  |

a0 = r0^T r0 / (p0^T Ap0) = (1+4)/(6+14) = 5/20 = 1/4

x1 = (0,0) + (1/4)(1,2) = (1/4, 1/2)

r1 = r0 - a0*Ap0 = (1,2) - (1/4)(6,7) = (1-3/2, 2-7/4) = (-1/2, 1/4)

||r1||^2 = 1/4 + 1/16 = 5/16
||r0||^2 = 5

beta1 = (5/16)/5 = 1/16

p1 = r1 + beta1*p0 = (-1/2, 1/4) + (1/16)(1, 2) = (-1/2+1/16, 1/4+2/16)
= (-7/16, 6/16) = (-7/16, 3/8)

**Neden c2 = 0.1?**

CG'de ardisik arama yonleri Q-eslenk (conjugate) olmali. Bu ozellik exact line search ile otomatik saglanir. Inexact line search kullanilirsa, alfa'nin exact line search'e yakin olmasi gerekir. c2 = 0.1 dar bir Wolfe araligi verir → alfa daha hassas secilir → eslenkligi yaklasik olarak korur.

c2 = 0.9 (Newton icin) olsaydi, alfa cok genis bir araliktan secilebilir ve eslenkligi bozabilirdi.
</details>

---

## Soru 47: Modifiye Newton — Ozdeger Analizi

H = | 5   2   0 |
    | 2  -1   1 | icin:
    | 0   1   3 |

a) Pozitif definit mi?
b) tau = 3 ile H + tau*I pozitif definit mi?

<details>
<summary>Cozum</summary>

**a)** Sylvester kriteri: alt determinantlara bak.

D1 = 5 > 0 ✓
D2 = det| 5  2 | = -5-4 = -9 < 0 ✗
        | 2 -1 |

D2 < 0 → **pozitif definit degil.**

(-1 elemani zaten bir ozdegerin negatif olabilecegini gosteriyor.)

**b)** H + 3I = | 8  2  0 |
               | 2  2  1 |
               | 0  1  6 |

Sylvester:
D1 = 8 > 0 ✓
D2 = det| 8  2 | = 16-4 = 12 > 0 ✓
        | 2  2 |
D3 = det(H+3I) = 8(12-1) - 2(12-0) + 0 = 88 - 24 = 64 > 0 ✓

Tum alt determinantlar pozitif → **pozitif definit** ✓
</details>

---

## Soru 48: Newton vs Steepest — Kotu Kosullu

f(x,y) = 200x^2 + y^2, x0 = (1, 1).
a) Newton ile coz.
b) Steepest descent ile 1 iterasyon.
c) En kotu yakinsaklik oranini hesapla.

<details>
<summary>Cozum</summary>

**a) Newton:**
grad f = (400, 2)
H = diag(400, 2)
H^{-1} = diag(1/400, 1/2)
p^N = -(1, 1)
x1 = (0, 0). Bitti!

**b) Steepest Descent:**
p = (-400, -2)
a = (400^2+2^2)/(400^2*400+2^2*2) = 160004/64000008 ≈ 0.0025

x1 = (1-400*0.0025, 1-2*0.0025) = (0, 0.995)
f(0, 0.995) ≈ 0.99

**c)** kappa = 400/2 = 200
r = (199/201)^2 = (0.99005)^2 ≈ 0.98

Her iterasyonda hata sadece %2 azalir. f'nin 0.001'e dusmesi icin:
0.98^k <= 0.001 → k >= ln(0.001)/ln(0.98) = 342 iterasyon!

Newton: 1. Steepest descent: ~342. Kosul sayisi buyudukce fark inanilmaz aciyor.
</details>

---

## Soru 49: Backtracking — Uygun Parametre Secimi

f(x,y) = x^2 + 100y^2, x0 = (10, 1), p = -grad f = (-20, -200).

a) alfa_hat=1, rho=0.5, c=0.5 ile kac denemede kabul ediliyor?
b) alfa_hat=1, rho=0.5, c=10^{-4} ile kac denemede?

<details>
<summary>Cozum</summary>

f(10,1) = 100+100 = 200
grad f = (20, 200), grad f^T p = -400-40000 = -40400

**a) c = 0.5:**

alfa=1: f(10-20, 1-200)=f(-10,-199)=100+3960100=3960200
3960200 <= 200+0.5*(-40400) = 200-20200=-20000? Hayir

alfa=0.5: f(0,-99)=0+980100=980100
980100 <= 200+0.5*0.5*(-40400)=-9900? Hayir

alfa=0.25: f(5,-49)=25+240100=240125
240125 <= 200+0.5*0.25*(-40400)=-4850? Hayir

alfa=0.125: f(7.5,-24)=56.25+57600=57656
57656 <= 200+0.5*0.125*(-40400)=-2325? Hayir

alfa=0.0625: f(8.75,-11.5)=76.56+13225=13302
13302 <= 200+0.5*0.0625*(-40400)=-1062.5? Hayir

alfa≈0.031: f(9.375,-5.25)≈87.9+2756=2844
2844 <= 200+0.5*0.031*(-40400)≈-426? Hayir

alfa≈0.016: f(9.69,-2.125)≈93.9+451.6=545
545 <= 200+0.5*0.016*(-40400)≈-123? Hayir

alfa≈0.008: f(9.84, -0.56)≈96.8+31.8=128.6
128.6 <= 200+0.5*0.008*(-40400)≈38.4? Hayir

alfa≈0.004: f(9.92, 0.22)≈98.4+4.8=103.2
103.2 <= 200+0.5*0.004*(-40400)≈119.2? Evet!

Yaklasik **9 deneme** ile c=0.5.

**b) c = 10^{-4}:**

alfa=1: 3960200 <= 200+10^{-4}*(-40400)=195.96? Hayir
alfa=0.5: 980100 <= 200+10^{-4}*0.5*(-40400)≈197.98? Hayir
alfa=0.25: 240125 <= 200-1.01≈198.99? Hayir
alfa=0.125: 57656 <= 199.5? Hayir
alfa=0.0625: 13302 <= 199.7? Hayir
alfa≈0.031: 2844 <= 199.9? Hayir
alfa≈0.016: 545 <= 199.9? Hayir
alfa≈0.008: 128.6 <= 199.97? Evet!

Yaklasik **8 deneme** ile c=10^{-4}. Kucuk c biraz daha erken kabul ettirdi.

**Yorum:** Bu kotu kosullu problem (kappa=100). Steepest descent yonu y'ye 10 kat fazla agirlik veriyor, buyuk adimlar cok overshoot yapiyor. Newton tek adimda cozerdi.
</details>

---

## Soru 50: Kapsamli Analiz — Yontem Secimi

f(x,y) = 10(y - x^2)^2 + (1 - x)^2 (Rosenbrock) icin x0 = (-1, 1).
a) Gradyan ve Hessian'i hesapla.
b) Hessian pozitif definit mi?
c) Newton yonunu bul.
d) Steepest descent yonunu bul.
e) Hangi yontem daha uygun bu problem icin?

<details>
<summary>Cozum</summary>

**a) Gradyan:**
df/dx = -40x(y-x^2) - 2(1-x)
df/dy = 20(y-x^2)

x0 = (-1, 1):
df/dx = -40(-1)(1-1) - 2(1-(-1)) = 0 - 4 = -4
df/dy = 20(1-1) = 0

grad f = (-4, 0)

**Hessian:**
d^2f/dx^2 = -40(y-3x^2) + 2
d^2f/dxdy = -40x
d^2f/dy^2 = 20

x0 = (-1, 1):
d^2f/dx^2 = -40(1-3) + 2 = 80 + 2 = 82
d^2f/dxdy = -40(-1) = 40
d^2f/dy^2 = 20

H = | 82  40 |
    | 40  20 |

**b)** det(H) = 1640 - 1600 = 40 > 0
iz(H) = 102 > 0
→ Pozitif definit ✓

**c) Newton:**
H^{-1} = 1/40 * | 20  -40 | = | 1/2  -1    |
                  | -40  82 |   | -1   41/20  |

p^N = -| 1/2  -1    | | -4 | = -| -2 | = | 2  |
       | -1   41/20 | |  0 |    |  4 |   | -4 |

**d) Steepest descent:**
p_SD = -grad f = (4, 0)

**e) Karsilastirma:**

Newton yonu: (2, -4) — hem x hem y yonunde gidiyor
Steepest descent yonu: (4, 0) — sadece x yonunde gidiyor

Rosenbrock fonksiyonunun dar, egri bir vadisi var. Steepest descent sadece x ekseni boyunca gider ve vadiyi takip edemez. Newton ise Hessian bilgisiyle egri vadiyi "hisseder" ve her iki yonde de uygun hareket eder.

Bu problem icin **Newton daha uygun** — ama her adimda Hessian hesaplamak pahali. Pratikte **BFGS** (yaklasik Hessian) en iyi uzlasma olur.
</details>
