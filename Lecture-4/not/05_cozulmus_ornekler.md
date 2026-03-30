# Cozulmus Ornekler

## Ornek 1: Kuadratik Model Olusturma

**Problem:** f(x,y) = x^4 + 2x^3 + 24x^2 + y^4 + 12y^2 fonksiyonu icin (x_0, y_0) = (2, 1) noktasinda kuadratik modeli m(p) olusturunuz.

**Cozum:**

**Adim 1:** Fonksiyon degerini hesapla.

$$f(2,1) = 2^4 + 2 \cdot 2^3 + 24 \cdot 2^2 + 1^4 + 12 \cdot 1^2 = 16 + 16 + 96 + 1 + 12 = 141$$

**Adim 2:** Gradyani hesapla.

$$\nabla f(x,y) = \begin{pmatrix} 4x^3 + 6x^2 + 48x \\ 4y^3 + 24y \end{pmatrix}$$

$$\nabla f(2,1) = \begin{pmatrix} 4(8) + 6(4) + 48(2) \\ 4(1) + 24(1) \end{pmatrix} = \begin{pmatrix} 32 + 24 + 96 \\ 4 + 24 \end{pmatrix} = \begin{pmatrix} 152 \\ 28 \end{pmatrix}$$

**Adim 3:** Hessian matrisini hesapla.

$$\nabla^2 f(x,y) = \begin{pmatrix} 12x^2 + 12x + 48 & 0 \\ 0 & 12y^2 + 24 \end{pmatrix}$$

$$\nabla^2 f(2,1) = \begin{pmatrix} 12(4) + 12(2) + 48 & 0 \\ 0 & 12(1) + 24 \end{pmatrix} = \begin{pmatrix} 120 & 0 \\ 0 & 36 \end{pmatrix}$$

**Adim 4:** Kuadratik modeli yaz.

$$m(p) = f(2,1) + \nabla f(2,1)^T p + \frac{1}{2} p^T \nabla^2 f(2,1) \, p$$

p = (p_1, p_2)^T olarak yazarsak ve p_1 = x - 2, p_2 = y - 1 donusumunu yaparsak:

$$m(x,y) = 60(2-x)^2 + 18(1-y)^2 + 152(2-x) + 28(1-y) + 141$$

---

## Ornek 2: Newton Adimi ve Trust Region Karsilastirmasi

**Problem:** Ornek 1'deki fonksiyon icin (2,1) noktasinda Newton adimini hesaplayiniz. Newton adimi Delta = 1 yaricapli guven bolgesi icinde midir?

**Cozum:**

**Newton adimi:**

$$p^N = -(\nabla^2 f)^{-1} \nabla f = -\begin{pmatrix} 120 & 0 \\ 0 & 36 \end{pmatrix}^{-1} \begin{pmatrix} 152 \\ 28 \end{pmatrix}$$

Matris diyagonal oldugu icin tersi kolayca alinir:

$$p^N = -\begin{pmatrix} 1/120 & 0 \\ 0 & 1/36 \end{pmatrix} \begin{pmatrix} 152 \\ 28 \end{pmatrix} = \begin{pmatrix} -152/120 \\ -28/36 \end{pmatrix} = \begin{pmatrix} -1.267 \\ -0.778 \end{pmatrix}$$

**Newton adiminin uzunlugu:**

$$\|p^N\| = \sqrt{(-1.267)^2 + (-0.778)^2} = \sqrt{1.604 + 0.605} = \sqrt{2.209} \approx 1.486$$

**Sonuc:** ||p^N|| = 1.486 > 1 = Delta. Newton adimi guven bolgesi **disinda**! Dogrudan kullanilamaz; trust region alt problemini cozmemiz gerekir.

---

## Ornek 3: Optimallik Kosullarini Kullanarak Trust Region Cozumu

**Problem:** Ornek 1'deki fonksiyonda Delta = 1 icin trust region alt probleminin tam cozumunu bulunuz.

**Cozum:**

Newton adimi disarida oldugu icin kisit aktiftir (||p*|| = Delta = 1). Optimallik kosullarindan:

**(B + lambda I) p* = -g** ve **||p*|| = 1**

$$\begin{pmatrix} 120 + \lambda & 0 \\ 0 & 36 + \lambda \end{pmatrix} p = \begin{pmatrix} -152 \\ -28 \end{pmatrix}$$

Matris diyagonal oldugu icin:

$$p = \begin{pmatrix} \frac{-152}{120 + \lambda} \\ \frac{-28}{36 + \lambda} \end{pmatrix}$$

||p|| = 1 kosulu:

$$\left(\frac{152}{120 + \lambda}\right)^2 + \left(\frac{28}{36 + \lambda}\right)^2 = 1$$

Bu denklemi lambda icin sayisal olarak cozeriz. Ornegin Newton yontemi veya bisection kullanarak:

$$\lambda \approx 42.655$$

Cozum:

$$p^* = \begin{pmatrix} \frac{-152}{120 + 42.655} \\ \frac{-28}{36 + 42.655} \end{pmatrix} = \begin{pmatrix} \frac{-152}{162.655} \\ \frac{-28}{78.655} \end{pmatrix} \approx \begin{pmatrix} -0.9345 \\ -0.3560 \end{pmatrix}$$

**Dogrulama:** ||p*|| = sqrt(0.9345^2 + 0.3560^2) = sqrt(0.8733 + 0.1267) = sqrt(1.0000) = 1. Dogru!

---

## Ornek 4: Cauchy Noktasi Hesabi

**Problem:** Ornek 1'deki fonksiyonda (2,1) noktasinda Delta = 1 icin Cauchy noktasini hesaplayiniz.

**Cozum:**

g = (152, 28)^T, B = [[120, 0], [0, 36]]

**Adim 1:** g^T B g hesapla.

$$g^T B g = (152, 28) \begin{pmatrix} 120 & 0 \\ 0 & 36 \end{pmatrix} \begin{pmatrix} 152 \\ 28 \end{pmatrix} = (152, 28) \begin{pmatrix} 18240 \\ 1008 \end{pmatrix}$$

$$= 152 \times 18240 + 28 \times 1008 = 2{,}772{,}480 + 28{,}224 = 2{,}800{,}704$$

g^T B g > 0 oldugu icin pozitif egrilik durumundayiz.

**Adim 2:** ||g||^2 ve ||g|| hesapla.

$$\|g\|^2 = 152^2 + 28^2 = 23{,}104 + 784 = 23{,}888$$

$$\|g\| = \sqrt{23{,}888} \approx 154.56$$

**Adim 3:** p_k^S hesapla (sinirdaki steepest descent noktasi).

$$p_k^S = -\frac{\Delta}{\|g\|} g = -\frac{1}{154.56} \begin{pmatrix} 152 \\ 28 \end{pmatrix} = \begin{pmatrix} -0.9834 \\ -0.1812 \end{pmatrix}$$

**Adim 4:** tau_k hesapla.

$$\tau_k = \min\left(\frac{\|g\|^3}{\Delta \cdot g^T B g}, \; 1\right) = \min\left(\frac{(154.56)^3}{1 \times 2{,}800{,}704}, \; 1\right)$$

$$= \min\left(\frac{3{,}693{,}627}{2{,}800{,}704}, \; 1\right) = \min(1.319, \; 1) = 1$$

tau_k = 1 oldugu icin Cauchy noktasi sinirda:

$$p^C = 1 \times p_k^S = \begin{pmatrix} -0.9834 \\ -0.1812 \end{pmatrix}$$

**Karsilastirma:** Trust region tam cozumu p* = (-0.9345, -0.3560) idi. Cauchy noktasi (-0.9834, -0.1812) — daha fazla x yonunde, daha az y yonunde. Cauchy sadece gradyan yonunde gittigi icin Newton bilgisini kullanmiyor.

---

## Ornek 5: Dogleg Yontemi

**Problem:** f(x) = (1/2) x^T Q x - c^T x fonksiyonu icin Q = [[1/4, 0], [0, 1]], c = (1, 1)^T, x_0 = (0, 0)^T. Delta = 1, 2, 3 icin dogleg cozumlerini bulunuz.

**Cozum:**

(0,0) noktasinda: g = nabla f(0,0) = Q x_0 - c = -c = (-1, -1)^T, B = Q = [[1/4, 0], [0, 1]]

**Cauchy noktasi (p^U):**

$$p^U = -\frac{g^T g}{g^T B g} g = -\frac{(-1)^2 + (-1)^2}{(-1, -1) \begin{pmatrix} 1/4 & 0 \\ 0 & 1 \end{pmatrix} \begin{pmatrix} -1 \\ -1 \end{pmatrix}} \begin{pmatrix} -1 \\ -1 \end{pmatrix}$$

$$g^T B g = (-1)(1/4)(-1) + (-1)(1)(-1) = 1/4 + 1 = 5/4$$

$$p^U = -\frac{2}{5/4} \begin{pmatrix} -1 \\ -1 \end{pmatrix} = \frac{8}{5} \begin{pmatrix} 1 \\ 1 \end{pmatrix} = \begin{pmatrix} 1.6 \\ 1.6 \end{pmatrix}$$

**Newton adimi (p^B):**

$$p^B = -B^{-1} g = -\begin{pmatrix} 4 & 0 \\ 0 & 1 \end{pmatrix} \begin{pmatrix} -1 \\ -1 \end{pmatrix} = \begin{pmatrix} 4 \\ 1 \end{pmatrix}$$

||p^U|| = sqrt(1.6^2 + 1.6^2) = sqrt(5.12) ≈ 2.263

||p^B|| = sqrt(16 + 1) = sqrt(17) ≈ 4.123

**p^B - p^U = (4 - 1.6, 1 - 1.6) = (2.4, -0.6)**

### Delta = 1:

||p^U|| = 2.263 > 1 = Delta. Cauchy noktasi bile disarida! Gradyan yonunde sinira kadar git:

$$p = \frac{\Delta}{\|g\|} (-g) = \frac{1}{\sqrt{2}} \begin{pmatrix} 1 \\ 1 \end{pmatrix} \approx \begin{pmatrix} 0.707 \\ 0.707 \end{pmatrix}$$

Ama Cauchy noktasinin tau_k degerine bakmamiz lazim. tau_k = min(||g||^3/(Delta g^T B g), 1) = min(2sqrt(2)/(1 * 5/4), 1) = min(2.263, 1) = 1.

Cauchy yonunde guven bolgesi sinirinda: p^C = (1/sqrt(2)) * (1, 1) = (0.707, 0.707). Dogleg icin ilk parcada (orijinden p^U'ya) sinirla kesisimi buluruz:

||tau * p^U|| = 1 => tau * 2.263 = 1 => tau = 0.442

p = 0.442 * (1.6, 1.6) = (0.707, 0.707)

**Dogleg cozumu Delta=1 icin:** p ≈ (0.707, 0.707), f(p) ≈ -1.1017

### Delta = 2:

||p^U|| = 2.263 > 2 = Delta ama yakin. Yine ilk parcada sinirla kesisir:

tau = 2 / 2.263 = 0.884

p = 0.884 * (1.6, 1.6) = (1.414, 1.414)

Ama bu sefer ikinci parcaya da bakmaliyiz. ||p^U|| > Delta oldugu icin hala ilk parcadayiz.

tau * ||p^U|| = Delta => tau = 2/2.263 = 0.884

p = (0.884 * 1.6, 0.884 * 1.6) = (1.414, 1.414)

**Dogleg cozumu Delta=2 icin:** p ≈ (1.414, 1.414)

Ikinci parcaya gectiginde: ||p^U + (tau-1)(p^B - p^U)||^2 = Delta^2 denklemini coz:

||(1.6 + (tau-1)*2.4)^2 + (1.6 + (tau-1)*(-0.6))^2|| = 4

tau ≈ 1.064, p ≈ (1.754, 1.562), f(p) ≈ -1.7116

### Delta = 3:

Ikinci parcada: ||(1.6 + (tau-1)*2.4)^2 + (1.6 + (tau-1)*(-0.6))^2|| = 9

tau ≈ 1.551, p ≈ (2.922, 1.269)

**Dogleg cozumu Delta=3 icin:** p ≈ (2.922, 1.269), f(p) ≈ -2.3193

**Sonuc tablosu (dersten):**

| Delta | lambda | min f(p) (tam cozum) | tau | f(p(tau)) (dogleg) |
|-------|--------|---------------------|-----|-------------------|
| 1 | 0.9212 | -1.1478 | 0.625 | -1.1017 |
| 2 | 0.2912 | -1.8935 | 1.064 | -1.7116 |
| 3 | 0.0998 | -2.3331 | 1.551 | -2.3193 |

Dogleg cozumleri tam cozumlere yakin ama tam olarak ayni degil. Delta buyudukce fark azaliyor.

---

## Ornek 6: Konveks Olmayan Fonksiyonda Trust Region

**Problem:** f(x) = x_1^2 - x_2^2 fonksiyonu icin x_0 = (0, 0) noktasinda trust region adimini hesaplayiniz. Delta_0 = 1.

**Cozum:**

$$\nabla f(0,0) = \begin{pmatrix} 0 \\ 0 \end{pmatrix}, \quad \nabla^2 f = \begin{pmatrix} 2 & 0 \\ 0 & -2 \end{pmatrix}$$

x_0 = (0,0) bir eyer noktasi (saddle point) — gradyan sifir ama minimum degil!

Gradyan sifir oldugu icin model: m(p) = (1/2) p^T B p = p_1^2 - p_2^2

Bu, kisitsiz durumda sinira gitmez — ama trust region ile:

min m(p) = min(p_1^2 - p_2^2) kosul ||p|| <= 1

p_2 yonunde m azalir (cunku -p_2^2). Optimal cozum: p* = (0, +-1), yani m(p*) = -1.

**Newton metodu** gradyan sifir oldugu icin hic bir sey yapmaz (x_1 = x_0). Ama trust region eyer noktasindan kacabilir! Bu, trust region'un onemli bir avantajidir.

---

## Ornek 7: Degerlendirme Orani (rho_k) Hesabi

**Problem:** f(x) = x^2 + 1 fonksiyonu, x_0 = 2, Delta = 1. Trust region adimini at ve rho_0'i hesapla.

**Cozum:**

f(2) = 5, f'(2) = 4, f''(2) = 2

Model: m(p) = 5 + 4p + (1/2)(2)p^2 = 5 + 4p + p^2

Kisitsiz minimum: m'(p) = 4 + 2p = 0 => p = -2. Ama ||p|| = 2 > Delta = 1.

Kisit aktif: p* = -1 (guven bolgesi sinirinda, inis yonunde).

**Gercek azalma:**
$$f(2) - f(2 + (-1)) = f(2) - f(1) = 5 - 2 = 3$$

**Tahmin edilen azalma:**
$$m(0) - m(-1) = 5 - (5 + 4(-1) + (-1)^2) = 5 - 2 = 3$$

$$\rho_0 = \frac{3}{3} = 1$$

rho_0 = 1: Model mukkemmel! (Bu ornekte fonksiyon zaten kuadratik oldugu icin model tam.)

rho_0 > 3/4 ve ||p|| = Delta = 1 oldugu icin: Delta_1 = min(2 * 1, Delta_hat) = 2. Bolge buyutulur.

---

## Ornek 8: Adim Reddedilmesi

**Problem:** Bir trust region iterasyonunda f(x_k) = 10, f(x_k + p_k) = 11, m_k(0) = 10, m_k(p_k) = 7 ise rho_k'yi hesaplayip adimin kabul edilip edilmeyecegini belirleyiniz (eta = 0.1).

**Cozum:**

$$\rho_k = \frac{f(x_k) - f(x_k + p_k)}{m_k(0) - m_k(p_k)} = \frac{10 - 11}{10 - 7} = \frac{-1}{3} \approx -0.333$$

**Yorum:**
- Pay = -1: Fonksiyon **artti** (kotu!)
- Payda = 3: Model 3 birimlik azalma tahmin etmisti
- rho_k = -1/3 < 0: Model tamamen yanilmis

**Karar:**
- rho_k = -0.333 < 1/4: Adim **reddedilir** (x_{k+1} = x_k)
- Delta_{k+1} = (1/4) Delta_k: Bolge dort kat kucultulur
- Bir sonraki iterasyonda daha kucuk bir adim denenecek

---

## Ornek 9: Newton Yontemi + Trust Region (Homework Sorusu 1)

**Problem:** f(x_1, x_2) = (1/2)(x_1 - 2x_2)^2 + x_1^4 fonksiyonunda x = (2, 1)^T noktasinda:
(a) Newton arama yonunu ve bir sonraki iterasyonu bulunuz.
(b) Backtracking ile alpha = 1, mu = 0.2 icin Armijo kosulunu kontrol ediniz.

**Cozum (a):**

**Gradyan:**

$$\nabla f = \begin{pmatrix} (x_1 - 2x_2) + 4x_1^3 \\ -2(x_1 - 2x_2) \end{pmatrix}$$

$$\nabla f(2,1) = \begin{pmatrix} (2-2) + 4(8) \\ -2(2-2) \end{pmatrix} = \begin{pmatrix} 32 \\ 0 \end{pmatrix}$$

**Hessian:**

$$\nabla^2 f = \begin{pmatrix} 1 + 12x_1^2 & -2 \\ -2 & 4 \end{pmatrix}$$

$$\nabla^2 f(2,1) = \begin{pmatrix} 49 & -2 \\ -2 & 4 \end{pmatrix}$$

**Newton yonu:**

$$p^N = -(\nabla^2 f)^{-1} \nabla f$$

$$(\nabla^2 f)^{-1} = \frac{1}{49 \cdot 4 - (-2)(-2)} \begin{pmatrix} 4 & 2 \\ 2 & 49 \end{pmatrix} = \frac{1}{192} \begin{pmatrix} 4 & 2 \\ 2 & 49 \end{pmatrix}$$

$$p^N = -\frac{1}{192} \begin{pmatrix} 4 & 2 \\ 2 & 49 \end{pmatrix} \begin{pmatrix} 32 \\ 0 \end{pmatrix} = -\frac{1}{192} \begin{pmatrix} 128 \\ 64 \end{pmatrix} = \begin{pmatrix} -2/3 \\ -1/3 \end{pmatrix}$$

**Bir sonraki iterasyon (alpha = 1 ile):**

$$x_1 = x_0 + p^N = \begin{pmatrix} 2 \\ 1 \end{pmatrix} + \begin{pmatrix} -2/3 \\ -1/3 \end{pmatrix} = \begin{pmatrix} 4/3 \\ 2/3 \end{pmatrix}$$

**Cozum (b): Armijo Kosulu Kontrolu**

Armijo kosulu: f(x_k + alpha p_k) <= f(x_k) + mu * alpha * nabla f_k^T p_k

- f(2, 1) = (1/2)(2-2)^2 + 2^4 = 0 + 16 = 16
- f(4/3, 2/3) = (1/2)(4/3 - 4/3)^2 + (4/3)^4 = 0 + 256/81 ≈ 3.16
- nabla f(2,1)^T p^N = (32)(−2/3) + (0)(−1/3) = −64/3 ≈ −21.33

Armijo (mu = 0.2, alpha = 1):
- Sol taraf: f(4/3, 2/3) = 3.16
- Sag taraf: 16 + 0.2 * 1 * (−64/3) = 16 − 4.267 = 11.73
- 3.16 <= 11.73? **Evet!** Armijo kosulu saglanir.

---

## Ornek 10: Trust Region Algoritmasi ile Adim Adim Iterasyon (Homework Sorusu 2)

**Problem:** Asagidaki trust region algoritmasini f(x_1, x_2) = (1/2)(x_1 - 2x_2)^2 + x_1^4 icin x_0 = (2,1)^T, mu_0 = 1, tau_1 = 1/4, tau_2 = 3/4 ile uygulayiniz.

Algoritmadaki p_k = -(nabla^2 f(x_k) + mu I)^(-1) nabla f(x_k)

**Cozum — Iterasyon 0:**

g_0 = nabla f(2,1) = (32, 0)^T, B_0 = nabla^2 f(2,1) = [[49, -2], [-2, 4]]

mu_0 = 1 ile:

$$B_0 + \mu_0 I = \begin{pmatrix} 50 & -2 \\ -2 & 5 \end{pmatrix}$$

$$(B_0 + \mu_0 I)^{-1} = \frac{1}{250 - 4} \begin{pmatrix} 5 & 2 \\ 2 & 50 \end{pmatrix} = \frac{1}{246} \begin{pmatrix} 5 & 2 \\ 2 & 50 \end{pmatrix}$$

$$p_0 = -\frac{1}{246} \begin{pmatrix} 5 & 2 \\ 2 & 50 \end{pmatrix} \begin{pmatrix} 32 \\ 0 \end{pmatrix} = -\frac{1}{246} \begin{pmatrix} 160 \\ 64 \end{pmatrix} = \begin{pmatrix} -0.6504 \\ -0.2602 \end{pmatrix}$$

**Trust region yaricapi:** Delta_0 = ||p_0|| = sqrt(0.6504^2 + 0.2602^2) = sqrt(0.4230 + 0.0677) = sqrt(0.4907) ≈ 0.7005

**rho_0 hesabi:**

- f(x_0) = f(2, 1) = 16
- f(x_0 + p_0) = f(2 - 0.6504, 1 - 0.2602) = f(1.3496, 0.7398)
  - = (1/2)(1.3496 - 2*0.7398)^2 + (1.3496)^4
  - = (1/2)(1.3496 - 1.4796)^2 + 3.316
  - = (1/2)(−0.1300)^2 + 3.316
  - = 0.00845 + 3.316 = 3.325

- psi_0(p_0) = f(x_0) + nabla f(x_0)^T p_0 + (1/2) p_0^T nabla^2 f(x_0) p_0
  - = 16 + (32)(−0.6504) + (1/2) p_0^T B_0 p_0
  - Lineer kisim: 32 * (−0.6504) = −20.813
  - Kuadratik kisim: (1/2)[(−0.6504, −0.2602) [[49, −2], [−2, 4]] (−0.6504, −0.2602)^T]
    - B_0 p_0 = (49*(-0.6504) + (-2)*(-0.2602), (-2)*(-0.6504) + 4*(-0.2602)) = (-31.37, 0.260)
    - p_0^T (B_0 p_0) = (-0.6504)(-31.37) + (-0.2602)(0.260) = 20.40 - 0.068 = 20.33
    - (1/2) * 20.33 = 10.17
  - psi_0 = 16 - 20.813 + 10.17 = 5.36

$$\rho_0 = \frac{f(x_0) - f(x_0 + p_0)}{f(x_0) - \psi_0(p_0)} = \frac{16 - 3.325}{16 - 5.36} = \frac{12.675}{10.64} \approx 1.19$$

rho_0 ≈ 1.19 > tau_2 = 3/4: Adim **cok iyi**! x_1 = x_0 + p_0, mu_1 = (1/2)mu_0 = 0.5.

---

## Ornek 11: Eksponansiyel Fonksiyonda Trust Region (Homework Sorusu 3)

**Problem:** f(x_1, x_2) = e^(x_1 + x_2 - 2) + (x_1 - x_2)^2 fonksiyonunda x_0 = (1, 1)^T.
(a) Newton adimini (alpha = 1) uygulayip x_1'i bulunuz.
(b) mu = 1 ile trust region arama yonunu hesaplayip, adimin kabul edilip edilmeyecegini belirleyiniz.

**Cozum (a):**

$$f(1,1) = e^{1+1-2} + (1-1)^2 = e^0 + 0 = 1$$

**Gradyan:**

$$\nabla f = \begin{pmatrix} e^{x_1+x_2-2} + 2(x_1-x_2) \\ e^{x_1+x_2-2} - 2(x_1-x_2) \end{pmatrix}$$

$$\nabla f(1,1) = \begin{pmatrix} 1 + 0 \\ 1 - 0 \end{pmatrix} = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$$

**Hessian:**

$$\nabla^2 f = \begin{pmatrix} e^{x_1+x_2-2} + 2 & e^{x_1+x_2-2} - 2 \\ e^{x_1+x_2-2} - 2 & e^{x_1+x_2-2} + 2 \end{pmatrix}$$

$$\nabla^2 f(1,1) = \begin{pmatrix} 3 & -1 \\ -1 & 3 \end{pmatrix}$$

**Newton adimi:**

$$p^N = -\begin{pmatrix} 3 & -1 \\ -1 & 3 \end{pmatrix}^{-1} \begin{pmatrix} 1 \\ 1 \end{pmatrix}$$

$$\det = 9 - 1 = 8$$

$$(\nabla^2 f)^{-1} = \frac{1}{8} \begin{pmatrix} 3 & 1 \\ 1 & 3 \end{pmatrix}$$

$$p^N = -\frac{1}{8} \begin{pmatrix} 3 & 1 \\ 1 & 3 \end{pmatrix} \begin{pmatrix} 1 \\ 1 \end{pmatrix} = -\frac{1}{8} \begin{pmatrix} 4 \\ 4 \end{pmatrix} = \begin{pmatrix} -0.5 \\ -0.5 \end{pmatrix}$$

$$x_1 = x_0 + p^N = \begin{pmatrix} 1 \\ 1 \end{pmatrix} + \begin{pmatrix} -0.5 \\ -0.5 \end{pmatrix} = \begin{pmatrix} 0.5 \\ 0.5 \end{pmatrix}$$

**Cozum (b):**

mu = 1 ile trust region yonu:

$$p_{TR} = -(B + \mu I)^{-1} g = -\begin{pmatrix} 4 & -1 \\ -1 & 4 \end{pmatrix}^{-1} \begin{pmatrix} 1 \\ 1 \end{pmatrix}$$

$$\det = 16 - 1 = 15$$

$$p_{TR} = -\frac{1}{15} \begin{pmatrix} 4 & 1 \\ 1 & 4 \end{pmatrix} \begin{pmatrix} 1 \\ 1 \end{pmatrix} = -\frac{1}{15} \begin{pmatrix} 5 \\ 5 \end{pmatrix} = \begin{pmatrix} -1/3 \\ -1/3 \end{pmatrix}$$

Delta = ||p_{TR}|| = sqrt(1/9 + 1/9) = sqrt(2/9) ≈ 0.471

**rho hesabi:**

- f(1,1) = 1
- f(1 - 1/3, 1 - 1/3) = f(2/3, 2/3) = e^(2/3 + 2/3 - 2) + (2/3 - 2/3)^2 = e^(-2/3) + 0 ≈ 0.5134

Model degeri:
- psi(p) = f(x_0) + g^T p + (1/2) p^T B p
- g^T p = (1)(−1/3) + (1)(−1/3) = −2/3
- p^T B p = (−1/3, −1/3) [[3, −1], [−1, 3]] (−1/3, −1/3)^T
  - B p = (3(-1/3) + (-1)(-1/3), (-1)(-1/3) + 3(-1/3)) = (-2/3, -2/3)
  - p^T Bp = (-1/3)(-2/3) + (-1/3)(-2/3) = 2/9 + 2/9 = 4/9
- psi = 1 - 2/3 + (1/2)(4/9) = 1 - 0.667 + 0.222 = 0.556

$$\rho = \frac{1 - 0.5134}{1 - 0.556} = \frac{0.4866}{0.444} \approx 1.096$$

rho ≈ 1.096 > tau_2 = 3/4: Adim **kabul edilir** ve mu kucultulur (mu_new = 0.5).

---

## Ornek 12: Trust Region — Konveks Olmayan Kuadratik

**Problem:** f(x) = x_1^2 - x_2^2 (eyer fonksiyonu). x_k = (0, 0), Delta_k = 1. Trust region alt probleminin cozumunu bulunuz.

**Cozum:**

g = nabla f(0,0) = (0, 0)^T (gradyan sifir — eyer noktasi!)

B = nabla^2 f = [[2, 0], [0, -2]]

Gradyan sifir oldugu icin model: m(p) = (1/2) p^T B p = p_1^2 - p_2^2

B pozitif tanili degil (bir ozdegeri -2). Newton yontemi p = -B^(-1)g = 0 verir — hicbir sey yapmaz!

Trust region ile: min(p_1^2 - p_2^2) kosul p_1^2 + p_2^2 <= 1

p_2^2'yi maksimize etmek istiyoruz (cunku onunde eksi isareti var). p_1 = 0, p_2 = +-1 optimal.

**Optimallik kosullarini dogrulayalim:**

(B + lambda I) p* = -g => [[2+lambda, 0], [0, -2+lambda]] (0, 1)^T = (0, 0)^T

=> (-2 + lambda) * 1 = 0 => lambda = 2

B + lambda I = [[4, 0], [0, 0]] — pozitif yari-tanili. Dogrulandi!

lambda(Delta - ||p*||) = 2(1 - 1) = 0. Tamamlayici gevsetme saglandi.

**Sonuc:** p* = (0, +-1). Trust region eyer noktasindan kacar, Newton kalakalir.

---

## Ornek 13: Farkli Delta Degerleri Icin Cozum Degisimi

**Problem:** f(x) = (1/2)(x_1^2 + 10 x_2^2) fonksiyonunda x_0 = (10, 1). Delta = 1, 5, 20 icin trust region cozumlerini bulunuz.

**Cozum:**

g = (10, 10)^T, B = [[1, 0], [0, 10]]

Newton adimi: p^N = -B^(-1)g = -(10, 1)^T, ||p^N|| = sqrt(100 + 1) ≈ 10.05

**Delta = 1:**

||p^N|| = 10.05 >> 1. Kisit aktif.

(B + lambda I)p = -g => p = (-10/(1+lambda), -10/(10+lambda))^T

||p|| = 1: (10/(1+lambda))^2 + (10/(10+lambda))^2 = 1

Sayisal cozum: lambda ≈ 9.04

p* ≈ (-0.995, -0.525) => inis yonu steepest descent'e yakin

**Delta = 5:**

(10/(1+lambda))^2 + (10/(10+lambda))^2 = 25

lambda ≈ 1.24

p* ≈ (-4.464, -0.890) => steepest descent ile Newton arasi

**Delta = 20:**

||p^N|| = 10.05 < 20. Kisit pasif! lambda = 0.

p* = p^N = (-10, -1) (tam Newton adimi)

**Gozlem:** Delta kuculdukce cozum steepest descent'e yaklasir, buyudukce Newton adimina yaklasir.

---

## Genel Cozum Stratejisi Ozeti

Trust region problemlerini cozerken su adimlari takip et:

1. **Gradyan ve Hessian'i hesapla** (g_k ve B_k)
2. **Newton adimini hesapla**: p^N = -B^(-1) g
3. **||p^N|| ile Delta'yi karsilastir**:
   - ||p^N|| <= Delta: Cozum p^N (kisit pasif, lambda = 0)
   - ||p^N|| > Delta: Optimallik kosullarindan lambda'yi bul
4. **rho_k hesapla** ve adimi kabul/reddet
5. **Delta'yi guncelle**
