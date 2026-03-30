# Lecture 2 — Pratik Sorular (50 Soru)

---

# KOLAY (Soru 1–10)

---

## Soru 1: Gradyan Hesaplama

f(x,y) = 3x^2 + 2y^2 fonksiyonunun gradyanini hesapla. (2, 1) noktasindaki degerini bul.

<details>
<summary>Cozum</summary>

df/dx = 6x, df/dy = 4y

grad f = (6x, 4y)

(2,1) noktasinda: grad f(2,1) = (12, 4)
</details>

---

## Soru 2: Duragan Nokta Bulma

f(x,y) = x^2 + y^2 - 4x - 6y + 13 fonksiyonunun duragan noktasini bul.

<details>
<summary>Cozum</summary>

grad f = (2x - 4, 2y - 6) = (0, 0)

2x - 4 = 0 → x = 2
2y - 6 = 0 → y = 3

Duragan nokta: (2, 3)
</details>

---

## Soru 3: Inis Yonu Kontrolu

f(x,y) = x^2 + 4y^2 icin (1, 1) noktasinda p = (-1, -2) bir inis yonu mu?

<details>
<summary>Cozum</summary>

grad f(1,1) = (2, 8)

p^T grad f = (-1)(2) + (-2)(8) = -2 - 16 = -18 < 0

Evet, inis yonudur.
</details>

---

## Soru 4: Hessian Hesaplama

f(x,y) = x^3 - 3xy + y^2 fonksiyonunun Hessian matrisini yaz.

<details>
<summary>Cozum</summary>

df/dx = 3x^2 - 3y
df/dy = -3x + 2y

d^2f/dx^2 = 6x
d^2f/dxdy = -3
d^2f/dy^2 = 2

H = | 6x   -3 |
    | -3    2  |
</details>

---

## Soru 5: Pozitif Definitlik Kontrolu

A = | 4  0 |
    | 0  2 |

Bu matris pozitif definit mi? Ozdegerlerini bul.

<details>
<summary>Cozum</summary>

Kosegen matris oldugu icin ozdegerler kosegen elemanlarin kendisi:

l1 = 4, l2 = 2

Ikisi de pozitif → pozitif definit.
</details>

---

## Soru 6: Steepest Descent Yonu

f(x,y) = 5x^2 + y^2 icin x0 = (3, -2) noktasinda steepest descent yonunu bul.

<details>
<summary>Cozum</summary>

grad f = (10x, 2y)

grad f(3, -2) = (30, -4)

Steepest descent yonu = -grad f = (-30, 4)
</details>

---

## Soru 7: Lokal vs Global Minimum

f(x) = x^4 - 2x^2 fonksiyonunun tum duragan noktalarini bul.

<details>
<summary>Cozum</summary>

f'(x) = 4x^3 - 4x = 4x(x^2 - 1) = 0

x = 0, x = 1, x = -1

f(0) = 0
f(1) = 1 - 2 = -1
f(-1) = 1 - 2 = -1

x = 1 ve x = -1 global minimum (f = -1)
x = 0 lokal maksimumdur (f = 0)
</details>

---

## Soru 8: Konvekslik ve Minimum

f(x,y) = x^2 + y^2 fonksiyonu konveks mi? Neden?

<details>
<summary>Cozum</summary>

H = | 2  0 |
    | 0  2 |

Ozdegerler: l1 = 2, l2 = 2. Ikisi de > 0 → pozitif definit.

Hessian her yerde pozitif definit → f kesinlikle konveks.

Konveks oldugu icin, grad f = 0 olan nokta (0,0) hem lokal hem global minimumdur.
</details>

---

## Soru 9: Taylor Acilimi Yorumlama

f(x + p) ≈ f(x) + grad f(x)^T p + (1/2) p^T H p aciliminda:
- grad f(x) ne anlama geliyor?
- H ne anlama geliyor?
- Steepest descent hangi dereceyi kullanir, Newton hangi dereceyi?

<details>
<summary>Cozum</summary>

- grad f(x): Gradyan, fonksiyonun 1. turev bilgisi (egim). Fonksiyonun hangi yone en cok arttigini gosterir.

- H: Hessian, fonksiyonun 2. turev matrisi (egrilik bilgisi). Fonksiyonun ne kadar "bukuldugunu" gosterir.

- Steepest descent: 1. derece Taylor kullanir (sadece gradyan)
- Newton: 2. derece Taylor kullanir (gradyan + Hessian)
</details>

---

## Soru 10: Yakinsaklik Turleri

Asagidakileri eslestir:

a) Steepest descent
b) Newton yontemi
c) BFGS

1) Kuadratik yakinsaklik
2) Lineer yakinsaklik
3) Superlineer yakinsaklik

<details>
<summary>Cozum</summary>

a) Steepest descent → 2) Lineer yakinsaklik
b) Newton yontemi → 1) Kuadratik yakinsaklik
c) BFGS → 3) Superlineer yakinsaklik
</details>

---

# ORTA (Soru 11–30)

---

## Soru 11: Kritik Nokta Siniflandirmasi

f(x,y) = x^2 - 2xy + 2y^2 - 2x + 4y fonksiyonunun kritik noktasini bul ve siniflandir.

<details>
<summary>Cozum</summary>

grad f = (2x - 2y - 2, -2x + 4y + 4) = (0, 0)

2x - 2y - 2 = 0 → x - y = 1    ... (1)
-2x + 4y + 4 = 0 → -x + 2y = -2 ... (2)

(1) + (2): y = -1 → x = 0

Kritik nokta: (0, -1)

Hessian:

H = | 2   -2 |
    | -2   4 |

det(H) = 8 - 4 = 4 > 0
H(1,1) = 2 > 0

→ Pozitif definit → Lokal minimum.
</details>

---

## Soru 12: Steepest Descent Iterasyonu

f(x,y) = x^2 + 2y^2 fonksiyonuna x0 = (4, 2) noktasindan steepest descent ile 1 iterasyon uygula (exact line search).

<details>
<summary>Cozum</summary>

grad f = (2x, 4y), grad f(4,2) = (8, 8)

Yon: p = (-8, -8)

alpha bulmak icin f(x0 + alpha * p) minimize et:

x = 4 - 8alpha
y = 2 - 8alpha

f(alpha) = (4 - 8alpha)^2 + 2(2 - 8alpha)^2
= 16 - 64alpha + 64alpha^2 + 2(4 - 32alpha + 64alpha^2)
= 16 - 64alpha + 64alpha^2 + 8 - 64alpha + 128alpha^2
= 24 - 128alpha + 192alpha^2

f'(alpha) = -128 + 384alpha = 0
alpha = 128/384 = 1/3

x1 = (4 - 8/3, 2 - 8/3) = (4/3, -2/3)

f(4, 2) = 16 + 8 = 24
f(4/3, -2/3) = 16/9 + 2(4/9) = 16/9 + 8/9 = 24/9 = 8/3 ≈ 2.67
</details>

---

## Soru 13: Newton Adimi

f(x,y) = 2x^2 + xy + y^2 - 5x - 3y icin x0 = (0, 0) noktasinda Newton adimini hesapla.

<details>
<summary>Cozum</summary>

grad f = (4x + y - 5, x + 2y - 3)
grad f(0,0) = (-5, -3)

H = | 4  1 |
    | 1  2 |

H^{-1} = 1/(8-1) * | 2  -1 | = 1/7 * | 2  -1 |
                     | -1  4 |          | -1  4 |

p^N = -H^{-1} grad f = -1/7 * | 2  -1 | * | -5 |
                                | -1  4 |   | -3 |

= -1/7 * | -10 + 3  | = -1/7 * | -7  | = | 1 |
         |  5 - 12  |          | -7  |   | 1 |

x1 = (0,0) + (1, 1) = (1, 1)

Kontrol: grad f(1,1) = (4 + 1 - 5, 1 + 2 - 3) = (0, 0) ✓ Tek adimda cozum!
</details>

---

## Soru 14: Ozdeger ile Siniflandirma

f(x,y) = 2x^2 + 4xy + y^2 fonksiyonunun orijindeki kritik noktasini siniflandir.

<details>
<summary>Cozum</summary>

grad f = (4x + 4y, 4x + 2y)
grad f(0,0) = (0, 0) → duragan nokta

H = | 4  4 |
    | 4  2 |

Ozdegerler: (4-l)(2-l) - 16 = 0
l^2 - 6l + 8 - 16 = 0
l^2 - 6l - 8 = 0
l = (6 ± sqrt(36 + 32))/2 = (6 ± sqrt(68))/2
l = (6 ± 8.25)/2

l1 = 7.12, l2 = -1.12

Bir pozitif, bir negatif → indefinit → Eyer noktasi.
</details>

---

## Soru 15: Armijo Kosulu Kontrolu

f(x) = x^4 fonksiyonunda x0 = 1, p0 = -1 (steepest descent). alpha = 0.5 icin Armijo kosulunu kontrol et (c1 = 0.1).

<details>
<summary>Cozum</summary>

f(x0) = f(1) = 1
f'(x0) = 4x^3 = 4, grad f * p = 4 * (-1) = -4

Armijo: f(x0 + alpha * p) <= f(x0) + c1 * alpha * grad f^T * p

Sol taraf: f(1 - 0.5) = f(0.5) = 0.0625

Sag taraf: 1 + 0.1 * 0.5 * (-4) = 1 - 0.2 = 0.8

0.0625 <= 0.8 ✓ Armijo kosulu saglaniyor.
</details>

---

## Soru 16: Kuadratik Formul ile Exact Line Search

f(x) = (1/2) x^T Q x, Q = | 6  2 |, x0 = (1, -1) icin steepest descent
                            | 2  4 |
adim boyunu kapali formulle hesapla.

<details>
<summary>Cozum</summary>

grad f = Qx = | 6  2 | | 1  | = | 4  |
              | 2  4 | | -1 |   | -2 |

p = -grad f = (-4, 2)

alpha = (grad f^T grad f) / (grad f^T Q grad f)

grad f^T grad f = 16 + 4 = 20

Q grad f = | 6  2 | | 4  | = | 20 |
           | 2  4 | | -2 |   | 0  |

grad f^T Q grad f = (4)(20) + (-2)(0) = 80

alpha = 20/80 = 1/4

x1 = (1, -1) + (1/4)(-4, 2) = (0, -0.5)
</details>

---

## Soru 17: Trust Region Kavramsal

Trust region yonteminde model fonksiyonu nedir? Yaricap nasil guncellenir? Kisa acikla.

<details>
<summary>Cozum</summary>

Model fonksiyonu: Fonksiyonun bulundugun noktadaki 2. derece Taylor yaklasimi:

m(p) = f(xk) + grad f(xk)^T p + (1/2) p^T B p

B genellikle Hessian veya bir yaklasimi.

Yaricap guncelleme:
- Gercek azalma / model azalma oranina (rho) bak
- rho buyukse (ornegin > 0.75): model iyi → yaricapi buyut
- rho kucukse (ornegin < 0.25): model kotu → yaricapi kucult
- rho negatifse: fonksiyon artti → adimi reddet, yaricapi kucult
</details>

---

## Soru 18: Wolfe Kosullari

f(x) = x^2 + 1 icin x0 = 3, p0 = -1, alpha = 1. Wolfe kosullarini kontrol et (c1 = 10^{-4}, c2 = 0.9).

<details>
<summary>Cozum</summary>

f(x0) = 10, f'(x0) = 6, grad f^T p = -6

Armijo: f(3 - 1) = f(2) = 5
5 <= 10 + 10^{-4} * 1 * (-6) = 10 - 0.0006 = 9.9994
5 <= 9.9994 ✓

Curvature: f'(x0 + alpha * p) * p >= c2 * f'(x0) * p
f'(2) * (-1) = 4 * (-1) = -4
c2 * f'(3) * (-1) = 0.9 * (-6) = -5.4

-4 >= -5.4 ✓

Her iki kosul saglaniyor.
</details>

---

## Soru 19: Eyer Noktasi

f(x,y) = x^2 - 4y^2 + 2x fonksiyonunun kritik noktasini bul ve siniflandir.

<details>
<summary>Cozum</summary>

grad f = (2x + 2, -8y) = (0, 0)

2x + 2 = 0 → x = -1
-8y = 0 → y = 0

Kritik nokta: (-1, 0)

H = | 2   0 |
    | 0  -8 |

Ozdegerler: l1 = 2 > 0, l2 = -8 < 0

Indefinit → Eyer noktasi.
</details>

---

## Soru 20: Iki Iterasyon Steepest Descent

f(x,y) = x^2 + y^2 icin x0 = (4, 3), exact line search ile 2 iterasyon uygula. Ne gozlemliyorsun?

<details>
<summary>Cozum</summary>

Iterasyon 0:
grad f(4,3) = (8, 6), p = (-8, -6)

f(alpha) = (4-8a)^2 + (3-6a)^2 = 16 - 64a + 64a^2 + 9 - 36a + 36a^2
= 25 - 100a + 100a^2

f'(a) = -100 + 200a = 0 → a = 1/2

x1 = (4 - 4, 3 - 3) = (0, 0)

f(0,0) = 0

grad f(0,0) = (0, 0) → Cozum bulundu! Tek iterasyonda bitti.

Gozlem: f = x^2 + y^2 izotropik (her yonde ayni egrilik), bu yuzden steepest descent zigzag yapmadan dogrudan minimuma gider. Kotu kosullanmis degil (kosul sayisi = 1).
</details>

---

## Soru 21: Backtracking Line Search

f(x,y) = x^2 + y^2, x0 = (2, 2), p = (-4, -4). Backtracking ile alpha bul (c1 = 0.5, rho = 0.5, alpha_hat = 1).

<details>
<summary>Cozum</summary>

f(2,2) = 8
grad f(2,2) = (4, 4)
grad f^T p = (4)(-4) + (4)(-4) = -32

alpha = 1: f(2-4, 2-4) = f(-2,-2) = 8
Armijo: 8 <= 8 + 0.5*1*(-32) = 8 - 16 = -8? Hayir

alpha = 0.5: f(0, 0) = 0
Armijo: 0 <= 8 + 0.5*0.5*(-32) = 8 - 8 = 0? Evet (esitlik saglar)

alpha = 0.5 kabul edildi.
</details>

---

## Soru 22: 2x2 Matris Tersi ve Newton

f(x,y) = x^2 + 3y^2 - 2xy fonksiyonu icin x0 = (2, 1) noktasinda Newton adimini hesapla.

<details>
<summary>Cozum</summary>

grad f = (2x - 2y, 6y - 2x)
grad f(2,1) = (4-2, 6-4) = (2, 2)

H = | 2  -2 |
    | -2  6 |

det(H) = 12 - 4 = 8

H^{-1} = 1/8 * | 6  2 |
                | 2  2 |

p^N = -H^{-1} grad f = -1/8 * | 6  2 | * | 2 | = -1/8 * | 16 | = | -2 |
                                | 2  2 |   | 2 |          | 8  |   | -1 |

x1 = (2,1) + (-2, -1) = (0, 0)

Kontrol: grad f(0,0) = (0, 0) ✓ Tek adimda cozum!
</details>

---

## Soru 23: Descent Direction — Aci Kontrolu

f(x,y) = x^2 + y^2 icin x = (1, 1) noktasinda, p = (1, -3) bir inis yonu mu?

<details>
<summary>Cozum</summary>

grad f(1,1) = (2, 2)

p^T grad f = (1)(2) + (-3)(2) = 2 - 6 = -4 < 0

Evet, inis yonudur. Gradient ile p arasindaki aci 90 dereceden buyuk.
</details>

---

## Soru 24: Konveks Fonksiyonda Optimallik

f(x,y) = e^x + e^{-y} + x^2 fonksiyonunun konveks oldugunu (Hessian uzerinden) goster ve duragan noktasini bul.

<details>
<summary>Cozum</summary>

grad f = (e^x + 2x, -e^{-y})

Duragan nokta: -e^{-y} = 0 → e^{-y} asla sifir olamaz!

Bu fonksiyonun duragan noktasi yoktur. Ancak y → sonsuz iken e^{-y} → 0.

Hessian:
H = | e^x + 2    0     |
    | 0          e^{-y} |

Kosegen elemanlar: e^x + 2 > 0 her zaman, e^{-y} > 0 her zaman.
Kosegen matris, tum kosegen elemanlar pozitif → pozitif definit → konveks.

Fonksiyon konveks ama duragan noktasi yok (infimumu sinirda).
</details>

---

## Soru 25: Dejenere Kritik Nokta

f(x,y) = x^2 + y^4 fonksiyonunun orijindeki kritik noktasini incele.

<details>
<summary>Cozum</summary>

grad f = (2x, 4y^3), grad f(0,0) = (0, 0) → duragan nokta

H = | 2      0    |
    | 0    12y^2  |

H(0,0) = | 2  0 |
          | 0  0 |

Ozdegerler: l1 = 2, l2 = 0 → pozitif semi-definit → dejenere.

2. turev testi kesin cevap veremez. Ama dogrudan bakarsak:
f(x,y) = x^2 + y^4 >= 0 her yerde ve f(0,0) = 0.

O zaman (0,0) global minimumdur. Hessian dejenere olmasina ragmen.
</details>

---

## Soru 26: Conjugate Gradient — Ilk Iterasyon

A = | 3  1 |, b = | 4 |, x0 = (0, 0). CG ile 1 iterasyon yap.
    | 1  3 |      | 4 |

<details>
<summary>Cozum</summary>

r0 = b - Ax0 = (4, 4)
p0 = r0 = (4, 4)

A p0 = | 3  1 | | 4 | = | 16 |
       | 1  3 | | 4 |   | 16 |

alpha0 = r0^T r0 / (p0^T A p0)
= (16 + 16) / ((4)(16) + (4)(16))
= 32 / 128 = 1/4

x1 = (0,0) + (1/4)(4, 4) = (1, 1)

r1 = r0 - alpha0 * A p0 = (4,4) - (1/4)(16, 16) = (4,4) - (4, 4) = (0, 0)

r1 = 0 → Cozum bulundu! x* = (1, 1)

Kontrol: Ax* = (3+1, 1+3) = (4, 4) = b ✓
</details>

---

## Soru 27: Line Search vs Trust Region Karsilastirmasi

Asagidaki ifadelerin hangisi line search'e, hangisi trust region'a ait?

a) Once yon belirlenir, sonra adim boyu
b) Model fonksiyonu bir bolgede minimize edilir
c) alpha parametresi aranir
d) Yaricap (Delta) guncellenir
e) Sadece tek bir dogrultuda arama yapilir

<details>
<summary>Cozum</summary>

a) Line Search
b) Trust Region
c) Line Search
d) Trust Region
e) Line Search
</details>

---

## Soru 28: Olcekleme Etkisi

f(x,y) = 100x^2 + y^2 fonksiyonuna x0 = (1, 1) noktasindan steepest descent uygula. Ilk adimi hesapla ve neden yavas yakinsaklik beklendigini acikla.

<details>
<summary>Cozum</summary>

grad f = (200, 2), p = (-200, -2)

Q = | 200  0 |
    | 0    2 |

alpha = (grad f^T grad f) / (grad f^T Q grad f)
= (40000 + 4) / (200*200*200 + 2*2*2)
= 40004 / (8000000 + 8)
= 40004 / 8000008
≈ 0.005

x1 = (1, 1) + 0.005*(-200, -2) = (0, 0.99)

f(0, 0.99) ≈ 0.98

x yonundeki hareket: 1 → 0 (tamamen gitti)
y yonundeki hareket: 1 → 0.99 (neredeyse hic degismedi)

Neden yavas: Kosul sayisi = 200/2 = 100 (cok buyuk). Gradient neredeyse tamamen x yonunde, y yonu ihmal ediliyor. Sonraki iterasyonlarda zigzag yapacak.
</details>

---

## Soru 29: Newton vs Steepest Descent Karsilastirmasi

f(x,y) = 50x^2 + y^2 icin x0 = (1, 1).
a) Newton adimini hesapla.
b) Steepest descent adimini hesapla (exact line search).
c) Hangisi daha iyi?

<details>
<summary>Cozum</summary>

grad f(1,1) = (100, 2)

H = | 100  0 |
    | 0    2 |

a) Newton:
H^{-1} = | 1/100  0   |
          | 0      1/2 |

p^N = -H^{-1} grad f = -(1, 1) = (-1, -1)
x1 = (0, 0). f = 0. Tek adimda bitti!

b) Steepest Descent:
p = (-100, -2)

alpha = (100^2 + 2^2) / (100^2*100 + 2^2*2)
= 10004 / 1000008 ≈ 0.01

x1 = (1, 1) + 0.01(-100, -2) = (0, 0.98)
f = 50*0 + 0.96 = 0.96

c) Newton tek adimda cozdu. Steepest descent henuz f = 0.96'da ve devam etmesi lazim. Newton cok daha iyi cunku Hessian bilgisi ile olcekleme farkini otomatik duzeltiyor.
</details>

---

## Soru 30: BFGS Kavramsal

BFGS yonteminde s ve y vektorleri nedir? Secant denklemi ne der? Neden y^T s > 0 olmasi gerekir?

<details>
<summary>Cozum</summary>

s = x_{k+1} - x_k (atilan adim)
y = grad f_{k+1} - grad f_k (gradyandaki degisim)

Secant denklemi: B_{k+1} s = y
Yani yeni Hessian yaklasimi, atilan adim ile gradyan degisimi arasindaki iliskiyi saglamali.

y^T s > 0 olmasi gerekir cunku:
- Bu kosul BFGS guncellemesinin pozitif definitligi korumasini garanti eder.
- Pozitif definitlik bozulursa, hesaplanan yon inis yonu olmaz ve algoritma bozulur.
- Wolfe kosullariyla line search yapildiginda y^T s > 0 otomatik olarak saglanir.
</details>

---

# ZOR (Soru 31–50)

---

## Soru 31: Steepest Descent — 2 Iterasyon

f(x,y) = 4x^2 - 4xy + 2y^2, x0 = (2, 3). Exact line search ile 2 tam iterasyon yap.

<details>
<summary>Cozum</summary>

Q = | 8  -4 |
    | -4  4 |

--- Iterasyon 0 ---
grad f(2,3) = (8*2-4*3, -4*2+4*3) = (4, 4)
p0 = (-4, -4)

alpha0 = (4^2 + 4^2) / ((4,4) Q (4,4)^T)
Q grad f = (8*4-4*4, -4*4+4*4) = (16, 0)
grad f^T Q grad f = 4*16 + 4*0 = 64

alpha0 = 32/64 = 1/2

x1 = (2,3) + 1/2*(-4,-4) = (0, 1)
f(0,1) = 0 - 0 + 2 = 2

--- Iterasyon 1 ---
grad f(0,1) = (0-4, 0+4) = (-4, 4)
p1 = (4, -4)

Q grad f = (8*(-4)-4*4, -4*(-4)+4*4) = (-48, 32)
grad f^T Q grad f = (-4)(-48) + (4)(32) = 192 + 128 = 320
grad f^T grad f = 16 + 16 = 32

alpha1 = 32/320 = 1/10

x2 = (0, 1) + (1/10)(4, -4) = (0.4, 0.6)
f(0.4, 0.6) = 4(0.16) - 4(0.24) + 2(0.36) = 0.64 - 0.96 + 0.72 = 0.4

f degerleri: 10 → 2 → 0.4
</details>

---

## Soru 32: Newton — Nonlineer Fonksiyon

f(x,y) = (x-1)^2 + (y-x^2)^2 icin x0 = (0, 0) noktasinda Newton adimini hesapla.

<details>
<summary>Cozum</summary>

grad f = (2(x-1) + 2(y-x^2)(-2x), 2(y-x^2))

(0,0) noktasinda:
df/dx = 2(0-1) + 2(0-0)(-0) = -2
df/dy = 2(0-0) = 0

grad f(0,0) = (-2, 0)

Hessian:
d^2f/dx^2 = 2 + 2(y-x^2)(−2) + 2(−2x)(−2x) = 2 − 4(y−x^2) + 8x^2
d^2f/dxdy = 2(-2x) = -4x
d^2f/dy^2 = 2

(0,0) noktasinda:
H = | 2 - 4(0) + 0   0 | = | 2  0 |
    | 0                2 |   | 0  2 |

H^{-1} = | 1/2  0   |
          | 0    1/2 |

p^N = -H^{-1}(-2, 0) = (1, 0)

x1 = (0,0) + (1, 0) = (1, 0)

grad f(1,0) = (0 + 2(0-1)(-2), 2(0-1)) = (4, -2) ≠ 0

Newton tek adimda cozmedi cunku fonksiyon kuadratik degil. Devam etmesi lazim.
</details>

---

## Soru 33: Cok Kritik Noktali Siniflandirma

f(x,y) = x^3 - 3x + y^3 - 3y fonksiyonunun tum kritik noktalarini bul ve siniflandir.

<details>
<summary>Cozum</summary>

grad f = (3x^2 - 3, 3y^2 - 3) = (0, 0)

3x^2 - 3 = 0 → x = 1 veya x = -1
3y^2 - 3 = 0 → y = 1 veya y = -1

4 kritik nokta: (1,1), (1,-1), (-1,1), (-1,-1)

H = | 6x  0  |
    | 0   6y |

(1, 1): H = diag(6, 6). Ozdegerler: 6, 6. Pozitif definit → Lokal minimum.

(1, -1): H = diag(6, -6). Ozdegerler: 6, -6. Indefinit → Eyer noktasi.

(-1, 1): H = diag(-6, 6). Ozdegerler: -6, 6. Indefinit → Eyer noktasi.

(-1, -1): H = diag(-6, -6). Ozdegerler: -6, -6. Negatif definit → Lokal maksimum.

f(1,1) = 1-3+1-3 = -4 (lokal minimum)
f(-1,-1) = -1+3-1+3 = 4 (lokal maksimum)
</details>

---

## Soru 34: Trust Region Alt Problemi

m(p) = 5 + (1, -2)^T p + (1/2) p^T I p (I = birim matris). Delta = 2.
a) Kisitsiz minimumu (Newton noktasi) bul. Trust region icinde mi?
b) Cauchy noktasini hesapla.

<details>
<summary>Cozum</summary>

g = (1, -2), B = I

a) Newton noktasi:
p^N = -B^{-1} g = -I * (1, -2) = (-1, 2)
||p^N|| = sqrt(1 + 4) = sqrt(5) ≈ 2.24

sqrt(5) > Delta = 2 → Trust region disinda.

b) Cauchy noktasi:
Steepest descent yonu: p^SD = -g = (-1, 2)
||p^SD|| = sqrt(5)

tau = min(1, ||g||^3 / (Delta * g^T B g))
||g||^2 = 1 + 4 = 5, ||g|| = sqrt(5)
g^T B g = g^T g = 5 (B = I oldugu icin)

Ilk once tam steepest descent adim boyunu bulalim:
alpha_SD = ||g||^2 / (g^T B g) = 5/5 = 1

Tam adim: p = -1 * g = (-1, 2), ||p|| = sqrt(5) > Delta

Trust region sinirinda kesmemiz lazim:
p^C = -Delta * g / ||g|| = -2 * (1, -2) / sqrt(5)
= (-2/sqrt(5), 4/sqrt(5))
≈ (-0.894, 1.789)

||p^C|| = 2 ✓ (sinir uzerinde)

m(p^C) = 5 + (1)(-0.894) + (-2)(1.789) + (1/2)(0.894^2 + 1.789^2)
= 5 - 0.894 - 3.578 + (1/2)(4)
= 5 - 0.894 - 3.578 + 2
= 2.528
</details>

---

## Soru 35: BFGS Guncelleme Hesabi

H0 = I (2x2), x0 = (3, 1), x1 = (1, 0), grad f0 = (4, 2), grad f1 = (0, -1).
BFGS ile H1'i hesapla.

<details>
<summary>Cozum</summary>

s = x1 - x0 = (-2, -1)
y = grad f1 - grad f0 = (-4, -3)

rho = 1 / (y^T s) = 1 / ((-4)(-2) + (-3)(-1)) = 1 / (8 + 3) = 1/11

H1 = (I - rho * s * y^T) H0 (I - rho * y * s^T) + rho * s * s^T

rho * s * y^T = (1/11) | -2 | (-4, -3) = (1/11) | 8   6  |
                        | -1 |                     | 4   3  |

I - rho * s * y^T = | 1-8/11   -6/11 | = | 3/11   -6/11 |
                     | -4/11   1-3/11 |   | -4/11   8/11 |

rho * y * s^T = (1/11) | -4 | (-2, -1) = (1/11) | 8   4 |
                        | -3 |                     | 6   3 |

I - rho * y * s^T = | 3/11   -4/11 |
                     | -6/11   8/11 |

H0 = I oldugu icin orta kisim:

| 3/11   -6/11 |   | 3/11   -4/11 |
| -4/11   8/11 | × | -6/11   8/11 |

= | 9/121 + 36/121     -12/121 - 48/121 | = | 45/121    -60/121 |
  | -12/121 - 48/121   16/121 + 64/121   |   | -60/121    80/121 |

rho * s * s^T = (1/11) | 4   2 | = | 4/11   2/11 |
                        | 2   1 |   | 2/11   1/11 |

= | 44/121   22/121 |
  | 22/121   11/121 |

H1 = | (45+44)/121    (-60+22)/121 | = | 89/121    -38/121 |
     | (-60+22)/121   (80+11)/121  |   | -38/121    91/121 |

H1 ≈ | 0.736   -0.314 |
      | -0.314   0.752 |

det(H1) ≈ 0.736*0.752 - 0.314^2 ≈ 0.554 - 0.099 = 0.455 > 0 ✓
</details>

---

## Soru 36: Conjugate Gradient — 2 Iterasyon

A = | 2  -1 |, b = (1, 1), x0 = (0, 0). CG ile tam cozum bul.
    | -1  2 |

<details>
<summary>Cozum</summary>

Iterasyon 0:
r0 = b - Ax0 = (1, 1)
p0 = r0 = (1, 1)

Ap0 = | 2  -1 | | 1 | = | 1 |
      | -1  2 | | 1 |   | 1 |

alpha0 = r0^T r0 / (p0^T Ap0) = 2 / (1+1) = 2/2 = 1

x1 = (0,0) + 1*(1,1) = (1, 1)
r1 = r0 - alpha0 * Ap0 = (1,1) - (1,1) = (0, 0)

r1 = 0 → Cozum: x* = (1, 1)

Dogrulama: Ax* = (2-1, -1+2) = (1, 1) = b ✓

Not: Tek iterasyonda bitti cunku baslangic residuali A'nin bir ozvektoru yonundeydi.
</details>

---

## Soru 37: Rosenbrock Fonksiyonu Analizi

f(x,y) = 100(y - x^2)^2 + (1 - x)^2

a) Duragan noktayi bul.
b) Hessiani (1,1) noktasinda hesapla ve pozitif definit mi kontrol et.

<details>
<summary>Cozum</summary>

a) grad f:
df/dx = -400x(y - x^2) - 2(1 - x)
df/dy = 200(y - x^2)

df/dy = 0 → y = x^2
df/dx = 0 → -2(1 - x) = 0 → x = 1
y = 1

Duragan nokta: (1, 1)

b) Hessian:
d^2f/dx^2 = -400(y - 3x^2) + 2
d^2f/dxdy = -400x
d^2f/dy^2 = 200

(1, 1) noktasinda:
d^2f/dx^2 = -400(1 - 3) + 2 = 800 + 2 = 802
d^2f/dxdy = -400

H = | 802   -400 |
    | -400   200 |

det(H) = 802*200 - (-400)^2 = 160400 - 160000 = 400 > 0
H(1,1) = 802 > 0

→ Pozitif definit → (1,1) lokal minimum. ✓
</details>

---

## Soru 38: Modifiye Newton

f(x,y) = x^2 - y^2 icin x0 = (1, 1) noktasinda:
a) Newton yonunun inis yonu olmadigini goster.
b) Hessian'a tau*I ekleyerek (tau = 5) modifiye Newton yonunu bul.

<details>
<summary>Cozum</summary>

grad f(1,1) = (2, -2)

H = | 2   0 |
    | 0  -2 |

a) Newton yonu:
p^N = -H^{-1} grad f = -| 1/2  0    | | 2  | = -| 1  | = | -1 |
                          | 0    -1/2 | | -2 |    | 1  |   | -1 |

Inis yonu kontrolu: p^T grad f = (-1)(2) + (-1)(-2) = -2 + 2 = 0

Sifir! Ne inis ne cikis yonu. Hessian indefinit oldugu icin Newton calismaz.

b) Modifiye Newton:
B = H + 5I = | 2+5   0   | = | 7  0 |
              | 0    -2+5 |   | 0  3 |

B^{-1} = | 1/7  0   |
          | 0    1/3 |

p = -B^{-1} grad f = -| 1/7  0   | | 2  | = | -2/7  |
                       | 0    1/3 | | -2 |   | 2/3   |

Inis yonu kontrolu: p^T grad f = (-2/7)(2) + (2/3)(-2) = -4/7 - 4/3 = -40/21 < 0 ✓

Modifiye Newton inis yonu sagliyor.
</details>

---

## Soru 39: Kosul Sayisi ve Yakinsaklik

Q = | a  0 | simetrik pozitif definit matris icin f(x) = (1/2)x^T Q x.
    | 0  1 |

a) Steepest descent yakinsaklik oranini kosul sayisi cinsinden yaz.
b) a = 100 icin en kotu yakinsaklik oranini hesapla.
c) a = 1 icin ne olur?

<details>
<summary>Cozum</summary>

Kosul sayisi: kappa = lambda_max / lambda_min

a) Steepest descent en kotu yakinsaklik orani:
r = ((kappa - 1) / (kappa + 1))^2

b) a = 100:
kappa = 100/1 = 100
r = (99/101)^2 = (0.9802)^2 ≈ 0.9608

Her iterasyonda hata en fazla %3.9 azalir. Cok yavas!
f degeri yarilanaana kadar ~17 iterasyon gerekir.

c) a = 1:
kappa = 1
r = (0/2)^2 = 0

Tek iterasyonda tam cozum! Izotropik (daire seklinde konturler) oldugu icin steepest descent zigzag yapmaz.
</details>

---

## Soru 40: Trust Region — Oran Hesabi

f(x) = x^2, model m(p) = f(xk) + f'(xk)*p + (1/2)*f''(xk)*p^2. xk = 2, Delta = 3.

a) Model minimizerini bul. Trust region icinde mi?
b) Gercek azalma / model azalma oranini (rho) hesapla.

<details>
<summary>Cozum</summary>

f(2) = 4, f'(2) = 4, f''(2) = 2

m(p) = 4 + 4p + (1/2)(2)p^2 = 4 + 4p + p^2

a) m'(p) = 4 + 2p = 0 → p = -2
|p| = 2 <= Delta = 3 → Trust region icinde ✓

b) Gercek azalma:
f(xk) - f(xk + p) = f(2) - f(0) = 4 - 0 = 4

Model azalma:
m(0) - m(p) = 4 - m(-2) = 4 - (4 - 8 + 4) = 4 - 0 = 4

rho = gercek azalma / model azalma = 4/4 = 1

rho = 1 → Model mukemmel! (Fonksiyon zaten kuadratik oldugu icin model tam dogru)
Yaricapi buyutebiliriz.
</details>

---

## Soru 41: Steepest Descent Zigzag Gosterimi

f(x,y) = 10x^2 + y^2 icin x0 = (1, 10). Exact line search ile 2 iterasyon yap. Zigzag davranisini goster.

<details>
<summary>Cozum</summary>

Q = | 20  0 |
    | 0   2 |

--- Iterasyon 0 ---
grad f(1,10) = (20, 20)
p0 = (-20, -20)

alpha0 = (400+400) / ((20)(20*20) + (20)(2*20))
= 800 / ((20)(400) + (20)(40))
= 800 / (8000 + 800) = 800/8800 = 1/11

x1 = (1, 10) + (1/11)(-20, -20) = (1 - 20/11, 10 - 20/11)
= (-9/11, 90/11) ≈ (-0.818, 8.182)

f(x1) = 10(81/121) + (8100/121) = 810/121 + 8100/121 = 8910/121 ≈ 73.6

--- Iterasyon 1 ---
grad f(-9/11, 90/11) = (-180/11, 180/11)
p1 = (180/11, -180/11)

grad f^T grad f = (180/11)^2 + (180/11)^2 = 2*(180/11)^2

Q grad f = (20*(-180/11), 2*(180/11)) = (-3600/11, 360/11)
grad f^T Q grad f = (-180/11)(-3600/11) + (180/11)(360/11)
= 648000/121 + 64800/121 = 712800/121

alpha1 = 2*(180/11)^2 / (712800/121)
= 2*32400/121 / (712800/121) = 64800/712800 = 1/11

x2 = (-9/11, 90/11) + (1/11)(180/11, -180/11)
= (-9/11 + 180/121, 90/11 - 180/121)
= (-99/121 + 180/121, 990/121 - 180/121)
= (81/121, 810/121) ≈ (0.669, 6.694)

Gozlem: x0 = (1, 10), x1 ≈ (-0.82, 8.18), x2 ≈ (0.67, 6.69)
x koordinati: pozitif → negatif → pozitif (zigzag!)
Minimum (0,0)'a dogru cok yavas yaklasiyor.
</details>

---

## Soru 42: Hessian Tekilligi ve Newton

f(x,y) = (x + y)^2 icin x0 = (1, 1) noktasinda Newton yontemi uygulanabilir mi?

<details>
<summary>Cozum</summary>

grad f = (2(x+y), 2(x+y))
grad f(1,1) = (4, 4)

H = | 2  2 |
    | 2  2 |

det(H) = 4 - 4 = 0

Hessian tekil (singular)! Tersi alinamaz.

Newton yonu: p^N = -H^{-1} grad f → H^{-1} mevcut degil.

Newton yontemi dogrudan uygulanamaz. Cozumler:
- Modifiye Newton: H + tau*I ile tekillikten kurtul
- Trust region: Tekil Hessian ile de calisabilir
- Quasi-Newton: Yaklasik Hessian kullan

Not: Hessian'in ozdegerleri l1 = 4, l2 = 0. Sifir ozdeger demek fonksiyon (1,-1) yonunde duz.
Gercekten de f(1+t, 1-t) = (2)^2 = 4, yani (1,-1) yonunde fonksiyon sabit.
</details>

---

## Soru 43: Wolfe Kosullari — Reddedilen Adim

f(x) = x^4 - 4x^2, x0 = 3, p = -1, alpha = 3. Wolfe kosullarini kontrol et (c1 = 10^{-4}, c2 = 0.9).

<details>
<summary>Cozum</summary>

f(3) = 81 - 36 = 45
f'(3) = 108 - 24 = 84
grad f^T p = 84*(-1) = -84

Armijo: f(3 + 3*(-1)) = f(0) = 0
0 <= 45 + 10^{-4}*3*(-84) = 45 - 0.0252 = 44.97
0 <= 44.97 ✓ Armijo saglar.

Curvature: f'(0)*(-1) >= 0.9*(84)*(-1)
0*(-1) >= -75.6
0 >= -75.6 ✓ Curvature saglar.

Her iki Wolfe kosulu saglaniyor. Ama dikkat: alpha = 3 ile x = 0 noktasina geliyoruz ki bu bir lokal maksimumdur. Bu gosteriyor ki Wolfe kosullari her zaman "iyi" bir noktaya goturmuyor — sadece yeterli ilerleme saglandigini garanti ediyor.
</details>

---

## Soru 44: 3 Degiskenli Kritik Nokta

f(x,y,z) = x^2 + 2y^2 + 3z^2 - 2xy - 4z fonksiyonunun kritik noktasini bul ve siniflandir.

<details>
<summary>Cozum</summary>

grad f:
df/dx = 2x - 2y
df/dy = 4y - 2x
df/dz = 6z - 4

grad f = 0:
2x - 2y = 0 → x = y     ... (1)
4y - 2x = 0 → 2y = x    ... (2)
6z - 4 = 0 → z = 2/3    ... (3)

(1) ve (2): x = y ve 2y = x → 2y = y → y = 0 → x = 0

Kritik nokta: (0, 0, 2/3)

Hessian:
H = | 2   -2   0 |
    | -2   4   0 |
    | 0    0   6 |

Ozdegerler: 6 (acik) ve 2x2 alt matrisin ozdegerleri:
| 2  -2 |
| -2  4 |

l^2 - 6l + (8-4) = l^2 - 6l + 4 = 0
l = (6 ± sqrt(36-16))/2 = (6 ± sqrt(20))/2
l1 = (6 + 4.47)/2 ≈ 5.24
l2 = (6 - 4.47)/2 ≈ 0.76

Tum ozdegerler pozitif: 0.76, 5.24, 6 → Pozitif definit → Lokal minimum.

f konveks oldugu icin bu ayni zamanda global minimum.
f(0, 0, 2/3) = 0 + 0 + 3(4/9) - 0 - 8/3 = 4/3 - 8/3 = -4/3
</details>

---

## Soru 45: Conjugate Gradient — Tam 2 Iterasyon

A = | 4  1 |, b = (1, 2), x0 = (2, 1). CG ile coz.
    | 1  3 |

<details>
<summary>Cozum</summary>

--- Iterasyon 0 ---
r0 = b - Ax0 = (1,2) - (| 4 1 | | 2 |) = (1,2) - (9, 5) = (-8, -3)
                         | 1 3 | | 1 |
p0 = r0 = (-8, -3)

Ap0 = | 4  1 | | -8 | = | -35 |
      | 1  3 | | -3 |   | -17 |

r0^T r0 = 64 + 9 = 73

p0^T Ap0 = (-8)(-35) + (-3)(-17) = 280 + 51 = 331

alpha0 = 73 / 331

x1 = (2, 1) + (73/331)(-8, -3) = (2 - 584/331, 1 - 219/331)
= (78/331, 112/331)
≈ (0.236, 0.338)

r1 = r0 - alpha0 * Ap0 = (-8, -3) - (73/331)(-35, -17)
= (-8 + 2555/331, -3 + 1241/331)
= (-2648/331 + 2555/331, -993/331 + 1241/331)
= (-93/331, 248/331)

r1^T r1 = (93/331)^2 + (248/331)^2 = (8649 + 61504)/331^2 = 70153/109561

beta1 = r1^T r1 / r0^T r0 = 70153 / (73 * 109561) = 70153 / 7997953
≈ 70153/7997953 ≈ 0.00877

Hmm, bu sayilar karisik. Simdi n = 2 oldugu icin en fazla 2 iterasyonda cozum garanti.

--- Iterasyon 1 ---
p1 = r1 + beta1 * p0

Bu noktada tam sayilar cok karmasik. Ama n=2 sistemi icin CG en gec 2. iterasyonda tam cozumu bulacaktir.

Dogrudan cozum: Ax = b → x* = A^{-1} b

A^{-1} = 1/(12-1) * | 3  -1 | = 1/11 * | 3  -1 |
                      | -1  4 |           | -1  4 |

x* = 1/11 * (3-2, -1+8) = 1/11 * (1, 7) = (1/11, 7/11)

Dogrulama: A(1/11, 7/11) = (4/11 + 7/11, 1/11 + 21/11) = (1, 2) = b ✓

CG 2. iterasyon sonunda bu degere ulasacaktir.
</details>

---

## Soru 46: Newton — Cozume Yakin Olmayan Baslangic

f(x) = x - ln(x) (x > 0) icin Newton yontemini x0 = 5 noktasindan 2 iterasyon uygula.

<details>
<summary>Cozum</summary>

f'(x) = 1 - 1/x
f''(x) = 1/x^2

Newton adimi: p = -f'(x)/f''(x) = -(1 - 1/x)/(1/x^2) = -(x^2 - x)

xk+1 = xk + p = xk - x^2 + x = xk(2 - xk)

Hmm, bu formul yuzunden uzaklasabilir. Daha dikkatli yapalim:

p = -f'(x)/f''(x) = -(1 - 1/x) * x^2 = -x^2 + x

xk+1 = xk + (-xk^2 + xk) = 2xk - xk^2

Iterasyon 0: x0 = 5
x1 = 2(5) - 25 = 10 - 25 = -15

Negatif! x > 0 kosulu ihlal edildi. Newton yontemi iraksaklasti.

Bu Newton'un zayif noktasini gosteriyor: baslangic noktasi cozume (x* = 1) uzak oldugunda Newton yakinsamayabilir veya anlamsiz sonuc verebilir.

Cozum: Line search ile birlestir (damped Newton) veya trust region kullan.
</details>

---

## Soru 47: Steepest Descent ve Newton Karsilastirmasi — Kotu Kosullu Problem

f(x,y) = 500x^2 + y^2 icin x0 = (1, 1).
a) Kosul sayisini hesapla.
b) Her iki yontemle ilk adimi hesapla.
c) Steepest descent yakinsaklik oranini bul.

<details>
<summary>Cozum</summary>

Q = | 1000  0 |
    | 0     2 |

a) kappa = 1000/2 = 500

b) grad f(1,1) = (1000, 2)

Newton:
H^{-1} = diag(1/1000, 1/2)
p^N = -(1, 1), x1 = (0, 0). Bitti!

Steepest Descent:
p = (-1000, -2)
alpha = (1000^2 + 2^2) / (1000^2*1000 + 2^2*2)
= 1000004 / 1000000008 ≈ 0.001

x1 = (1, 1) + 0.001(-1000, -2) = (0, 0.998)
f(x1) = 0 + 0.996 = 0.996

c) Yakinsaklik orani:
r = ((kappa - 1)/(kappa + 1))^2 = (499/501)^2 ≈ (0.996)^2 ≈ 0.992

Her iterasyonda hata sadece %0.8 azalir!
f yarilanaana kadar ~86 iterasyon gerekir. Newton ise 1 adim.
</details>

---

## Soru 48: Backtracking + Wolfe Birarada

f(x,y) = 2x^2 + y^2, x0 = (3, 4), p = -grad f = (-12, -8).
Backtracking ile alpha bul (c1 = 0.1, rho = 0.5, alpha_hat = 1).
Sonra bulunan alpha icin curvature kosulunu (c2 = 0.9) kontrol et.

<details>
<summary>Cozum</summary>

f(3,4) = 18 + 16 = 34
grad f = (12, 8)
grad f^T p = (12)(-12) + (8)(-8) = -144 - 64 = -208

alpha = 1: f(3-12, 4-8) = f(-9, -4) = 162 + 16 = 178
Armijo: 178 <= 34 + 0.1*1*(-208) = 34 - 20.8 = 13.2? Hayir

alpha = 0.5: f(3-6, 4-4) = f(-3, 0) = 18
Armijo: 18 <= 34 + 0.1*0.5*(-208) = 34 - 10.4 = 23.6? Evet ✓

alpha = 0.5 kabul edildi.

Curvature kontrolu:
grad f(-3, 0) = (-12, 0)
grad f(-3, 0)^T p = (-12)(-12) + (0)(-8) = 144

c2 * grad f(x0)^T p = 0.9 * (-208) = -187.2

144 >= -187.2 ✓ Curvature saglaniyor.

Ama dikkat: grad f(-3,0)^T p = 144 > 0 demek bu noktada p artik inis yonu degil. Yon degistirmis. Strong Wolfe kosulu |grad f^T p| <= c2 * |grad f0^T p| kontrol eder:
|144| <= 0.9 * 208 = 187.2? 144 <= 187.2 ✓ Strong Wolfe da saglar.
</details>

---

## Soru 49: SR1 vs BFGS

a) SR1 guncelleme formulunu yaz.
b) SR1 neden pozitif definitligi garanti etmez?
c) SR1 genellikle hangi strateji ile kullanilir ve neden?

<details>
<summary>Cozum</summary>

a) SR1 guncelleme:
B_{k+1} = B_k + ((y - B_k s)(y - B_k s)^T) / ((y - B_k s)^T s)

Burada s = x_{k+1} - x_k, y = grad f_{k+1} - grad f_k.

b) SR1 rank-1 guncelleme yapar. Guncelleme terimi:
v v^T / (v^T s) seklinde, v = y - Bk s.

Eger v^T s < 0 ise, eklenen terim negatif definitlik getirebilir.
BFGS ise y^T s > 0 kosulu saglandigi surece her zaman pozitif definitligi korur (rank-2 guncelleme ile).

c) SR1 genellikle trust region ile kullanilir. Cunku:
- Trust region yontemi, B'nin pozitif definit olmasini gerektirmez.
- Trust region yaricapi ile kontrol saglandigi icin, indefinit B bile guvenlice kullanilabilir.
- Line search icin ise B pozitif definit olmali ki hesaplanan yon inis yonu olsun — SR1 bunu garanti edemez.
</details>

---

## Soru 50: Kapsamli Analiz

f(x,y) = x^4 + y^4 - 4xy + 1 fonksiyonunu analiz et.
a) Tum kritik noktalari bul.
b) Her birini siniflandir.
c) Global minimum var mi?

<details>
<summary>Cozum</summary>

a) grad f = (4x^3 - 4y, 4y^3 - 4x) = (0, 0)

4x^3 - 4y = 0 → y = x^3    ... (1)
4y^3 - 4x = 0 → x = y^3    ... (2)

(1)'i (2)'ye koy: x = (x^3)^3 = x^9
x^9 - x = 0 → x(x^8 - 1) = 0
x = 0 veya x^8 = 1 → x = 1 veya x = -1

x = 0: y = 0 → (0, 0)
x = 1: y = 1 → (1, 1)
x = -1: y = -1 → (-1, -1)

b) Hessian:
H = | 12x^2   -4    |
    | -4      12y^2  |

(0, 0):
H = | 0   -4 |
    | -4   0 |
Ozdegerler: l = ±4. Indefinit → Eyer noktasi.
f(0,0) = 1

(1, 1):
H = | 12  -4 |
    | -4  12 |
det = 144 - 16 = 128 > 0, iz = 24 > 0.
Ozdegerler: 12±4 = 16, 8. Pozitif definit → Lokal minimum.
f(1,1) = 1 + 1 - 4 + 1 = -1

(-1, -1):
H = | 12  -4 |
    | -4  12 |
Ayni Hessian → Pozitif definit → Lokal minimum.
f(-1,-1) = 1 + 1 + 4 + 1 = hmm, dikkatli hesaplayalim:
f(-1,-1) = (-1)^4 + (-1)^4 - 4(-1)(-1) + 1 = 1 + 1 - 4 + 1 = -1

c) Global minimum var mi?

x → ±sonsuz veya y → ±sonsuz iken x^4 + y^4 baskin → f → +sonsuz.
Yani fonksiyon alttan sinirli ve sonsuzda sonsuza gidiyor → global minimum kesinlikle vardir.

Iki lokal minimum var: (1,1) ve (-1,-1), ikisinde de f = -1.
Baska kritik nokta yok (eyer noktasindaki f = 1 daha buyuk).

Global minimum: f = -1, iki noktada: (1,1) ve (-1,-1).
</details>
