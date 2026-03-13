# 5. Cozulmus Ornekler

---

## Ornek 1: Gradient Hesaplama

**Soru:** f(x₁, x₂) = 2x₁² + x₁x₂ + x₂² fonksiyonunun gradientini bul ve (1, 2) noktasinda hesapla.

**Cozum:**

Kismi turevleri alalim:

$$\frac{\partial f}{\partial x_1} = 4x_1 + x_2$$

$$\frac{\partial f}{\partial x_2} = x_1 + 2x_2$$

Gradient:

$$\nabla f(x) = \begin{pmatrix} 4x_1 + x_2 \\ x_1 + 2x_2 \end{pmatrix}$$

(1, 2) noktasinda:

$$\nabla f(1, 2) = \begin{pmatrix} 4(1) + 2 \\ 1 + 2(2) \end{pmatrix} = \begin{pmatrix} 6 \\ 5 \end{pmatrix}$$

**Yorum:** (1, 2) noktasinda fonksiyon en hizli (6, 5) yonunde artar. Minimum bulmak icin **(-6, -5)** yonunde yurumeliyiz.

---

## Ornek 2: Hessian Hesaplama ve Pozitif Definitlik

**Soru:** f(x₁, x₂) = 3x₁² - 2x₁x₂ + x₂² fonksiyonunun Hessianini bul. Pozitif definit mi?

**Cozum:**

Gradient:

$$\nabla f = \begin{pmatrix} 6x_1 - 2x_2 \\ -2x_1 + 2x_2 \end{pmatrix}$$

Hessian (gradientin turevini al):

$$\nabla^2 f = \begin{pmatrix} 6 & -2 \\ -2 & 2 \end{pmatrix}$$

Pozitif definitlik kontrolu - ozdegerlere bakalim:

det(H - λI) = 0

$$(6-\lambda)(2-\lambda) - (-2)(-2) = 0$$
$$\lambda^2 - 8\lambda + 12 - 4 = 0$$
$$\lambda^2 - 8\lambda + 8 = 0$$
$$\lambda = \frac{8 \pm \sqrt{64-32}}{2} = \frac{8 \pm \sqrt{32}}{2}$$
$$\lambda_1 \approx 6.83, \quad \lambda_2 \approx 1.17$$

**Iki ozdeger de pozitif → Hessian pozitif definit → f konveks bir fonksiyon!**

---

## Ornek 3: Taylor Acilimi ile Yaklasim

**Soru:** f(x) = x₁² + x₂² fonksiyonunu x = (1, 1) noktasi etrafinda 2. derece Taylor ile yaklas.

**Cozum:**

$$f(x+p) \approx f(x) + \nabla f(x)^T p + \frac{1}{2} p^T \nabla^2 f(x) p$$

f(1, 1) = 1 + 1 = 2

$$\nabla f(1, 1) = \begin{pmatrix} 2 \\ 2 \end{pmatrix}$$

$$\nabla^2 f = \begin{pmatrix} 2 & 0 \\ 0 & 2 \end{pmatrix}$$

p = (0.1, 0.1) adimi atarsak:

$$f(1.1, 1.1) \approx 2 + (2, 2) \begin{pmatrix} 0.1 \\ 0.1 \end{pmatrix} + \frac{1}{2} (0.1, 0.1) \begin{pmatrix} 2 & 0 \\ 0 & 2 \end{pmatrix} \begin{pmatrix} 0.1 \\ 0.1 \end{pmatrix}$$

$$= 2 + 0.4 + \frac{1}{2}(0.04) = 2 + 0.4 + 0.02 = 2.42$$

Gercek deger: f(1.1, 1.1) = 1.21 + 1.21 = 2.42 ✓ (Bu fonksiyon kuadratik oldugu icin Taylor tam sonuc verir)

---

## Ornek 4: Konvekslik Kontrolu

**Soru:** f(x) = eˣ fonksiyonunun konveks oldugunu goster.

**Cozum:** Tanimdan: f(αx + (1-α)y) ≤ αf(x) + (1-α)f(y) mi?

$$e^{\alpha x + (1-\alpha)y} \leq \alpha e^x + (1-\alpha) e^y$$

Ikinci turev testi: f''(x) = eˣ > 0, ∀x ✓

f''(x) > 0 her yerde → f kesinlikle konveks.

**Kural:** Tek degiskenli fonksiyon icin f''(x) ≥ 0 ise konveks. Cok degiskenli icin Hessian pozitif semi-definit ise konveks.

---

## Ornek 5: Ozdeger Bulma

**Soru:** A = [[4, 2], [2, 1]] matrisinin ozdegerlerini ve ozvektorlerini bul.

**Cozum:**

det(A - λI) = 0:

$$(4-\lambda)(1-\lambda) - 4 = 0$$
$$4 - 5\lambda + \lambda^2 - 4 = 0$$
$$\lambda^2 - 5\lambda = 0$$
$$\lambda(\lambda - 5) = 0$$

**λ₁ = 0, λ₂ = 5**

λ₁ = 0 icin ozvektor: (A - 0I)x = 0

$$\begin{pmatrix} 4 & 2 \\ 2 & 1 \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \end{pmatrix} = 0$$

4x₁ + 2x₂ = 0 → x₂ = -2x₁ → **v₁ = (1, -2)^T**

λ₂ = 5 icin: (A - 5I)x = 0

$$\begin{pmatrix} -1 & 2 \\ 2 & -4 \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \end{pmatrix} = 0$$

-x₁ + 2x₂ = 0 → x₁ = 2x₂ → **v₂ = (2, 1)^T**

**Not:** λ₁ = 0 oldugu icin A tekil (singular). det(A) = 4·1 - 2·2 = 0 ✓

---

## Ornek 6: LU Ayrisimi

**Soru:** A = [[2, 1], [4, 3]] icin LU ayrisimini bul ve Ax = b'yi coz (b = [3, 7]^T).

**Cozum:**

**Adim 1: LU Ayrisimi (pivotlama gerekmiyorsa P = I)**

Gauss eliminasyonu yapalim:
- Satir 2'den (4/2 = 2) × Satir 1'i cikar

$$L = \begin{pmatrix} 1 & 0 \\ 2 & 1 \end{pmatrix}, \quad U = \begin{pmatrix} 2 & 1 \\ 0 & 1 \end{pmatrix}$$

Kontrol: LU = [[2,1],[4,3]] = A ✓

**Adim 2: Ly = b coz (ileri yerine koyma)**

$$\begin{pmatrix} 1 & 0 \\ 2 & 1 \end{pmatrix} \begin{pmatrix} y_1 \\ y_2 \end{pmatrix} = \begin{pmatrix} 3 \\ 7 \end{pmatrix}$$

- y₁ = 3
- 2(3) + y₂ = 7 → y₂ = 1

**Adim 3: Ux = y coz (geri yerine koyma)**

$$\begin{pmatrix} 2 & 1 \\ 0 & 1 \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \end{pmatrix} = \begin{pmatrix} 3 \\ 1 \end{pmatrix}$$

- x₂ = 1
- 2x₁ + 1 = 3 → x₁ = 1

**Cozum: x = (1, 1)^T**

---

## Ornek 7: Jacobian Hesaplama

**Soru:** r(x₁, x₂) = (x₁² + x₂², x₁x₂, eˣ¹) fonksiyonunun Jacobianini bul.

**Cozum:**

r: R² → R³ (2 giris, 3 cikis), yani Jacobian 3×2 matris.

$$J(x) = \begin{pmatrix} \frac{\partial f_1}{\partial x_1} & \frac{\partial f_1}{\partial x_2} \\ \frac{\partial f_2}{\partial x_1} & \frac{\partial f_2}{\partial x_2} \\ \frac{\partial f_3}{\partial x_1} & \frac{\partial f_3}{\partial x_2} \end{pmatrix} = \begin{pmatrix} 2x_1 & 2x_2 \\ x_2 & x_1 \\ e^{x_1} & 0 \end{pmatrix}$$

(1, 1) noktasinda:

$$J(1, 1) = \begin{pmatrix} 2 & 2 \\ 1 & 1 \\ e & 0 \end{pmatrix}$$

---

## Ornek 8: Kosul Sayisi

**Soru:** A = [[1, 0], [0, 0.001]] matrisinin kosul sayisini bul (2-norm ile).

**Cozum:**

A kosegen matris, ozdegerleri: λ₁ = 1, λ₂ = 0.001

2-norm icin:
- ||A||₂ = max ozdeger = 1
- ||A⁻¹||₂ = max(1/λᵢ) = 1/0.001 = 1000

$$\kappa(A) = 1 \times 1000 = 1000$$

**Yorum:** κ(A) = 1000 oldukca buyuk → bu matris **ill-conditioned**. Ax = b cozerken kucuk hatalar 1000 kat buyuyebilir.

---

## Ornek 9: Konveks Kombinasyon

**Soru:** A = (1, 3) ve B = (5, 1) noktalarinin konveks kombinasyonlarini yaz. (0.5, 0.5) ve (0.3, 0.7) icin hesapla.

**Cozum:**

Konveks kombinasyon: P = λA + (1-λ)B, λ ∈ [0,1]

λ = 0.5:
- P = 0.5(1,3) + 0.5(5,1) = (0.5+2.5, 1.5+0.5) = **(3, 2)** (orta nokta)

λ = 0.3:
- P = 0.3(1,3) + 0.7(5,1) = (0.3+3.5, 0.9+0.7) = **(3.8, 1.6)** (B'ye daha yakin)

**Geometrik anlam:** λ ∈ [0,1] degistikce, A ile B arasindaki dogru parcasi uzerinde tum noktalari elde ederiz.

---

## Ornek 10: Minimumu Bul (Gradient = 0)

**Soru:** f(x₁, x₂) = x₁² + x₂² - 2x₁ - 4x₂ + 5 fonksiyonunun minimumunu bul.

**Cozum:**

**Adim 1: Gradient = 0 yap**

$$\nabla f = \begin{pmatrix} 2x_1 - 2 \\ 2x_2 - 4 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}$$

- 2x₁ - 2 = 0 → x₁ = 1
- 2x₂ - 4 = 0 → x₂ = 2

Kritik nokta: **(1, 2)**

**Adim 2: Hessian ile kontrol**

$$\nabla^2 f = \begin{pmatrix} 2 & 0 \\ 0 & 2 \end{pmatrix}$$

Ozdegerleri: λ₁ = 2, λ₂ = 2 (ikisi de pozitif)

→ Hessian **pozitif definit** → bu nokta kesinlikle **minimum**!

**f(1, 2) = 1 + 4 - 2 - 8 + 5 = 0**

Minimum deger **0**, (1, 2) noktasinda.

---

## Ornek 11: Cholesky Ayrisimi

**Soru:** A = [[4, 2], [2, 5]] matrisinin Cholesky ayrisimini bul ve Ax = b'yi coz (b = [8, 11]^T).

**Cozum:**

**Adim 1: A'nin simetrik pozitif definit (SPD) oldugunu goster**

A simetrik mi? A^T = A ✓ (a₁₂ = a₂₁ = 2)

Ozdegerleri bulalim:

$$\det(A - \lambda I) = (4-\lambda)(5-\lambda) - 4 = 0$$
$$\lambda^2 - 9\lambda + 20 - 4 = 0$$
$$\lambda^2 - 9\lambda + 16 = 0$$
$$\lambda = \frac{9 \pm \sqrt{81 - 64}}{2} = \frac{9 \pm \sqrt{17}}{2}$$
$$\lambda_1 \approx 6.56, \quad \lambda_2 \approx 2.44$$

Iki ozdeger de pozitif → A **simetrik pozitif definit** → Cholesky ayrisimi uygulanabilir ✓

**Adim 2: L matrisini bul (A = LL^T)**

$$A = \begin{pmatrix} 4 & 2 \\ 2 & 5 \end{pmatrix} = \begin{pmatrix} l_{11} & 0 \\ l_{21} & l_{22} \end{pmatrix} \begin{pmatrix} l_{11} & l_{21} \\ 0 & l_{22} \end{pmatrix}$$

Carpimi acalim ve elemanlari esitleyelim:

- (1,1): $l_{11}^2 = 4$ → $l_{11} = \sqrt{4} = 2$
- (2,1): $l_{21} \cdot l_{11} = 2$ → $l_{21} = 2 / 2 = 1$
- (2,2): $l_{21}^2 + l_{22}^2 = 5$ → $1 + l_{22}^2 = 5$ → $l_{22} = \sqrt{4} = 2$

$$L = \begin{pmatrix} 2 & 0 \\ 1 & 2 \end{pmatrix}$$

Kontrol:

$$LL^T = \begin{pmatrix} 2 & 0 \\ 1 & 2 \end{pmatrix} \begin{pmatrix} 2 & 1 \\ 0 & 2 \end{pmatrix} = \begin{pmatrix} 4 & 2 \\ 2 & 5 \end{pmatrix} = A \quad ✓$$

**Adim 3: Ly = b coz (ileri yerine koyma)**

$$\begin{pmatrix} 2 & 0 \\ 1 & 2 \end{pmatrix} \begin{pmatrix} y_1 \\ y_2 \end{pmatrix} = \begin{pmatrix} 8 \\ 11 \end{pmatrix}$$

- $2y_1 = 8$ → $y_1 = 4$
- $y_1 + 2y_2 = 11$ → $4 + 2y_2 = 11$ → $y_2 = 3.5$

$$y = \begin{pmatrix} 4 \\ 3.5 \end{pmatrix}$$

**Adim 4: L^T x = y coz (geri yerine koyma)**

$$\begin{pmatrix} 2 & 1 \\ 0 & 2 \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \end{pmatrix} = \begin{pmatrix} 4 \\ 3.5 \end{pmatrix}$$

- $2x_2 = 3.5$ → $x_2 = 1.75$
- $2x_1 + x_2 = 4$ → $2x_1 + 1.75 = 4$ → $x_1 = 1.125$

$$\boxed{x = \begin{pmatrix} 1.125 \\ 1.75 \end{pmatrix}}$$

**Dogrulama:**

$$Ax = \begin{pmatrix} 4 & 2 \\ 2 & 5 \end{pmatrix} \begin{pmatrix} 1.125 \\ 1.75 \end{pmatrix} = \begin{pmatrix} 4(1.125) + 2(1.75) \\ 2(1.125) + 5(1.75) \end{pmatrix} = \begin{pmatrix} 4.5 + 3.5 \\ 2.25 + 8.75 \end{pmatrix} = \begin{pmatrix} 8 \\ 11 \end{pmatrix} = b \quad ✓$$

**Not:** Cholesky ayrisimi, LU ayrisimina gore yaklasik 2 kat daha hizlidir ve yalnizca SPD matrisler icin uygulanabilir.

---

## Ornek 12: SVD Hesaplama (2x2)

**Soru:** A = [[3, 0], [0, -2]] matrisinin SVD'sini bul.

**Cozum:**

SVD: $A = U \Sigma V^T$ seklinde yazilir. Burada U ve V ortogonal matrisler, $\Sigma$ kosegen matristir.

**Adim 1: A^T A ve AA^T hesapla**

$$A^T A = \begin{pmatrix} 3 & 0 \\ 0 & -2 \end{pmatrix}^T \begin{pmatrix} 3 & 0 \\ 0 & -2 \end{pmatrix} = \begin{pmatrix} 3 & 0 \\ 0 & -2 \end{pmatrix} \begin{pmatrix} 3 & 0 \\ 0 & -2 \end{pmatrix} = \begin{pmatrix} 9 & 0 \\ 0 & 4 \end{pmatrix}$$

$$AA^T = \begin{pmatrix} 3 & 0 \\ 0 & -2 \end{pmatrix} \begin{pmatrix} 3 & 0 \\ 0 & -2 \end{pmatrix} = \begin{pmatrix} 9 & 0 \\ 0 & 4 \end{pmatrix}$$

**Adim 2: Tekil degerleri (singular values) bul**

$A^T A$'nin ozdegerleri: $\lambda_1 = 9$, $\lambda_2 = 4$ (kosegen matris oldugu icin dogrudan okunur)

Tekil degerler:

$$\sigma_1 = \sqrt{\lambda_1} = \sqrt{9} = 3, \quad \sigma_2 = \sqrt{\lambda_2} = \sqrt{4} = 2$$

$$\Sigma = \begin{pmatrix} 3 & 0 \\ 0 & 2 \end{pmatrix}$$

**Adim 3: V matrisini bul (A^T A'nin ozvektorleri)**

$A^T A$ kosegen matris oldugu icin ozvektorler standart birim vektorlerdir:

- $\lambda_1 = 9$ icin: $v_1 = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$
- $\lambda_2 = 4$ icin: $v_2 = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$

$$V = \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix} = I$$

**Adim 4: U matrisini bul ($u_i = \frac{1}{\sigma_i} A v_i$ formuluyle)**

$$u_1 = \frac{1}{\sigma_1} A v_1 = \frac{1}{3} \begin{pmatrix} 3 & 0 \\ 0 & -2 \end{pmatrix} \begin{pmatrix} 1 \\ 0 \end{pmatrix} = \frac{1}{3} \begin{pmatrix} 3 \\ 0 \end{pmatrix} = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$$

$$u_2 = \frac{1}{\sigma_2} A v_2 = \frac{1}{2} \begin{pmatrix} 3 & 0 \\ 0 & -2 \end{pmatrix} \begin{pmatrix} 0 \\ 1 \end{pmatrix} = \frac{1}{2} \begin{pmatrix} 0 \\ -2 \end{pmatrix} = \begin{pmatrix} 0 \\ -1 \end{pmatrix}$$

$$U = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}$$

**Adim 5: SVD'yi yaz ve dogrula**

$$A = U \Sigma V^T = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix} \begin{pmatrix} 3 & 0 \\ 0 & 2 \end{pmatrix} \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix}$$

Dogrulama:

$$U \Sigma V^T = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix} \begin{pmatrix} 3 & 0 \\ 0 & 2 \end{pmatrix} = \begin{pmatrix} 3 & 0 \\ 0 & -2 \end{pmatrix} = A \quad ✓$$

**Onemli not:** Tekil degerler ($\sigma_1 = 3$, $\sigma_2 = 2$) her zaman negatif-olmayan sayilardir. A matrisinde -2 elemani olmasina ragmen, tekil deger olarak $\sigma_2 = 2$ (pozitif) alinir. Isaret bilgisi U matrisinde saklanir ($u_2$'nin yonu ters).

---

## Ornek 13: Norm Hesaplama ve Cauchy-Schwarz

**Soru:** $x = (1, -2, 3, -4)$ ve $y = (2, 1, -1, 3)$ vektorleri icin:

a) $\|x\|_1$, $\|x\|_2$, $\|x\|_\infty$ hesapla

b) $x^T y$ (ic carpim) hesapla

c) Cauchy-Schwarz esitsizligini dogrula: $|x^T y| \leq \|x\|_2 \cdot \|y\|_2$

**Cozum:**

**a) x vektorunun normlarini hesaplayalim**

**1-normu** (elemanlarin mutlak degerlerinin toplami):

$$\|x\|_1 = |1| + |-2| + |3| + |-4| = 1 + 2 + 3 + 4 = 10$$

**2-normu (Oklidyen norm)** (elemanlarin karelerinin toplaminin karekoku):

$$\|x\|_2 = \sqrt{1^2 + (-2)^2 + 3^2 + (-4)^2} = \sqrt{1 + 4 + 9 + 16} = \sqrt{30} \approx 5.477$$

**Sonsuzluk normu** (mutlak degerce en buyuk eleman):

$$\|x\|_\infty = \max(|1|, |-2|, |3|, |-4|) = 4$$

**Normlar arasi iliski:** Her zaman $\|x\|_\infty \leq \|x\|_2 \leq \|x\|_1$ saglanir. Kontrol edelim:

$$4 \leq 5.477 \leq 10 \quad ✓$$

**b) Ic carpimi hesaplayalim**

$$x^T y = (1)(2) + (-2)(1) + (3)(-1) + (-4)(3)$$
$$= 2 - 2 - 3 - 12 = -15$$

**c) Cauchy-Schwarz esitsizligini dogrulayalim**

Oncelikle $\|y\|_2$'yi hesaplayalim:

$$\|y\|_2 = \sqrt{2^2 + 1^2 + (-1)^2 + 3^2} = \sqrt{4 + 1 + 1 + 9} = \sqrt{15} \approx 3.873$$

Simdi esitsizligi kontrol edelim:

Sol taraf:

$$|x^T y| = |-15| = 15$$

Sag taraf:

$$\|x\|_2 \cdot \|y\|_2 = \sqrt{30} \cdot \sqrt{15} = \sqrt{450} = 15\sqrt{2} \approx 21.213$$

Cauchy-Schwarz esitsizligi:

$$|x^T y| = 15 \leq 21.213 = \|x\|_2 \cdot \|y\|_2 \quad ✓$$

Esitsizlik saglaniyor. Esitlik yalnizca $x$ ve $y$ birbirinin skaler katiysa ($x = \alpha y$) gerceklesir. Burada $15 < 21.213$ oldugu icin kesin esitsizlik var, yani $x$ ve $y$ dogrusal bagimsiz.

**Not:** Cauchy-Schwarz esitsizligi, ic carpimin buyuklugunu normlarla sinirlar ve optimizasyon ile makine ogreniminde temel bir aractir.
