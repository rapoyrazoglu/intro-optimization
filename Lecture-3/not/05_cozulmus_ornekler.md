# 5. Cozulmus Ornekler

---

## Ornek 1: Steepest Descent + Exact Line Search

**Soru:** f(x1, x2) = (x1 - 1)^2 + (x2 - 1)^2 fonksiyonunu steepest descent ile minimize et. Baslangic noktasi x0 = (1, 2).

**Cozum:**

Bu fonksiyon "merkezden uzakligin karesi" — minimum noktasi (1, 1) oldugu acik.

**Adim 1: Gradyani hesapla**

grad f(x) = (2(x1 - 1), 2(x2 - 1))

- Sol eleman: f'yi x1'e gore turevle → 2(x1 - 1)
- Sag eleman: f'yi x2'ye gore turevle → 2(x2 - 1)

x0 = (1, 2) noktasinda:

grad f(1, 2) = (2(1-1), 2(2-1)) = (0, 2)

**Adim 2: Yon sec (negatif gradyan)**

p0 = -grad f = (0, -2)

Yani sadece x2 yonunde asagi gidecegiz (x1 yonunde zaten egim sifir).

**Adim 3: Exact line search — alfa bul**

Yeni nokta: x0 + alfa * p0 = (1, 2) + alfa * (0, -2) = (1, 2 - 2*alfa)

Fonksiyona koyalim:

phi(alfa) = f(1, 2 - 2*alfa) = (1-1)^2 + (2 - 2*alfa - 1)^2 = (1 - 2*alfa)^2

Turev al, sifira esitle:

phi'(alfa) = 2(1 - 2*alfa)(-2) = -4(1 - 2*alfa) = 0

1 - 2*alfa = 0 → **alfa = 1/2**

**Adim 4: Yeni noktayi hesapla**

x1 = (1, 2) + (1/2)(0, -2) = (1, 1)

**Kontrol:** grad f(1, 1) = (0, 0) → Cozum bulundu! Tek iterasyonda bitti.

f(1, 2) = 1 → f(1, 1) = 0. Fonksiyon 1'den 0'a dustu.

---

## Ornek 2: Newton Yontemi — Ayni Problem

**Soru:** Ornek 1'deki fonksiyonu x0 = (1/2, 2) noktasindan Newton yontemi ile coz.

**Cozum:**

**Adim 1: Gradyan ve Hessian**

grad f(x) = (2(x1-1), 2(x2-1))

grad f(1/2, 2) = (2(1/2 - 1), 2(2-1)) = (-1, 2)

Hessian: her kismi turevin turevi:

H = | d^2f/dx1^2    d^2f/dx1dx2 |   = | 2  0 |
    | d^2f/dx2dx1   d^2f/dx2^2  |     | 0  2 |

Sabit matris — noktadan bagimsiz.

**Adim 2: Hessian'in tersini al**

H^{-1} = | 1/2   0  |
          |  0   1/2 |

**Adim 3: Newton yonunu hesapla**

p^N = -H^{-1} * grad f = -| 1/2  0  | * | -1 | = -| -1/2 | = | 1/2  |
                            |  0  1/2 |   |  2 |    |  1   |   | -1   |

**Adim 4: Yeni noktayi hesapla (alfa = 1)**

Newton yonteminde genellikle alfa = 1 ile baslanir:

x1 = (1/2, 2) + 1 * (1/2, -1) = (1, 1)

**Kontrol:** grad f(1, 1) = (0, 0) → Tek adimda cozum! Bu beklenen bir sonuc cunku fonksiyon kuadratik.

---

## Ornek 3: Backtracking Line Search

**Soru:** Ornek 1'deki fonksiyonu backtracking line search ile coz. Parametreler: alfa_hat = 3/4, rho = 1/5, c = 1/3. x0 = (1, 2).

**Cozum:**

Onceki ornekten biliyoruz:
- grad f(1, 2) = (0, 2)
- p0 = (0, -2)
- f(1, 2) = 1

Armijo sabitleri:
- grad f^T * p = (0)(0) + (2)(-2) = -4

**Deneme 1: alfa = 3/4**

Yeni nokta: (1, 2) + (3/4)(0, -2) = (1, 1/2)

Sol taraf: f(1, 1/2) = 0 + (1/2 - 1)^2 = 1/4

Sag taraf: f(x0) + c * alfa * grad f^T * p = 1 + (1/3)(3/4)(-4) = 1 - 1 = 0

Armijo: 1/4 <= 0? **Hayir!** → alfa'yi kucult.

**Deneme 2: alfa = (3/4) * (1/5) = 3/20**

Yeni nokta: (1, 2) + (3/20)(0, -2) = (1, 2 - 3/10) = (1, 17/10)

Sol taraf: f(1, 17/10) = (17/10 - 1)^2 = (7/10)^2 = 49/100

Sag taraf: 1 + (1/3)(3/20)(-4) = 1 - 4/20 = 1 - 1/5 = 4/5

Armijo: 49/100 <= 4/5 = 80/100? **Evet!** → alfa = 3/20 kabul.

x1 = (1, 17/10)

f degeri: 1 → 0.49. Azaldi ama optimal degil. Devam etmek lazim.

**Gozlem:** Exact line search alfa = 1/2 bulmustu ve tek adimda cozume gitmisti. Backtracking daha kucuk adim atti (3/20 = 0.15) cunku parametreler bunu zorluyor.

---

## Ornek 4: Wolfe Kosullari Kontrolu — Sufficient Decrease

**Soru:** f(x, y) = 4x^2 - 4xy + 2y^2, steepest descent, x0 = (2, 3).
Armijo kosulunu (c1 = 0.5) saglayan alfa araligini bul.

**Cozum:**

grad f = (8x - 4y, -4x + 4y)
grad f(2, 3) = (16 - 12, -8 + 12) = (4, 4)

p0 = -(4, 4) = (-4, -4)

f(2, 3) = 4(4) - 4(6) + 2(9) = 16 - 24 + 18 = 10

grad f^T * p = (4)(-4) + (4)(-4) = -32

**Armijo kosulu:** f(x0 + alfa * p) <= f(x0) + c1 * alfa * grad f^T * p

Yeni nokta: (2 - 4*alfa, 3 - 4*alfa)

Sol taraf: f(2-4a, 3-4a)
= 4(2-4a)^2 - 4(2-4a)(3-4a) + 2(3-4a)^2

Parcalayalim:
- 4(2-4a)^2 = 4(4 - 16a + 16a^2) = 16 - 64a + 64a^2
- -4(2-4a)(3-4a) = -4(6 - 8a - 12a + 16a^2) = -24 + 80a - 64a^2
- 2(3-4a)^2 = 2(9 - 24a + 16a^2) = 18 - 48a + 32a^2

Toplam: 10 - 32a + 32a^2

Sag taraf: 10 + 0.5 * alfa * (-32) = 10 - 16*alfa

**Esitsizlik:**

10 - 32a + 32a^2 <= 10 - 16a

32a^2 - 32a + 16a <= 0

32a^2 - 16a <= 0

16a(2a - 1) <= 0

a >= 0 oldugunda: 2a - 1 <= 0 → **a <= 1/2**

**Sonuc:** Armijo kosulu **0 < alfa <= 1/2** icin saglaniyor.

Bunun anlami: adim boyu 1/2'den buyuk olursa, fonksiyon yeterince azalmamis demektir.

---

## Ornek 5: Wolfe Kosullari Kontrolu — Curvature Condition

**Soru:** Ornek 4'te curvature kosulunu (c2 = 0.1) saglayan alfa araligini bul.

**Cozum:**

Curvature kosulu: grad f(x0 + alfa * p)^T * p >= c2 * grad f(x0)^T * p

Once grad f(yeni nokta) hesaplayalim:

Yeni nokta: (2 - 4a, 3 - 4a)

grad f = (8x - 4y, -4x + 4y)

grad f(2-4a, 3-4a) = (8(2-4a) - 4(3-4a), -4(2-4a) + 4(3-4a))
= (16 - 32a - 12 + 16a, -8 + 16a + 12 - 16a)
= (4 - 16a, 4)

Sol taraf: grad f(yeni)^T * p = (4-16a)(-4) + (4)(-4) = -16 + 64a - 16 = -32 + 64a

Sag taraf: c2 * grad f(x0)^T * p = 0.1 * (-32) = -3.2

Esitsizlik: -32 + 64a >= -3.2

64a >= 28.8

**a >= 28.8/64 = 0.45**

**Sonuc:** Curvature kosulu **alfa >= 0.45** icin saglaniyor.

---

## Ornek 6: Wolfe Kosullarinin Kesisimi

**Soru:** Ornek 4 ve 5'in sonuclarini birlestir. Hangi alfa degerleri **iki** Wolfe kosulunu birden saglar?

**Cozum:**

- Armijo (sufficient decrease): alfa <= 1/2 = 0.5
- Curvature: alfa >= 0.45

Kesisim: **0.45 <= alfa <= 0.5**

Bu araliktaki herhangi bir alfa, ornegin alfa = 0.45, 0.48, veya 0.5, iki kosulu birden saglar.

**Grafiksel gosterim:**

```
0         0.45     0.5         1
|__________|=========|__________|
           Wolfe ok
```

Exact line search alfa = 0.5 vermisti — Wolfe araliginin ust sinirina denk geliyor. Bu mantikli cunku exact line search optimali buluyor ve curvature kosulunun ust siniri da o noktada saglaniyor.

---

## Ornek 7: Wolfe Kosullari — Baska Fonksiyon

**Soru:** f(x1, x2) = (x1-1)^2 + (x2-1)^2, x0 = (0, 0), steepest descent.
c1 = 0.5, c2 = 0.1 icin Wolfe kosullarini saglayan alfa araligini bul.

**Cozum:**

grad f(0, 0) = (-2, -2)
p0 = (2, 2)
f(0, 0) = 1 + 1 = 2
grad f^T * p = (-2)(2) + (-2)(2) = -8

Yeni nokta: (2a, 2a)

**Armijo:**
f(2a, 2a) = (2a-1)^2 + (2a-1)^2 = 2(2a-1)^2

2(2a-1)^2 <= 2 + 0.5 * a * (-8) = 2 - 4a

2(4a^2 - 4a + 1) <= 2 - 4a
8a^2 - 8a + 2 <= 2 - 4a
8a^2 - 4a <= 0
4a(2a - 1) <= 0

a > 0 icin: **a <= 1/2**

**Curvature:**
grad f(2a, 2a) = (2(2a-1), 2(2a-1)) = (4a-2, 4a-2)

grad f(yeni)^T * p = (4a-2)(2) + (4a-2)(2) = 4(4a-2) = 16a - 8

16a - 8 >= 0.1 * (-8) = -0.8

16a >= 7.2

**a >= 0.45**

**Wolfe araligi: 0.45 <= alfa <= 0.5**

Exact line search: phi(a) = 2(2a-1)^2, phi'(a) = 8(2a-1) = 0 → a = 1/2

Yine alfa = 0.5 = exact line search sonucu Wolfe araliginin icinde.

---

## Ornek 8: Steepest Descent + Exact Line Search — Kuadratik

**Soru:** f(x) = (1/2) x^T Q x - b^T x ile Q = [[5, -3], [-3, 2]], b = (0, 1).
x0 = (0, 0). Exact line search ile 1 iterasyon uygula.

**Cozum:**

Bu ozel kuadratik formda gradyan soyle hesaplanir:

grad f(x) = Q*x - b

Neden? (1/2)x^T Q x'in turevi Qx, -b^T x'in turevi -b. Toplam: Qx - b.

grad f(0, 0) = Q * (0,0) - (0, 1) = (0, -1)

Yon: p0 = -grad f = (0, 1)

**Exact line search formulu (kuadratik icin):**

alfa = (grad f^T * grad f) / (grad f^T * Q * grad f)

Bu formul nereden geliyor? phi(alfa) = f(x + alfa*p) kuadratik, turevini sifira esitleyince bu cikiyor.

Pay: grad f^T * grad f = (0)^2 + (-1)^2 = 1

Q * grad f = | 5  -3 | | 0  | = | 3  |
             | -3  2 | | -1 |   | -2 |

Payda: grad f^T * Q * grad f = (0)(3) + (-1)(-2) = 2

alfa = 1/2

x1 = (0, 0) + (1/2)(0, 1) = (0, 1/2)

**Kontrol:**

grad f(0, 1/2) = Q*(0, 1/2) - (0, 1) = (-3/2, 1) - (0, 1) = (-3/2, 0)

Gradyan sifir degil → henuz bitmedi, devam etmek lazim.

f(0, 0) = 0 - 0 = 0
f(0, 1/2) = (1/2)(0, 1/2) Q (0, 1/2)^T - (0,1)(0,1/2)^T = (1/2)(1/2) - 1/2 = 1/4 - 1/2 = -1/4

f: 0 → -1/4. Azaldi.

---

## Ornek 9: Newton Yontemi — Kuadratik

**Soru:** Ornek 8'deki fonksiyonu x0 = (0, 0) noktasindan Newton yontemi ile coz.

**Cozum:**

grad f(0, 0) = (0, -1)

Hessian: H = Q = | 5  -3 |
                  | -3  2 |

(Kuadratik fonksiyonda Hessian her yerde ayni ve Q'ya esit.)

H^{-1}: 2x2 matrisin tersi icin formul: | a  b |^{-1} = 1/(ad-bc) * |  d  -b |
                                          | c  d |                     | -c   a |

det(H) = 5*2 - (-3)(-3) = 10 - 9 = 1

H^{-1} = | 2   3 |
          | 3   5 |

Newton yonu: p^N = -H^{-1} * grad f = -| 2  3 | | 0  | = -| -3 | = | 3 |
                                         | 3  5 | | -1 |    | -5 |   | 5 |

alfa = 1 ile: x1 = (0, 0) + (3, 5) = (3, 5)

**Kontrol:** grad f(3, 5) = Q*(3,5) - (0,1) = (15-15, -9+10) - (0,1) = (0, 1) - (0, 1) = (0, 0) ✓

**Tek adimda cozum!** Newton kuadratik fonksiyonlari her zaman 1 adimda cozer.

---

## Ornek 10: Modifiye Newton — Indefinit Hessian

**Soru:** f(x,y) = x^2 - 4y^2 + 6x fonksiyonunda x0 = (0, 1) noktasinda:
a) Normal Newton yonunun inis yonu olup olmadigini kontrol et.
b) Diagonal shift (tau = 10) ile modifiye Newton yonunu bul.

**Cozum:**

grad f = (2x + 6, -8y)
grad f(0, 1) = (6, -8)

H = | 2    0 |
    | 0   -8 |

**a) Normal Newton:**

H^{-1} = | 1/2   0    |
          |  0   -1/8  |

p^N = -H^{-1} * grad f = -| 1/2   0    | | 6  | = -| 3 | = | -3 |
                            |  0   -1/8  | | -8 |    | 1 |   | -1 |

Inis yonu kontrolu: p^T * grad f = (-3)(6) + (-1)(-8) = -18 + 8 = -10 < 0

Inis yonu — bu ornekte calisiyor! Ama Hessian indefinit (ozdegerler 2 ve -8), yani Newton yonu her zaman guvenilir degil.

**b) Modifiye Newton (tau = 10):**

H + tau*I = | 2+10    0    | = | 12   0 |
            |   0   -8+10  |   |  0   2 |

Pozitif definit mi? Ozdegerler 12, 2 — evet!

(H + tau*I)^{-1} = | 1/12   0   |
                    |   0   1/2  |

p = -(H+tau*I)^{-1} * grad f = -| 1/12   0  | | 6  | = -| 1/2 | = | -1/2 |
                                  |  0    1/2 | | -8 |    | -4  |   |  4   |

Inis yonu kontrolu: p^T * grad f = (-1/2)(6) + (4)(-8) = -3 - 32 = -35 < 0 ✓

**Karsilastirma:**

| | Normal Newton | Modifiye Newton |
|--|---------------|-----------------|
| Yon | (-3, -1) | (-0.5, 4) |
| p^T grad f | -10 | -35 |

Modifiye Newton daha "dik" bir inis yonu veriyor (daha negatif ic carpim).

---

## Ornek 11: Backtracking — Cok Adimli

**Soru:** f(x,y) = x^2 + 4y^2, x0 = (4, 2), steepest descent.
Backtracking parametreleri: alfa_hat = 1, rho = 0.5, c = 0.25.
Kabul edilen alfa'yi bul.

**Cozum:**

grad f(4, 2) = (8, 16)
p0 = (-8, -16)
f(4, 2) = 16 + 16 = 32
grad f^T * p = (8)(-8) + (16)(-16) = -64 - 256 = -320

**alfa = 1:**
x = (4-8, 2-16) = (-4, -14)
f(-4, -14) = 16 + 784 = 800
Armijo: 800 <= 32 + 0.25*1*(-320) = 32 - 80 = -48? **Hayir**

**alfa = 0.5:**
x = (4-4, 2-8) = (0, -6)
f(0, -6) = 0 + 144 = 144
Armijo: 144 <= 32 + 0.25*0.5*(-320) = 32 - 40 = -8? **Hayir**

**alfa = 0.25:**
x = (4-2, 2-4) = (2, -2)
f(2, -2) = 4 + 16 = 20
Armijo: 20 <= 32 + 0.25*0.25*(-320) = 32 - 20 = 12? **Hayir**

**alfa = 0.125:**
x = (4-1, 2-2) = (3, 0)
f(3, 0) = 9
Armijo: 9 <= 32 + 0.25*0.125*(-320) = 32 - 10 = 22? **Evet!**

alfa = 0.125 kabul edildi. f: 32 → 9.

**Yorum:** Neden 3 kere reddedildi? Cunku steepest descent yonu (-8, -16) cok agresif — x2 yonundeki gradyan buyuk ve uzun adim atinca overshoot yapiyor.

---

## Ornek 12: Diagonal Shift — tau Secimi

**Soru:** H = [[-2, 1], [1, -3]] Hessian'i icin, H + tau*I'nin pozitif definit olmasini saglayan minimum tam sayi tau degerini bul.

**Cozum:**

H'nin ozdegerlerini bulalim:

det(H - lambda*I) = (-2-l)(-3-l) - 1 = l^2 + 5l + 5 = 0

l = (-5 ± sqrt(25-20))/2 = (-5 ± sqrt(5))/2

l1 = (-5 + 2.24)/2 = -1.38
l2 = (-5 - 2.24)/2 = -3.62

Her iki ozdeger de negatif.

H + tau*I'nin ozdegerleri: -1.38 + tau, -3.62 + tau

Ikisi de pozitif olmali:
-3.62 + tau > 0 → tau > 3.62

Minimum tam sayi: **tau = 4**

Kontrol: H + 4I = [[2, 1], [1, 1]]
det = 2 - 1 = 1 > 0, iz = 3 > 0 → pozitif definit ✓

---

## Ornek 13: Steepest Descent — 2 Iterasyon (Kuadratik)

**Soru:** f(x) = (1/2) x^T Q x - b^T x, Q = [[5,-3],[-3,2]], b = (0,1), x0 = (0,0).
2 iterasyon exact line search ile steepest descent uygula.

**Cozum:**

**Iterasyon 0:** (Ornek 8'den)

grad f(0,0) = (0, -1), p0 = (0, 1)
alfa0 = 1/2
x1 = (0, 1/2)

**Iterasyon 1:**

grad f(0, 1/2) = Q*(0, 1/2) - b = (-3/2, 1) - (0, 1) = (-3/2, 0)

p1 = (3/2, 0)

alfa1 = (grad f^T * grad f) / (grad f^T * Q * grad f)

grad f^T * grad f = (-3/2)^2 + 0 = 9/4

Q * grad f = | 5  -3 | | -3/2 | = | -15/2 |
             | -3  2 | |  0   |   |  9/2  |

grad f^T * Q * grad f = (-3/2)(-15/2) + (0)(9/2) = 45/4

alfa1 = (9/4) / (45/4) = 9/45 = 1/5

x2 = (0, 1/2) + (1/5)(3/2, 0) = (3/10, 1/2)

grad f(3/10, 1/2) = Q*(3/10, 1/2) - b = (3/2 - 3/2, -9/10 + 1) - (0, 1) = (0, 1/10) - (0, 1) = (0, -9/10)

||grad f|| = 9/10, henuz sifir degil ama azaliyor (1 → 9/10).

Tam cozum: Ax = b → x* = Q^{-1} b = | 2  3 | | 0 | = | 3 |
                                       | 3  5 | | 1 |   | 5 |

x* = (3, 5). Daha cok yolumuz var!

---

## Ornek 14: Newton — Tek Adimda Kuadratik Cozum

**Soru:** Ornek 13'teki fonksiyonu Newton ile coz. x0 = (0, 0).

**Cozum:**

Ornek 9'da zaten cozduk: x1 = (3, 5), tek adimda bitti.

Bu, Newton'un kuadratik fonksiyonlardaki gucunu gosterir: steepest descent 2 iterasyonda hala uzaktayken, Newton tek adimda exact cozume ulasti.

| | Steepest Descent (2 iter.) | Newton (1 iter.) |
|--|---------------------------|-----------------|
| x_son | (3/10, 1/2) | (3, 5) = x* |
| ||grad f|| | 9/10 | 0 |
| Bitti mi? | Hayir | **Evet** |
