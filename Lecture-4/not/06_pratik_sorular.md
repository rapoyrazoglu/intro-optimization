# Lecture 4 — Pratik Sorular (50 Soru)

---

# KOLAY (Soru 1–10)

---

## Soru 1: Kuadratik Model Olusturma (1D)

f(x) = x^2 + 4x + 1 fonksiyonunda x_0 = 1 noktasinda kuadratik modeli m(p) = f_0 + g_0 p + (1/2) B_0 p^2 seklinde yaziniz.

<details>
<summary>Cozum</summary>

f(1) = 1 + 4 + 1 = 6
f'(1) = 2(1) + 4 = 6
f''(1) = 2

m(p) = 6 + 6p + (1/2)(2)p^2 = 6 + 6p + p^2

(Kontrol: m(0) = 6 = f(1). Dogru.)
</details>

---

## Soru 2: Newton Adiminin Guven Bolgesi Icinde mi Kontrolu

f(x) = x^4 - 2x^2 fonksiyonunda x_0 = 2 noktasinda Newton adimini hesaplayin. Delta = 0.5 icin Newton adimi guven bolgesi icinde midir?

<details>
<summary>Cozum</summary>

f'(x) = 4x^3 - 4x => f'(2) = 32 - 8 = 24
f''(x) = 12x^2 - 4 => f''(2) = 48 - 4 = 44

p^N = -f'(2)/f''(2) = -24/44 = -6/11 ≈ -0.545

|p^N| = 0.545 > 0.5 = Delta

Hayir, Newton adimi guven bolgesi disinda.
</details>

---

## Soru 3: Basit rho_k Hesabi

Bir trust region iterasyonunda f(x_k) = 20, f(x_k + p_k) = 15, m_k(0) = 20, m_k(p_k) = 14 ise rho_k nedir?

<details>
<summary>Cozum</summary>

rho_k = (f(x_k) - f(x_k + p_k)) / (m_k(0) - m_k(p_k))

rho_k = (20 - 15) / (20 - 14) = 5/6 ≈ 0.833

rho_k ≈ 0.833 (modelin iyi bir tahmin yaptigi gorulur)
</details>

---

## Soru 4: Yaricap Guncelleme Karari

rho_k = 0.1, ||p_k|| = Delta_k = 2 olduguna gore Delta_{k+1} ne olur? Adim kabul edilir mi? (eta = 0.1)

<details>
<summary>Cozum</summary>

rho_k = 0.1 < 1/4 => Delta_{k+1} = (1/4) * Delta_k = (1/4)(2) = 0.5

Adim kabul mu? rho_k = 0.1 >= eta = 0.1 => Evet, adim kabul edilir (sinirda).

x_{k+1} = x_k + p_k, Delta_{k+1} = 0.5
</details>

---

## Soru 5: Yaricap Buyutme Karari

rho_k = 0.9, ||p_k|| = Delta_k = 3, Delta_hat = 10 olduguna gore Delta_{k+1} nedir?

<details>
<summary>Cozum</summary>

rho_k = 0.9 > 3/4 ve ||p_k|| = Delta_k (kisit aktif)

=> Delta_{k+1} = min(2 * Delta_k, Delta_hat) = min(6, 10) = 6

Adim da kabul edilir (rho_k > eta).
</details>

---

## Soru 6: Adim Reddi

rho_k = -0.5 oldugunda ne olur? (eta = 0.2, Delta_k = 4)

<details>
<summary>Cozum</summary>

rho_k = -0.5 < 0 < 1/4

Delta_{k+1} = (1/4)(4) = 1

Adim kabul mu? rho_k = -0.5 < eta = 0.2 => Hayir, adim reddedilir.

x_{k+1} = x_k (yerinde kal), Delta_{k+1} = 1
</details>

---

## Soru 7: 2D Gradyan ve Hessian

f(x,y) = 2x^2 + 3y^2 + 2xy fonksiyonunun (1, -1) noktasindaki gradyan ve Hessian'ini hesaplayin.

<details>
<summary>Cozum</summary>

df/dx = 4x + 2y => df/dx(1,-1) = 4 - 2 = 2
df/dy = 6y + 2x => df/dy(1,-1) = -6 + 2 = -4

grad f(1,-1) = (2, -4)

d^2f/dx^2 = 4, d^2f/dy^2 = 6, d^2f/dxdy = 2

H = | 4  2 |
    | 2  6 |
</details>

---

## Soru 8: Model Degeri Hesabi

g = (3, -1)^T, B = [[4, 0], [0, 2]], f_k = 10, p = (-1, 1)^T icin m_k(p) degerini hesaplayin.

<details>
<summary>Cozum</summary>

m_k(p) = f_k + g^T p + (1/2) p^T B p

g^T p = (3)(-1) + (-1)(1) = -3 - 1 = -4

B p = (4(-1), 2(1)) = (-4, 2)
p^T B p = (-1)(-4) + (1)(2) = 4 + 2 = 6

m_k(p) = 10 + (-4) + (1/2)(6) = 10 - 4 + 3 = 9
</details>

---

## Soru 9: Kisit Aktif mi Pasif mi?

B = [[6, 0], [0, 2]], g = (3, 1)^T, Delta = 2. Newton adimi kisit icinde mi?

<details>
<summary>Cozum</summary>

p^N = -B^{-1} g = -(1/6 * 3, 1/2 * 1) = (-0.5, -0.5)

||p^N|| = sqrt(0.25 + 0.25) = sqrt(0.5) ≈ 0.707

0.707 < 2 = Delta => Kisit pasif. Newton adimi olduğu gibi kullanilir. lambda = 0.
</details>

---

## Soru 10: Tahmin Edilen Azalma

m_k(0) = 25, m_k(p_k) = 18 ise tahmin edilen azalma nedir? Gercek azalma 5 ise rho_k kactir?

<details>
<summary>Cozum</summary>

Tahmin edilen azalma = m_k(0) - m_k(p_k) = 25 - 18 = 7

rho_k = gercek azalma / tahmin edilen azalma = 5 / 7 ≈ 0.714

(0.25 < 0.714 < 0.75 oldugu icin yaricap degismez: Delta_{k+1} = Delta_k)
</details>

---

# ORTA (Soru 11–30)

---

## Soru 11: Trust Region Alt Problemi Tam Cozum (1D)

f(x) = x^3 - 3x fonksiyonunda x_0 = 2, Delta = 0.5. Trust region alt problemini cozunuz.

<details>
<summary>Cozum</summary>

f(2) = 8 - 6 = 2
f'(2) = 12 - 3 = 9
f''(2) = 12

Model: m(p) = 2 + 9p + 6p^2

Kisitsiz minimum: m'(p) = 9 + 12p = 0 => p = -3/4 = -0.75

|p| = 0.75 > Delta = 0.5 => Kisit aktif.

p* = -0.5 (sinirda, inis yonunde)

m(-0.5) = 2 + 9(-0.5) + 6(0.25) = 2 - 4.5 + 1.5 = -1.0

Dogrulama: f(2 - 0.5) = f(1.5) = 3.375 - 4.5 = -1.125
rho = (2 - (-1.125)) / (2 - (-1.0)) = 3.125 / 3.0 = 1.042
</details>

---

## Soru 12: Optimallik Kosullarini Dogrulama (1D)

Soru 11'deki cozum icin (B + lambda)p* = -g ve lambda(Delta - |p*|) = 0 kosullarini dogrulayiniz.

<details>
<summary>Cozum</summary>

B = 12, g = 9, p* = -0.5, Delta = 0.5

Kosul 1: (B + lambda)p* = -g
(12 + lambda)(-0.5) = -9
-6 - 0.5 lambda = -9
0.5 lambda = 3
lambda = 6

Kosul 2: lambda(Delta - |p*|) = 6(0.5 - 0.5) = 6(0) = 0 ✓

Kosul 3: B + lambda = 12 + 6 = 18 > 0 (pozitif tanili) ✓
</details>

---

## Soru 13: 2x2 Trust Region — Diyagonal Hessian

g = (8, 6)^T, B = [[4, 0], [0, 9]], Delta = 1. Optimallik kosullarini kullanarak trust region cozumunu bulunuz.

<details>
<summary>Cozum</summary>

Newton adimi: p^N = -B^{-1}g = (-8/4, -6/9) = (-2, -2/3)
||p^N|| = sqrt(4 + 4/9) = sqrt(40/9) ≈ 2.11 > 1 = Delta

Kisit aktif. (B + lambda I)p = -g:

p = (-8/(4+lambda), -6/(9+lambda))

||p|| = 1:
(8/(4+lambda))^2 + (6/(9+lambda))^2 = 1

lambda'yi sayisal olarak bulalim:

lambda = 0: 4 + 4/9 = 40/9 ≈ 4.44 (cok buyuk)
lambda = 4: (8/8)^2 + (6/13)^2 = 1 + 0.213 = 1.213 (hala buyuk)
lambda = 5: (8/9)^2 + (6/14)^2 = 0.790 + 0.184 = 0.974 (biraz kucuk)
lambda = 4.8: (8/8.8)^2 + (6/13.8)^2 = 0.826 + 0.189 = 1.015 (yakin)
lambda ≈ 4.9: (8/8.9)^2 + (6/13.9)^2 = 0.808 + 0.186 = 0.994

lambda ≈ 4.85 ile:
p* ≈ (-8/8.85, -6/13.85) ≈ (-0.904, -0.433)
||p*|| ≈ sqrt(0.817 + 0.187) = sqrt(1.004) ≈ 1.0 ✓
</details>

---

## Soru 14: Cauchy Noktasi (2D)

g = (4, 3)^T, B = [[2, 0], [0, 8]], Delta = 2. Cauchy noktasini hesaplayiniz.

<details>
<summary>Cozum</summary>

||g|| = sqrt(16 + 9) = 5

g^T B g = (4, 3) (2*4, 8*3)^T = (4)(8) + (3)(24) = 32 + 72 = 104 > 0

p_S = -(Delta/||g||) g = -(2/5)(4, 3) = (-1.6, -1.2)

tau = min(||g||^3 / (Delta * g^T B g), 1) = min(125 / (2 * 104), 1) = min(0.601, 1) = 0.601

p^C = tau * p_S = 0.601 * (-1.6, -1.2) = (-0.961, -0.721)

||p^C|| = 0.601 * 2 = 1.202 (guven bolgesi icinde, sinirda degil)
</details>

---

## Soru 15: Cauchy Noktasi — Negatif Egrilik

g = (1, 2)^T, B = [[-3, 0], [0, 1]], Delta = 1. Cauchy noktasini hesaplayiniz.

<details>
<summary>Cozum</summary>

||g|| = sqrt(1 + 4) = sqrt(5) ≈ 2.236

g^T B g = (1)(−3)(1) + (2)(1)(2) = −3 + 4 = 1 > 0

tau = min(||g||^3/(Delta * g^T B g), 1) = min((2.236)^3 / (1 * 1), 1) = min(11.18, 1) = 1

p_S = -(1/2.236)(1, 2) = (-0.447, -0.894)
p^C = 1 * p_S = (-0.447, -0.894)

||p^C|| = 1 (sinirda)
</details>

---

## Soru 16: Cauchy Noktasi — Tamamen Negatif Egrilik

g = (2, 0)^T, B = [[-1, 0], [0, -1]], Delta = 3. Cauchy noktasini hesaplayiniz.

<details>
<summary>Cozum</summary>

g^T B g = (2)(-1)(2) + (0)(-1)(0) = -4 < 0

Negatif egrilik => tau = 1

p_S = -(Delta/||g||) g = -(3/2)(2, 0) = (-3, 0)
p^C = 1 * (-3, 0) = (-3, 0)

||p^C|| = 3 = Delta (sinirda)
</details>

---

## Soru 17: Dogleg — p^U ve p^B Hesabi

g = (-2, -2)^T, B = [[1, 0], [0, 4]], Delta = 3. Dogleg yontemi icin p^U ve p^B'yi hesaplayiniz.

<details>
<summary>Cozum</summary>

p^B (Newton adimi):
p^B = -B^{-1} g = -[[1,0],[0,1/4]](-2,-2)^T = (2, 0.5)

||p^B|| = sqrt(4 + 0.25) = sqrt(4.25) ≈ 2.06

p^U (kisitsiz Cauchy):
g^T g = 4 + 4 = 8
g^T B g = (-2)(1)(-2) + (-2)(4)(-2) = 4 + 16 = 20

p^U = -(g^T g / g^T B g) g = -(8/20)(-2, -2) = (0.8, 0.8)

||p^U|| = sqrt(0.64 + 0.64) = sqrt(1.28) ≈ 1.131

||p^B|| = 2.06 < Delta = 3 => Newton adimi icerde! p* = p^B = (2, 0.5) kullanilir.
</details>

---

## Soru 18: Dogleg — Newton Disarida

Soru 17 ile ayni veriler ama Delta = 1.5. Dogleg cozumunu bulunuz.

<details>
<summary>Cozum</summary>

p^U = (0.8, 0.8), ||p^U|| = 1.131
p^B = (2, 0.5), ||p^B|| = 2.06

||p^B|| = 2.06 > Delta = 1.5. Newton disarida.
||p^U|| = 1.131 < Delta = 1.5. Cauchy icerde.

Ikinci parcadayiz (tau in (1,2)):
p(tau) = p^U + (tau-1)(p^B - p^U)

p^B - p^U = (2 - 0.8, 0.5 - 0.8) = (1.2, -0.3)

p(tau) = (0.8 + 1.2(tau-1), 0.8 - 0.3(tau-1))

||p(tau)||^2 = Delta^2 = 2.25:
(0.8 + 1.2(tau-1))^2 + (0.8 - 0.3(tau-1))^2 = 2.25

s = tau - 1 diyelim:
(0.8 + 1.2s)^2 + (0.8 - 0.3s)^2 = 2.25
0.64 + 1.92s + 1.44s^2 + 0.64 - 0.48s + 0.09s^2 = 2.25
1.53s^2 + 1.44s + 1.28 = 2.25
1.53s^2 + 1.44s - 0.97 = 0

s = (-1.44 + sqrt(1.44^2 + 4*1.53*0.97)) / (2*1.53)
s = (-1.44 + sqrt(2.0736 + 5.9364)) / 3.06
s = (-1.44 + sqrt(8.01)) / 3.06
s = (-1.44 + 2.83) / 3.06 = 1.39 / 3.06 = 0.454

tau = 1 + 0.454 = 1.454

p* = (0.8 + 1.2(0.454), 0.8 - 0.3(0.454)) = (1.345, 0.664)

||p*|| = sqrt(1.810 + 0.441) = sqrt(2.251) ≈ 1.50 ✓
</details>

---

## Soru 19: rho_k ve Tam Karar Dongusu

f(x,y) = x^2 + y^2, x_0 = (3, 4), Delta_0 = 2, eta = 0.1. Bir iterasyon gerceklestirin.

<details>
<summary>Cozum</summary>

f(3,4) = 25, g = (6, 8), B = [[2,0],[0,2]]

Newton: p^N = -B^{-1}g = -(3, 4), ||p^N|| = 5 > Delta = 2

Kisit aktif. (B + lambda I)p = -g:
(2+lambda)p_1 = -6, (2+lambda)p_2 = -8
p = (-6/(2+lambda), -8/(2+lambda))

||p|| = 2: sqrt(36 + 64)/(2+lambda) = 10/(2+lambda) = 2
2 + lambda = 5 => lambda = 3

p* = (-6/5, -8/5) = (-1.2, -1.6)

x_1 = (3-1.2, 4-1.6) = (1.8, 2.4)

rho_0:
- f(3,4) - f(1.8, 2.4) = 25 - (3.24 + 5.76) = 25 - 9.0 = 16.0
- m(0) - m(p*) = 25 - [25 + (6,8)(-1.2,-1.6)^T + (1/2)(-1.2,-1.6)[[2,0],[0,2]](-1.2,-1.6)^T]
  g^T p = 6(-1.2) + 8(-1.6) = -7.2 - 12.8 = -20
  p^T B p = 2(1.44) + 2(2.56) = 2.88 + 5.12 = 8.0
  m(p*) = 25 - 20 + 4 = 9
  Tahmin edilen azalma = 25 - 9 = 16

rho_0 = 16/16 = 1.0

rho_0 > 3/4 ve ||p*|| = Delta => Delta_1 = min(4, Delta_hat). Adim kabul.
</details>

---

## Soru 20: Kuadratik Model 2D

f(x,y) = x^3 + y^2 - xy icin (1, 1) noktasindaki kuadratik modeli yaziniz.

<details>
<summary>Cozum</summary>

f(1,1) = 1 + 1 - 1 = 1

df/dx = 3x^2 - y => df/dx(1,1) = 3 - 1 = 2
df/dy = 2y - x => df/dy(1,1) = 2 - 1 = 1
g = (2, 1)^T

d^2f/dx^2 = 6x => 6
d^2f/dy^2 = 2
d^2f/dxdy = -1

B = | 6  -1 |
    | -1  2  |

m(p) = 1 + (2, 1) p + (1/2) p^T [[6,-1],[-1,2]] p

Yani: m(p_1, p_2) = 1 + 2p_1 + p_2 + 3p_1^2 + p_2^2 - p_1 p_2
</details>

---

## Soru 21: Newton Adimi — Ters Capraz Hessian

g = (5, 3)^T, B = [[2, 1], [1, 4]]. Newton adimini hesaplayiniz.

<details>
<summary>Cozum</summary>

det(B) = 8 - 1 = 7

B^{-1} = (1/7) | 4  -1 |
               | -1  2  |

p^N = -B^{-1} g = -(1/7)(4*5 + (-1)*3, (-1)*5 + 2*3) = -(1/7)(17, 1) = (-17/7, -1/7)

p^N ≈ (-2.429, -0.143)

||p^N|| = sqrt(5.899 + 0.020) ≈ 2.433
</details>

---

## Soru 22: rho_k ile Model Kalitesi

f(x) = e^x fonksiyonunda x_0 = 0, Delta = 1. Trust region adimini at, rho hesapla.

<details>
<summary>Cozum</summary>

f(0) = 1, f'(0) = 1, f''(0) = 1

Model: m(p) = 1 + p + p^2/2

Kisitsiz min: m'(p) = 1 + p = 0 => p = -1. |p| = 1 = Delta. Tam sinirda!

m(-1) = 1 - 1 + 1/2 = 0.5

f(0 + (-1)) = f(-1) = e^{-1} ≈ 0.3679

rho = (f(0) - f(-1)) / (m(0) - m(-1)) = (1 - 0.3679) / (1 - 0.5) = 0.6321 / 0.5 = 1.264

rho > 3/4 ve |p| = Delta => Bolge buyutulur, adim kabul.
</details>

---

## Soru 23: Cauchy vs Newton Yonu Karsilastirmasi

g = (1, 0)^T, B = [[1, 0], [0, 100]]. Cauchy ve Newton yonlerini karsilastiriniz.

<details>
<summary>Cozum</summary>

Cauchy yonu: -g = (-1, 0)

Newton yonu: -B^{-1} g = -(1, 0) = (-1, 0)

Bu durumda Cauchy ve Newton ayni yonde! Cunku gradyanin sadece x bileseni var ve B diyagonal.

Ama farkli boylar:
- Cauchy adim boyu (kisitsiz): g^T g / g^T B g = 1/1 = 1. p^U = (-1, 0)
- Newton: p^N = -B^{-1}g = (-1, 0)

Bu ozel durumda ikisi de ayni!
</details>

---

## Soru 24: Cauchy vs Newton — Farkli Yonler

g = (1, 1)^T, B = [[1, 0], [0, 100]]. Cauchy ve Newton yonlerini karsilastiriniz.

<details>
<summary>Cozum</summary>

Cauchy yonu: -g/||g|| = (-1, -1)/sqrt(2) ≈ (-0.707, -0.707)

Newton yonu: p^N = -B^{-1}g = -(1, 1/100) = (-1, -0.01)
p^N yonu: (-1, -0.01)/||(-1,-0.01)|| ≈ (-0.99995, -0.01)

Cauchy: x ve y yonunde esit gidiyor.
Newton: neredeyse tamamen x yonunde gidiyor (y yonunde egrilik cok buyuk oldugu icin kucuk adim).

Newton, yuksek egrilikli yonde kisa adim atiyor — daha akilli!
</details>

---

## Soru 25: lambda Bulmak — Diyagonal 2x2

B = [[10, 0], [0, 2]], g = (5, 4)^T, Delta = 1. Trust region icin lambda'yi bulunuz.

<details>
<summary>Cozum</summary>

Newton: p^N = (-5/10, -4/2) = (-0.5, -2), ||p^N|| = sqrt(0.25 + 4) = sqrt(4.25) ≈ 2.06 > 1

Kisit aktif. p = (-5/(10+lambda), -4/(2+lambda))

(5/(10+lambda))^2 + (4/(2+lambda))^2 = 1

lambda = 0: 0.25 + 4 = 4.25 (buyuk)
lambda = 2: 25/144 + 16/16 = 0.174 + 1 = 1.174
lambda = 3: 25/169 + 16/25 = 0.148 + 0.64 = 0.788
lambda = 2.5: 25/156.25 + 16/20.25 = 0.16 + 0.790 = 0.950
lambda = 2.3: 25/151.29 + 16/18.49 = 0.165 + 0.865 = 1.030

lambda ≈ 2.35: (5/12.35)^2 + (4/4.35)^2 = 0.164 + 0.846 = 1.010

lambda ≈ 2.38 ile:
p* ≈ (-5/12.38, -4/4.38) ≈ (-0.404, -0.913)
||p*|| ≈ sqrt(0.163 + 0.834) ≈ 0.999 ≈ 1 ✓
</details>

---

## Soru 26: Trust Region Iterasyonu — Adim Reddi Durumu

f(x) = sin(x), x_0 = 3 (radyan), Delta = 1. Trust region adimini hesaplayin ve rho'yu bulun.

<details>
<summary>Cozum</summary>

f(3) = sin(3) ≈ 0.1411
f'(3) = cos(3) ≈ -0.9900
f''(3) = -sin(3) ≈ -0.1411

Model: m(p) = 0.1411 - 0.9900p - 0.0706p^2

Kisitsiz min: m'(p) = -0.9900 - 0.1411p = 0 => p = -7.015

|p| = 7.015 >> 1 = Delta. Kisit aktif.

f'(3) < 0 yani inis yonu p > 0 tarafi. Ama B = f''(3) < 0, yani negatif egrilik!

m(p) minimumu sinirda: p* = +1 mu -1 mi?

m(1) = 0.1411 - 0.9900 - 0.0706 = -0.9195
m(-1) = 0.1411 + 0.9900 - 0.0706 = 1.0605

p* = 1 (inis yonunde sinirda)

f(3 + 1) = f(4) = sin(4) ≈ -0.7568

rho = (0.1411 - (-0.7568)) / (0.1411 - (-0.9195)) = 0.8979 / 1.0606 = 0.847

rho > 3/4 ve |p| = Delta => Bolge buyutulur, adim kabul.
</details>

---

## Soru 27: Pozitif Yari-Tanilik Kontrolu

B = [[3, 1], [1, -1]] ve lambda = 2 icin B + lambda I pozitif yari-tanili mi?

<details>
<summary>Cozum</summary>

B + 2I = [[5, 1], [1, 1]]

Ozdegerler: det(B + 2I - mu I) = 0
(5-mu)(1-mu) - 1 = 0
mu^2 - 6mu + 4 = 0
mu = (6 +- sqrt(36-16))/2 = (6 +- sqrt(20))/2 = (6 +- 4.472)/2

mu_1 = 5.236, mu_2 = 0.764

Her iki ozdeger > 0 => Pozitif tanili (dolayisiyla pozitif yari-tanili de). ✓

(B'nin kendisi pozitif tanili degil: ozdegerleri (3.24, -1.24). lambda = 2 eklemek yeterli oldu.)
</details>

---

## Soru 28: Tamamlayici Gevsetme

B = [[4, 0], [0, 4]], g = (2, 2)^T, Delta = 1. p* = (-0.5, -0.5) olarak verilmis. Bu cozum icin lambda'yi bulunuz ve tamamlayici gevsetme kosulunu dogrulayiniz.

<details>
<summary>Cozum</summary>

||p*|| = sqrt(0.25 + 0.25) = sqrt(0.5) ≈ 0.707 < 1 = Delta

Kisit pasif => lambda = 0 olmali.

Dogrulama: (B + 0*I)p* = Bp* = [[4,0],[0,4]](-0.5, -0.5)^T = (-2, -2) = -g ✓

Tamamlayici gevsetme: lambda(Delta - ||p*||) = 0 * (1 - 0.707) = 0 ✓
</details>

---

## Soru 29: Eliptik Guven Bolgesi

f(x,y) = 10^4 x^2 + y^2 fonksiyonunda (1, 1) noktasinda D = [[100, 0], [0, 1]] ile eliptik guven bolgesi kullanin. Delta = 1 icin ||Dp|| <= 1 kisiti altinda model minimumunu bulunuz.

<details>
<summary>Cozum</summary>

g = (2*10^4, 2), B = [[2*10^4, 0], [0, 2]]

q = Dp degiskeni ile: p = D^{-1}q = (q_1/100, q_2)

Donusturulmus problem: min m(D^{-1}q) s.t. ||q|| <= 1

Yeni gradyan (q uzayinda): D^{-1}g = (200, 2)
Yeni Hessian: D^{-1}BD^{-1} = [[2, 0], [0, 2]]

Bu simetrik bir problem! Newton adimi q uzayinda:
q^N = -[[1/2, 0],[0, 1/2]](200, 2) = (-100, -1)
||q^N|| ≈ 100 >> 1

Kisit aktif, ama B_new = 2I oldugu icin cozum basit:
q* = -Delta * g_new/||g_new|| = -(1/sqrt(40004))(200, 2) ≈ (-0.9999, -0.01)

p* = D^{-1}q* ≈ (-0.01, -0.01)

Eliptik bolge x yonunde cok kisa (1/100), y yonunde tam 1 adim izin veriyor. Bu, kotu olcekli probleme uyum saglar.
</details>

---

## Soru 30: Iki Iterasyon

f(x) = (x-3)^2 + 1, x_0 = 0, Delta_0 = 1, eta = 0.1, Delta_hat = 10. Iki iterasyon gerceklestirin.

<details>
<summary>Cozum</summary>

**Iterasyon 0:**
f(0) = 10, f'(0) = -6, f''(0) = 2

Newton: p^N = -(-6)/2 = 3, |p^N| = 3 > 1 = Delta_0. Kisit aktif.
p* = 1 (inis yonunde sinirda, f'(0) < 0 yani sag taraf)

f(0 + 1) = f(1) = 5
rho_0 = (10 - 5) / (10 - (10 - 6 + 0.5*2)) = 5 / (10 - 5) = 5/5 = 1.0

m(1) = 10 + (-6)(1) + (1/2)(2)(1)^2 = 10 - 6 + 1 = 5. Dolayisiyla m(0)-m(1) = 5.

rho_0 = 1.0 > 3/4 ve |p| = Delta => Delta_1 = min(2, 10) = 2. Adim kabul: x_1 = 1.

**Iterasyon 1:**
f(1) = 5, f'(1) = -4, f''(1) = 2

Newton: p^N = 4/2 = 2, |p^N| = 2 = Delta_1. Tam sinirda!
p* = 2

f(1 + 2) = f(3) = 1
m(2) = 5 + (-4)(2) + (1/2)(2)(4) = 5 - 8 + 4 = 1

rho_1 = (5 - 1)/(5 - 1) = 4/4 = 1.0

Mukkemmel! (Fonksiyon kuadratik, model tam.) x_2 = 3. Optimuma ulastik!
</details>

---

# ZOR (Soru 31–50)

---

## Soru 31: Trust Region — Capraz Hessian ile Tam Cozum

g = (10, 4)^T, B = [[5, 2], [2, 3]], Delta = 1. Trust region cozumunu bulunuz.

<details>
<summary>Cozum</summary>

Newton: det(B) = 15 - 4 = 11
B^{-1} = (1/11)[[3,-2],[-2,5]]
p^N = -(1/11)(3*10 + (-2)*4, (-2)*10 + 5*4) = -(1/11)(22, 0) = (-2, 0)
||p^N|| = 2 > 1

Kisit aktif. (B + lambda I)p = -g:

B + lambda I = [[5+lambda, 2], [2, 3+lambda]]

(B + lambda I)p = -g coz:
det = (5+lambda)(3+lambda) - 4 = lambda^2 + 8lambda + 11

p_1 = (-(3+lambda)*10 + 2*4) / (lambda^2 + 8lambda + 11) = (-10lambda - 22) / (lambda^2 + 8lambda + 11)
p_2 = (2*10 - (5+lambda)*4) / (lambda^2 + 8lambda + 11) = (-4lambda) / (lambda^2 + 8lambda + 11)

||p|| = 1:
p_1^2 + p_2^2 = 1

D = lambda^2 + 8lambda + 11 ile:
(10lambda + 22)^2 + (4lambda)^2 = D^2

100lambda^2 + 440lambda + 484 + 16lambda^2 = (lambda^2 + 8lambda + 11)^2

116lambda^2 + 440lambda + 484 = lambda^4 + 16lambda^3 + 86lambda^2 + 176lambda + 121

lambda^4 + 16lambda^3 - 30lambda^2 - 264lambda - 363 = 0

Sayisal cozum (Newton yontemi ile):
lambda ≈ 4.33

D = 4.33^2 + 8*4.33 + 11 = 18.75 + 34.64 + 11 = 64.39

p_1 = -(10*4.33 + 22)/64.39 = -65.3/64.39 ≈ -1.014...

Tekrar kontrol edelim lambda ≈ 4.5:
D = 20.25 + 36 + 11 = 67.25
p_1 = -(45+22)/67.25 = -67/67.25 = -0.9963
p_2 = -18/67.25 = -0.2677
||p|| = sqrt(0.9926 + 0.0717) = sqrt(1.064) = 1.032 (biraz buyuk)

lambda ≈ 4.7:
D = 22.09 + 37.6 + 11 = 70.69
p_1 = -69/70.69 = -0.9761
p_2 = -18.8/70.69 = -0.2659
||p|| = sqrt(0.953 + 0.071) = sqrt(1.024) = 1.012

lambda ≈ 5.0:
D = 25 + 40 + 11 = 76
p_1 = -72/76 = -0.9474
p_2 = -20/76 = -0.2632
||p|| = sqrt(0.8976 + 0.0693) = sqrt(0.967) = 0.983

lambda ≈ 4.85:
D = 23.52 + 38.8 + 11 = 73.32
p_1 = -70.5/73.32 = -0.9616
p_2 = -19.4/73.32 = -0.2646
||p|| = sqrt(0.925 + 0.070) = sqrt(0.995) ≈ 0.998

lambda ≈ 4.84, p* ≈ (-0.962, -0.265), ||p*|| ≈ 1.0
</details>

---

## Soru 32: Dogleg ile rho_k Hesabi

f(x,y) = 3x^2 + y^2, x_0 = (2, 3), Delta = 1. Dogleg cozumunu bulup rho hesaplayiniz.

<details>
<summary>Cozum</summary>

f(2,3) = 12 + 9 = 21
g = (12, 6), B = [[6, 0], [0, 2]]

p^B = -B^{-1}g = (-2, -3), ||p^B|| = sqrt(4+9) = sqrt(13) ≈ 3.606 > 1

p^U = -(g^T g / g^T B g) g
g^T g = 144 + 36 = 180
g^T B g = (12)(72) + (6)(12) = 864 + 72 = 936
p^U = -(180/936)(12, 6) = -0.1923(12, 6) = (-2.308, -1.154)
||p^U|| = sqrt(5.327 + 1.332) = sqrt(6.659) ≈ 2.580 > Delta = 1

p^U bile disarida! Birinci parcada sinirla kesisim:
||tau * p^U|| = 1 => tau * 2.580 = 1 => tau = 0.3876

p* = 0.3876 * (-2.308, -1.154) = (-0.895, -0.447)
||p*|| = sqrt(0.801 + 0.200) ≈ 1.0 ✓

f(2-0.895, 3-0.447) = f(1.105, 2.553) = 3(1.221) + 6.518 = 3.664 + 6.518 = 10.182

m(p*): g^T p = 12(-0.895) + 6(-0.447) = -10.74 - 2.682 = -13.422
Bp* = (6(-0.895), 2(-0.447)) = (-5.37, -0.894)
p^T Bp = (-0.895)(-5.37) + (-0.447)(-0.894) = 4.806 + 0.400 = 5.206
m(p*) = 21 - 13.422 + 2.603 = 10.181

rho = (21 - 10.182) / (21 - 10.181) = 10.818 / 10.819 ≈ 1.0

(Fonksiyon kuadratik, model tam. rho ≈ 1.)
</details>

---

## Soru 33: Eyer Noktasinda Trust Region

f(x,y) = x^2 - 4y^2 + 2x fonksiyonunda x_0 = (-1, 0). Delta = 2. Trust region adimini bulunuz.

<details>
<summary>Cozum</summary>

f(-1, 0) = 1 - 0 - 2 = -1
g = (2x+2, -8y) |(_{-1,0}) = (0, 0)

Gradyan sifir! Ama bu bir minimum degil (eyer noktasi, cunku B belirsiz).

B = [[2, 0], [0, -8]]

Model: m(p) = -1 + 0 + (1/2)p^T [[2,0],[0,-8]] p = -1 + p_1^2 - 4p_2^2

min m(p) s.t. p_1^2 + p_2^2 <= 4

p_2^2 maksimize edilmeli (eksi isareti). p_1 = 0, p_2 = +-2.

m(0, +-2) = -1 + 0 - 16 = -17

Optimallik: (B + lambda I)p* = -g = 0
[[2+lambda, 0], [0, -8+lambda]](0, 2) = (0, (-8+lambda)*2) = (0, 0)
lambda = 8

B + 8I = [[10, 0], [0, 0]] — pozitif yari-tanili ✓
lambda(Delta - ||p*||) = 8(2-2) = 0 ✓

Trust region eyer noktasindan kaciyor: p* = (0, +-2).
</details>

---

## Soru 34: Uc Iterasyon — Tam Algoritma

f(x) = x^4 - 4x^2 + 4 = (x^2 - 2)^2, x_0 = 3, Delta_0 = 1, eta = 0.2, Delta_hat = 8. Uc iterasyon gerceklestirin.

<details>
<summary>Cozum</summary>

**Iterasyon 0:**
f(3) = 81 - 36 + 4 = 49
f'(3) = 4(27) - 8(3) = 108 - 24 = 84
f''(3) = 12(9) - 8 = 100

Newton: p^N = -84/100 = -0.84, |p^N| = 0.84 < Delta_0 = 1. Kisit pasif!

p* = -0.84, x_1 = 3 - 0.84 = 2.16

f(2.16) = (2.16)^4 - 4(2.16)^2 + 4 = 21.77 - 18.66 + 4 = 7.11
m(-0.84) = 49 + 84(-0.84) + 50(0.84)^2 = 49 - 70.56 + 35.28 = 13.72

rho = (49 - 7.11) / (49 - 13.72) = 41.89 / 35.28 = 1.187

rho > 3/4. |p| = 0.84 < Delta = 1, yani kisit aktif degil. Delta_1 = Delta_0 = 1. Adim kabul.

**Iterasyon 1:**
f(2.16) ≈ 7.11
f'(2.16) = 4(2.16)^3 - 8(2.16) = 40.31 - 17.28 = 23.03
f''(2.16) = 12(2.16)^2 - 8 = 55.96 - 8 = 47.96

Newton: p^N = -23.03/47.96 = -0.480, |p^N| < 1. Kisit pasif.

x_2 = 2.16 - 0.480 = 1.680

f(1.680) = (1.680)^4 - 4(1.680)^2 + 4 = 7.97 - 11.29 + 4 = 0.68

rho hesabi: m(p) = 7.11 + 23.03(-0.480) + (1/2)(47.96)(0.480)^2 = 7.11 - 11.05 + 5.53 = 1.59
rho = (7.11 - 0.68) / (7.11 - 1.59) = 6.43 / 5.52 = 1.165

Adim kabul, Delta_2 = 1.

**Iterasyon 2:**
f(1.680) ≈ 0.68
f'(1.680) = 4(1.680)^3 - 8(1.680) = 18.96 - 13.44 = 5.52
f''(1.680) = 12(1.680)^2 - 8 = 33.87 - 8 = 25.87

Newton: p^N = -5.52/25.87 = -0.213, |p^N| < 1. Kisit pasif.

x_3 = 1.680 - 0.213 = 1.467

f(1.467) = (1.467)^4 - 4(1.467)^2 + 4 = 4.63 - 8.61 + 4 = 0.02

Cozume (x = sqrt(2) ≈ 1.414) hizla yaklasiyoruz!
</details>

---

## Soru 35: 2D Alt-Uzay Minimizasyonu

g = (6, 2)^T, B = [[3, 0], [0, 1]], Delta = 1. span{g, B^{-1}g} icinde trust region cozumunu bulunuz.

<details>
<summary>Cozum</summary>

B^{-1}g = (6/3, 2/1) = (2, 2)

span{g, B^{-1}g} = span{(6,2), (2,2)}

p = alpha (6, 2) + beta (2, 2) = (6alpha + 2beta, 2alpha + 2beta)

Kisit: ||p||^2 = (6alpha+2beta)^2 + (2alpha+2beta)^2 <= 1

Model: m(p) = f_k + g^T p + (1/2)p^T B p

g^T p = 6(6alpha+2beta) + 2(2alpha+2beta) = 36alpha + 12beta + 4alpha + 4beta = 40alpha + 16beta

Bp = [[3,0],[0,1]](6alpha+2beta, 2alpha+2beta) = (18alpha+6beta, 2alpha+2beta)
p^T Bp = (6a+2b)(18a+6b) + (2a+2b)(2a+2b) = 108a^2+36ab+36ab+12b^2 + 4a^2+4ab+4ab+4b^2
= 112a^2 + 80ab + 16b^2

m(p) = f_k + 40a + 16b + (1/2)(112a^2 + 80ab + 16b^2)
= f_k + 40a + 16b + 56a^2 + 40ab + 8b^2

Bu 2 degiskenli kisitli optimizasyon problemi Lagrange carpanlari ile cozulur.

Newton adimi: p^N = -B^{-1}g = (-2, -2), ||p^N|| = 2sqrt(2) ≈ 2.83 > 1

Kisit aktif olacak. Sayisal olarak cozum:
Lagrange: grad_p m = lambda * 2p (sinirda)

Bu zaten bildigimiz (B+lambda I)p = -g formu!
p = (-6/(3+lambda), -2/(1+lambda))

36/(3+lambda)^2 + 4/(1+lambda)^2 = 1

lambda ≈ 4.56: p* ≈ (-0.793, -0.360), ||p*|| ≈ sqrt(0.629+0.130) ≈ 0.871
lambda ≈ 3.5: p* ≈ (-0.923, -0.444), ||p*|| ≈ sqrt(0.852+0.198) ≈ 1.025

lambda ≈ 3.6: p* ≈ (-0.909, -0.435), ||p*|| ≈ sqrt(0.826+0.189) ≈ 1.008
lambda ≈ 3.65: p ≈ (-0.902, -0.430), ||p|| ≈ 0.999

p* ≈ (-0.902, -0.430)
</details>

---

## Soru 36: Rosenbrock Fonksiyonunda Trust Region

f(x,y) = (1-x)^2 + 100(y-x^2)^2, x_0 = (-1, 1). Kuadratik modeli olusturun ve Delta = 0.5 icin Newton adiminin durumunu belirleyin.

<details>
<summary>Cozum</summary>

f(-1, 1) = (1-(-1))^2 + 100(1-1)^2 = 4 + 0 = 4

df/dx = -2(1-x) + 100 * 2(y-x^2)(-2x) = -2(1-x) - 400x(y-x^2)
df/dx(-1,1) = -2(2) - 400(-1)(1-1) = -4 - 0 = -4

df/dy = 200(y-x^2)
df/dy(-1,1) = 200(1-1) = 0

g = (-4, 0)^T

d^2f/dx^2 = 2 - 400(y-x^2) + 800x^2 = 2 - 400(y-3x^2)
d^2f/dx^2(-1,1) = 2 - 400(1-3) = 2 + 800 = 802

d^2f/dxdy = -400x
d^2f/dxdy(-1,1) = 400

d^2f/dy^2 = 200
d^2f/dy^2(-1,1) = 200

B = [[802, 400], [400, 200]]

det(B) = 802*200 - 400*400 = 160400 - 160000 = 400

B^{-1} = (1/400)[[200, -400], [-400, 802]] = [[0.5, -1], [-1, 2.005]]

p^N = -B^{-1}g = -[[0.5,-1],[-1,2.005]](-4, 0) = -(−2, 4) = (2, -4)

||p^N|| = sqrt(4 + 16) = sqrt(20) ≈ 4.47 >> 0.5 = Delta

Newton adimi cok buyuk! Trust region bunu budayacak. Bu, Rosenbrock fonksiyonunun "dar vadi" yapisinin Newton'u yanilttigi klasik bir ornek.
</details>

---

## Soru 37: Farkli eta Degerleri ile Karar

rho_k = 0.15 icin eta = 0.05, eta = 0.1, eta = 0.2 degerlerinde adim kabul edilir mi?

<details>
<summary>Cozum</summary>

eta = 0.05: rho_k = 0.15 > 0.05 => Adim KABUL
eta = 0.1: rho_k = 0.15 > 0.1 => Adim KABUL
eta = 0.2: rho_k = 0.15 < 0.2 => Adim REDDEDILIR

Hepsinde rho_k = 0.15 < 1/4 oldugu icin bolge kucultulur: Delta_{k+1} = Delta_k/4.

eta kucuk secilirse daha "hosgurulu" olunur — kucuk ilerlemeler bile kabul edilir.
eta buyuk secilirse daha "secici" olunur — yalnizca iyi adimlar kabul edilir.
</details>

---

## Soru 38: Cauchy ile Dogleg Karsilastirmasi

g = (3, 4)^T, B = [[2, 0], [0, 2]], Delta = 2. Cauchy noktasi ile Dogleg cozumunu karsilastirin ve model degerlerini hesaplayin.

<details>
<summary>Cozum</summary>

||g|| = 5, f_k = 0 diyelim.

**Cauchy:**
g^T Bg = (3,4)(6,8) = 18+32 = 50
p_S = -(2/5)(3,4) = (-1.2, -1.6)
tau = min(125/(2*50), 1) = min(1.25, 1) = 1
p^C = (-1.2, -1.6), ||p^C|| = 2.0 = Delta (sinirda)

m(p^C) = 0 + (3,4)(-1.2,-1.6) + (1/2)(-1.2,-1.6)[[2,0],[0,2]](-1.2,-1.6)^T
= (-3.6-6.4) + (1/2)(2*1.44 + 2*2.56)
= -10 + (1/2)(2.88+5.12) = -10 + 4 = -6

**Dogleg:**
p^U = -(g^Tg/g^TBg)g = -(25/50)(3,4) = (-1.5, -2), ||p^U|| = 2.5
p^B = -B^{-1}g = (-1.5, -2), ||p^B|| = 2.5

p^U = p^B! (B = 2I oldugu icin Cauchy kisitsiz noktasi = Newton noktasi)

||p^B|| = 2.5 > 2 = Delta. Newton disarida.
||p^U|| = 2.5 > 2 = Delta. p^U de disarida!

Sinira oturt: p = (Delta/||p^B||) * p^B = (2/2.5)(-1.5,-2) = (-1.2, -1.6)

**Sonuc:** B = cI (sabit carpi birim matris) oldugunda Cauchy = Dogleg = olcekli Newton!

m(p_dogleg) = m(p^C) = -6
</details>

---

## Soru 39: Homework Stili — Newton + Armijo + Trust Region

f(x_1, x_2) = x_1^2 + x_2^2 + x_1 x_2 - 3x_1 fonksiyonunda x_0 = (0, 0).
(a) Newton adimini bulun.
(b) Trust region adimini mu = 1 ile bulun.
(c) Her iki adim icin rho hesaplayin.

<details>
<summary>Cozum</summary>

f(0,0) = 0
g = (2x_1 + x_2 - 3, 2x_2 + x_1)|(0,0) = (-3, 0)
B = [[2, 1], [1, 2]]

**(a) Newton:**
det(B) = 4 - 1 = 3
B^{-1} = (1/3)[[2,-1],[-1,2]]
p^N = -(1/3)(2(-3)+(-1)(0), (-1)(-3)+2(0)) = -(1/3)(-6, 3) = (2, -1)

x_1 = (2, -1). f(2,-1) = 4+1-2-6 = -3

**(b) Trust region (mu=1):**
B + I = [[3, 1], [1, 3]], det = 8
(B+I)^{-1} = (1/8)[[3,-1],[-1,3]]
p_{TR} = -(1/8)(3(-3)+(-1)(0), (-1)(-3)+3(0)) = -(1/8)(-9, 3) = (9/8, -3/8)

x_1^{TR} = (9/8, -3/8). Delta = ||p_{TR}|| = sqrt(81/64 + 9/64) = sqrt(90/64) = sqrt(90)/8 ≈ 1.186

f(9/8, -3/8) = 81/64 + 9/64 + (-27/64) - 27/8 = 63/64 - 27/8 = 63/64 - 216/64 = -153/64 ≈ -2.391

**(c) rho:**
Newton: m(p^N) = 0 + (-3)(2) + (0)(-1) + (1/2)(2,-1)[[2,1],[1,2]](2,-1)^T
Bp^N = (2*2+1*(-1), 1*2+2*(-1)) = (3, 0)
(p^N)^T B p^N = 2(3)+(-1)(0) = 6
m(p^N) = 0 - 6 + 3 = -3

rho_Newton = (0 - (-3)) / (0 - (-3)) = 3/3 = 1.0 (mukkemmel, fonksiyon kuadratik!)

Trust region:
m(p_{TR}) = 0 + (-3)(9/8) + (1/2)(9/8,-3/8) B (9/8,-3/8)^T
g^T p = -27/8
Bp = (2*9/8+1*(-3/8), 1*9/8+2*(-3/8)) = (15/8, 3/8)
p^T Bp = (9/8)(15/8)+(-3/8)(3/8) = 135/64 - 9/64 = 126/64
m(p_{TR}) = 0 - 27/8 + 63/64 = -216/64 + 63/64 = -153/64 ≈ -2.391

rho_TR = (0 - (-2.391)) / (0 - (-2.391)) = 1.0

Her ikisi de mukkemmel (kuadratik fonksiyon).
</details>

---

## Soru 40: Belirsiz (Indefinite) Hessian ile Trust Region

g = (1, -1)^T, B = [[2, 0], [0, -3]], Delta = 1. Trust region cozumunu bulunuz.

<details>
<summary>Cozum</summary>

B'nin ozdegerleri: 2 ve -3 (belirsiz — pozitif tanili degil!)

Newton: p^N = -B^{-1}g = -(1/2, 1/3) = (-0.5, 0.333)
||p^N|| = sqrt(0.25 + 0.111) = 0.601 < 1 = Delta

Ama! B pozitif tanili degil, yani p^N bir minimum degil, eyer noktasi veya maksimum olabilir.

m(p^N) = f_k + g^T p^N + (1/2)(p^N)^T B p^N
g^T p^N = (1)(-0.5) + (-1)(0.333) = -0.833
p^T Bp = (-0.5)(2)(-0.5) + (0.333)(-3)(0.333) = 0.5 - 0.333 = 0.167
m(p^N) = f_k - 0.833 + 0.083 = f_k - 0.75

Ama sinirda daha iyi bir cozum olabilir:
(B + lambda I)p = -g: p = (-1/(2+lambda), 1/(−3+lambda))

||p|| = 1: 1/(2+lambda)^2 + 1/(-3+lambda)^2 = 1

lambda >= 3 olmali (B+lambda I pozitif yari-tanili icin)

lambda = 3: 1/25 + 1/0 = inf (kutup!)
lambda = 3.5: 1/30.25 + 1/0.25 = 0.033 + 4 = 4.033 (buyuk)
lambda = 5: 1/49 + 1/4 = 0.020 + 0.25 = 0.270
lambda = 10: 1/144 + 1/49 = 0.007 + 0.020 = 0.027 (kucuk)
lambda = 4: 1/36 + 1/1 = 0.028 + 1 = 1.028
lambda = 4.02: 1/36.24 + 1/(1.02)^2 = 0.0276 + 0.961 = 0.989

lambda ≈ 4.01: p = (-1/6.01, 1/1.01) ≈ (-0.166, 0.990)
||p|| ≈ sqrt(0.028 + 0.980) ≈ 1.003

lambda ≈ 4.02, p* ≈ (-0.166, 0.989), ||p*|| ≈ 1.0

m(p*) = f_k + (1)(-0.166) + (-1)(0.989) + (1/2)[2(0.028) + (-3)(0.978)]
= f_k - 0.166 - 0.989 + (1/2)(0.056 - 2.934)
= f_k - 1.155 + (-1.439) = f_k - 2.594

Bu, Newton cozumundan (f_k - 0.75) cok daha iyi! Negatif egrilik yonunde sinira kadar giderek buyuk kazanc elde ettik.
</details>

---

## Soru 41: Yakinsaklik Orani Analizi

f(x) = x^4, x_0 = 1. Trust region Delta_k = 0.5 (sabit) ile ilk 3 iterasyonu gerceklestirin. Yakinsaklik oranini gozlemleyin.

<details>
<summary>Cozum</summary>

**Iterasyon 0:** x_0 = 1
f(1) = 1, f'(1) = 4, f''(1) = 12
Newton: p^N = -4/12 = -1/3 ≈ -0.333, |p^N| < 0.5. Kisit pasif.
x_1 = 1 - 1/3 = 2/3 ≈ 0.667

**Iterasyon 1:** x_1 = 2/3
f(2/3) = 16/81 ≈ 0.198, f'(2/3) = 4(8/27) = 32/27 ≈ 1.185, f''(2/3) = 12(4/9) = 16/3 ≈ 5.333
Newton: p^N = -1.185/5.333 = -0.222, |p^N| < 0.5. Kisit pasif.
x_2 = 0.667 - 0.222 = 0.444

**Iterasyon 2:** x_2 = 0.444
f(0.444) = 0.0389, f'(0.444) = 4(0.0878) = 0.351, f''(0.444) = 12(0.198) = 2.371
Newton: p^N = -0.351/2.371 = -0.148, |p^N| < 0.5. Kisit pasif.
x_3 = 0.444 - 0.148 = 0.296

Hata orani: |x_k - 0| / |x_{k-1} - 0|
|x_1|/|x_0| = 0.667
|x_2|/|x_1| = 0.667
|x_3|/|x_2| = 0.667

Lineer yakinsaklik orani 2/3! (Newton normalde kuadratik yakinsar ama x*=0 dejenere bir minimum — f''(0)=0.)
</details>

---

## Soru 42: Buyuk Olcek Farki — Kotu Olceklenme

f(x,y) = 100x^2 + y^2, x_0 = (1, 100). Daire seklindeki trust region (Delta=10) ve eliptik trust region (D=[[10,0],[0,1]], Delta=10) ile cozumleri karsilastiriniz.

<details>
<summary>Cozum</summary>

g = (200, 200), B = [[200, 0], [0, 2]]

Newton: p^N = (-200/200, -200/2) = (-1, -100), ||p^N|| ≈ 100

**Daire trust region (Delta=10):**
(B+lambda I)p = -g => p = (-200/(200+lambda), -200/(2+lambda))
||p|| = 10:

lambda ≈ 10 ile: p ≈ (-200/210, -200/12) = (-0.952, -16.67), ||p|| ≈ 16.7 (buyuk)
lambda ≈ 20 ile: p ≈ (-200/220, -200/22) = (-0.909, -9.09), ||p|| ≈ 9.14 (yakin)
lambda ≈ 18.5: p ≈ (-0.915, -9.76), ||p|| ≈ 9.80
lambda ≈ 19.5: p ≈ (-0.911, -9.30), ||p|| ≈ 9.34

lambda ≈ 19: p ≈ (-0.913, -9.52), ||p|| ≈ 9.57

Daire bolge ile: x yonunde cok az ilerleniyor (-0.91) ama y yonunde buyuk adim (-9.5). Oysa optimumda x yonu daha onemli!

**Eliptik trust region (||Dp|| <= 10):**
q = Dp, p = D^{-1}q = (q_1/10, q_2)
Yeni gradyan: D^{-1}g = (20, 200)
Yeni Hessian: D^{-1}BD^{-1} = [[2, 0], [0, 2]]

Newton (q uzayi): q^N = -(10, 100), ||q^N|| ≈ 100.5 > 10
Kisit aktif: q* ≈ 10 * (-10,-100)/100.5 ≈ (-0.995, -9.95)
p* = D^{-1}q* ≈ (-0.0995, -9.95)

Eliptik bolge x yonunu "korur" — her iki yonde orantili ilerleme saglar.
</details>

---

## Soru 43: Model Kalitesinin Bozulmasi

f(x) = x + x^3, x_0 = 1, Delta = 2. Model tahmini neden kotu olur?

<details>
<summary>Cozum</summary>

f(1) = 2, f'(1) = 1 + 3 = 4, f''(1) = 6

Model: m(p) = 2 + 4p + 3p^2

Kisitsiz min: m'(p) = 4 + 6p = 0 => p = -2/3, |p| < 2. Kisit pasif.

m(-2/3) = 2 + 4(-2/3) + 3(4/9) = 2 - 8/3 + 4/3 = 2 - 4/3 = 2/3

f(1 - 2/3) = f(1/3) = 1/3 + 1/27 = 10/27 ≈ 0.370

rho = (2 - 0.370) / (2 - 0.667) = 1.630/1.333 = 1.223

Simdi Delta = 2 ile deneyelim: p = -2 (sinirda)
m(-2) = 2 + 4(-2) + 3(4) = 2 - 8 + 12 = 6
f(1-2) = f(-1) = -1 - 1 = -2

rho = (2 - (-2)) / (2 - 6) = 4/(-4) = -1.0

Model 6'ya cikacak dedi ama fonksiyon -2'ye dustu! Buyuk Delta'da model cok kotu cunku kubik terim baskın oluyor ve kuadratik model bunu yakalayamiyor.
</details>

---

## Soru 44: Lagrange Carpani Yorumlama

B = [[8, 0], [0, 2]], g = (4, 2)^T, Delta = 0.5 icin lambda'yi bulun ve yorumlayiniz.

<details>
<summary>Cozum</summary>

Newton: p^N = (-4/8, -2/2) = (-0.5, -1), ||p^N|| = sqrt(0.25+1) = sqrt(1.25) ≈ 1.118 > 0.5

Kisit aktif: p = (-4/(8+lambda), -2/(2+lambda))

16/(8+lambda)^2 + 4/(2+lambda)^2 = 0.25

lambda = 0: 16/64 + 4/4 = 0.25 + 1 = 1.25
lambda = 2: 16/100 + 4/16 = 0.16 + 0.25 = 0.41
lambda = 4: 16/144 + 4/36 = 0.111 + 0.111 = 0.222
lambda = 3: 16/121 + 4/25 = 0.132 + 0.16 = 0.292
lambda = 3.5: 16/132.25 + 4/30.25 = 0.121 + 0.132 = 0.253

lambda ≈ 3.45: yaklaşık 0.25

p* ≈ (-4/11.45, -2/5.45) ≈ (-0.349, -0.367)
||p*|| ≈ sqrt(0.122+0.135) ≈ 0.507 (yakin)

**Yorum:** lambda = 3.45 oldukca buyuk — Newton adimini onemli olcude budamak gerekti. B'nin en kucuk ozdegeri 2, lambda bunun 1.7 kati. Bu, kisitlamanin cok aktif oldugu anlamina gelir.
</details>

---

## Soru 45: Cok Adimli Trust Region — Yaricap Dinamigi

f(x,y) = x^2 + y^2, x_0 = (10, 10), Delta_0 = 1, eta = 0.1, Delta_hat = 100. 4 iterasyon boyunca Delta'nin degisimini izleyiniz.

<details>
<summary>Cozum</summary>

B = [[2,0],[0,2]] (sabit). Her iterasyonda model tam!

**Iter 0:** g = (20,20), ||p^N|| = ||(−10,−10)|| = 14.14 > 1
p* = (−1/sqrt(2), −1/sqrt(2)) ≈ (−0.707, −0.707)
f: 200 -> f(9.293, 9.293) = 172.72. rho = 1.0 (kuadratik fonksiyon)
rho > 3/4, ||p|| = Delta => Delta_1 = min(2, 100) = 2

**Iter 1:** x = (9.293, 9.293), g = (18.586, 18.586), ||p^N|| = 13.14 > 2
p* = 2/sqrt(2) * (−1/sqrt(2), −1/sqrt(2)) = (−1.414, −1.414)
rho = 1.0 => Delta_2 = min(4, 100) = 4

**Iter 2:** x = (7.879, 7.879), g = (15.758, 15.758), ||p^N|| = 11.14 > 4
p* = (−2.828, −2.828). rho = 1.0 => Delta_3 = min(8, 100) = 8

**Iter 3:** x = (5.050, 5.050), g = (10.1, 10.1), ||p^N|| = 7.14 > 8? Hayir! 7.14 < 8.
Newton kisit icinde! p* = (−5.050, −5.050). rho = 1.0.
Delta_4 = 8 (||p|| < Delta, kisit pasif, buyutme yok)

x_4 = (0, 0). Optimuma ulastik!

Delta dizisi: 1 -> 2 -> 4 -> 8. Her basarili adimda ikiye katlandi.
</details>

---

## Soru 46: Iki Minimumlu Fonksiyon

f(x) = x^4 - 2x^2 = x^2(x^2-2), x_0 = 0.3, Delta = 0.5. Trust region hangi minimuma gider?

<details>
<summary>Cozum</summary>

Minimumlar: x = +-sqrt(2) ≈ +-1.414

f(0.3) = 0.0081 - 0.18 = -0.1719
f'(0.3) = 4(0.027) - 4(0.3) = 0.108 - 1.2 = -1.092
f''(0.3) = 12(0.09) - 4 = 1.08 - 4 = -2.92

B = -2.92 < 0! Negatif egrilik.

Model: m(p) = -0.1719 - 1.092p - 1.46p^2

f'(0.3) < 0 yani inis yonu pozitif tarafta. Negatif egrilik demek model surekli azaliyor.

Sinirda: p* = 0.5 (sag tarafa, inis yonunde)

x_1 = 0.3 + 0.5 = 0.8. f(0.8) = 0.4096 - 1.28 = -0.8704

Devam edersek: f'(0.8) = 4(0.512) - 4(0.8) = 2.048 - 3.2 = -1.152 (hala negatif, saga git)

Algoritma x = +sqrt(2) ≈ 1.414 minimumuna yaklasacak (baslangic noktasina en yakin minimum).
</details>

---

## Soru 47: Cauchy Noktasinin Yeterliligi — Teorem 4.5 Kontrolu

g = (6, 8)^T, B = [[3, 0], [0, 3]], Delta = 2. Cauchy noktasinin sagladigi model azalmasinin yeterli azalma kosulunu sagladigini dogrulayiniz.

<details>
<summary>Cozum</summary>

||g|| = 10, ||B|| = 3

Yeterli azalma kosulu: m(0) - m(p^C) >= c_1 ||g|| min(Delta, ||g||/||B||)

Sag taraf: c_1 * 10 * min(2, 10/3) = c_1 * 10 * 2 = 20 c_1

**Cauchy noktasi:**
g^T B g = (6)(18) + (8)(24) = 108 + 192 = 300
tau = min(||g||^3/(Delta * g^T B g), 1) = min(1000/600, 1) = 1

p^C = -(2/10)(6, 8) = (-1.2, -1.6), ||p^C|| = 2 = Delta

m(p^C):
g^T p^C = 6(-1.2) + 8(-1.6) = -7.2 - 12.8 = -20
Bp^C = (3(-1.2), 3(-1.6)) = (-3.6, -4.8)
(p^C)^T B p^C = (-1.2)(-3.6) + (-1.6)(-4.8) = 4.32 + 7.68 = 12

m(0) - m(p^C) = -(g^T p^C) - (1/2)(p^C)^T B p^C = 20 - 6 = 14

Kosul: 14 >= 20 c_1 => c_1 <= 0.7

c_1 = 0.5 icin: 14 >= 10 ✓. Yeterli azalma saglaniyor.
</details>

---

## Soru 48: Trust Region — Dogrusal Fonksiyon

f(x,y) = 2x + 3y (dogrusal). x_0 = (5, 5), Delta = 1, B = 0 (sifir matris — ikinci turev yok). Trust region adimi ne olur?

<details>
<summary>Cozum</summary>

g = (2, 3), B = [[0,0],[0,0]]

Model: m(p) = f_k + g^T p + 0 = f_k + 2p_1 + 3p_2

Bu tamamen lineer! min(2p_1 + 3p_2) s.t. p_1^2 + p_2^2 <= 1

Lineer fonksiyonu kure icinde minimize etmek icin: p = -Delta * g/||g||

||g|| = sqrt(4+9) = sqrt(13) ≈ 3.606

p* = -(1/3.606)(2, 3) = (-0.555, -0.832)

Bu tam steepest descent yonu! B = 0 oldugunda trust region tam olarak steepest descent olur.

m(p*) = f_k + (2)(-0.555) + (3)(-0.832) = f_k - 1.110 - 2.496 = f_k - 3.606

(Model azalmasi = ||g|| * Delta = 3.606 * 1 = 3.606)
</details>

---

## Soru 49: Uc Boyutlu Trust Region

f(x,y,z) = x^2 + 2y^2 + 4z^2 + 2xy fonksiyonunda x_0 = (1, 1, 1), Delta = 1. Newton adiminin trust region icinde olup olmadigini belirleyiniz.

<details>
<summary>Cozum</summary>

g = (2x+2y, 4y+2x, 8z) |(1,1,1) = (4, 6, 8)

B = [[2, 2, 0],
     [2, 4, 0],
     [0, 0, 8]]

Newton: B p = -g

| 2  2  0 | |p_1|   |-4|
| 2  4  0 | |p_2| = |-6|
| 0  0  8 | |p_3|   |-8|

Ucuncu denklem: 8 p_3 = -8 => p_3 = -1

Ilk iki denklem: 2p_1 + 2p_2 = -4, 2p_1 + 4p_2 = -6
Fark: 2p_2 = -2 => p_2 = -1
2p_1 + 2(-1) = -4 => p_1 = -1

p^N = (-1, -1, -1)

||p^N|| = sqrt(1 + 1 + 1) = sqrt(3) ≈ 1.732 > 1 = Delta

Newton adimi guven bolgesi disinda! Trust region alt problemini cozmek gerekir.
</details>

---

## Soru 50: Karmasik Fonksiyon — Tam Iterasyon

f(x,y) = e^x + e^y + e^{xy}, x_0 = (0, 0), Delta = 0.5, eta = 0.1. Bir iterasyon gerceklestirin.

<details>
<summary>Cozum</summary>

f(0,0) = 1 + 1 + 1 = 3

df/dx = e^x + y e^{xy} => df/dx(0,0) = 1 + 0 = 1
df/dy = e^y + x e^{xy} => df/dy(0,0) = 1 + 0 = 1
g = (1, 1)

d^2f/dx^2 = e^x + y^2 e^{xy} => 1
d^2f/dy^2 = e^y + x^2 e^{xy} => 1
d^2f/dxdy = e^{xy} + xy e^{xy} => 1

B = [[1, 1], [1, 1]]

B tekil (singular)! det = 0. Ozdegerler: 0 ve 2.

Newton adimi TANIMSIZ (B terslenemez). Ama trust region calisir!

(B + lambda I) p = -g:
[[1+lambda, 1], [1, 1+lambda]] p = (-1, -1)

det = (1+lambda)^2 - 1 = lambda^2 + 2lambda = lambda(lambda+2)

p_1 = (-(1+lambda)+1) / (lambda^2+2lambda) = -lambda/(lambda^2+2lambda) = -1/(lambda+2)
p_2 = (1-(1+lambda)) / (lambda^2+2lambda) = -lambda/(lambda^2+2lambda) = -1/(lambda+2)

||p|| = sqrt(2)/(lambda+2)

||p|| = 0.5: sqrt(2)/(lambda+2) = 0.5 => lambda + 2 = 2sqrt(2) => lambda = 2sqrt(2) - 2 ≈ 0.828

p* = (-1/(2sqrt(2)), -1/(2sqrt(2))) = (-sqrt(2)/4, -sqrt(2)/4) ≈ (-0.354, -0.354)

||p*|| = sqrt(0.125 + 0.125) = 0.5 ✓

x_1 = (0-0.354, 0-0.354) = (-0.354, -0.354)

f(-0.354, -0.354) = e^{-0.354} + e^{-0.354} + e^{0.125} = 0.702 + 0.702 + 1.133 = 2.537

m(p*) = 3 + (1,1)(-0.354,-0.354) + (1/2)(-0.354,-0.354)[[1,1],[1,1]](-0.354,-0.354)^T
g^T p = -0.708
Bp = [[1,1],[1,1]](-0.354,-0.354) = (-0.708, -0.708)
p^T Bp = (-0.354)(-0.708)+(-0.354)(-0.708) = 0.251 + 0.251 = 0.501
m(p*) = 3 - 0.708 + 0.251 = 2.543

rho = (3 - 2.537) / (3 - 2.543) = 0.463 / 0.457 = 1.013

rho > 3/4, ||p*|| = Delta => Delta_1 = min(1.0, Delta_hat) = 1.0. Adim kabul.

**Not:** B tekil olmasina ragmen trust region sorunsuz calisti! lambda > 0 ekleyerek B + lambda I'yi tersinir yaptik.
</details>
