# 3. Kalkulus Tekrari (Optimizasyon Icin Gereken)

## Yaklasim Hizi (Rate of Convergence)

Optimizasyon algoritmalari **iteratif** calisir: bir baslangic noktasi sec, adim adim cozume yaklas.
Peki ne kadar hizli yaklasiyorsun? Bunu olcen kavram **yaklasim hizi**.

{xₖ} dizisi x*'a yaklasiyor olsun:

### Q-Linear (Dogrusal Yaklasim)
$$\frac{\|x_{k+1} - x^*\|}{\|x_k - x^*\|} \leq r \quad \text{, } r \in (0,1)$$

Her adimda hatayi **sabit bir oranla** azaltirsin.

**Ornek:** r = 0.5 ise, her adimda hata yariya iner.
- Hata: 1 → 0.5 → 0.25 → 0.125 → ...

### Q-Superlinear (Dogrusal-Ustu)
$$\lim_{k \to \infty} \frac{\|x_{k+1} - x^*\|}{\|x_k - x^*\|} = 0$$

Oran giderek kuculuyor, yani her adim bir oncekinden **oransal olarak daha iyi**.

### Q-Order p (p. Dereceden)
$$\frac{\|x_{k+1} - x^*\|}{\|x_k - x^*\|^p} \leq M$$

p = 2 ise **kuadratik yaklasim**: hata her adimda **karesi** kadar azalir.
- Hata: 0.1 → 0.01 → 0.0001 → 0.00000001
- Newton metodu bunu basarir!

---

## Lipschitz Surekliligi

Bir fonksiyon f, N kumesinde **Lipschitz surekli** ise:

$$\|f(x) - f(y)\| \leq L \|x - y\| \quad \forall x, y \in \mathcal{N}$$

**Ne demek?** Fonksiyonun degisim hizi **sinirli**. Yani f "cok hizli" degisemez.
L sabiti ne kadar kucukse, fonksiyon o kadar "yavas" degisir.

**Ornek:** f(x) = 2x
- |f(x) - f(y)| = |2x - 2y| = 2|x - y|
- L = 2 ile Lipschitz surekli ✓

**Ornek:** f(x) = x²  (tum R'de)
- |x² - y²| = |x+y||x-y|
- |x+y| sinirli degilse L bulunamaz → Tum R'de Lipschitz degil
- Ama [-5, 5] gibi sinirli bir aralikta Lipschitz (L = 10)

**Onemli ozellik:** f ve g Lipschitz ise → f+g ve f·g de Lipschitz.

---

## Kismi Turev ve Gradient

### Tek Degiskenli Turev (Biliyorsun)
f(x) = x³ → f'(x) = 3x²

### Cok Degiskenli: Kismi Turev (Partial Derivative)

f(x₁, x₂) gibi birden fazla degiskenli fonksiyonlarda, **bir degiskene gore** turev alirken diger degiskenleri sabit tutarsin.

$$\frac{\partial f}{\partial x_i} = \lim_{h \to 0} \frac{f(x + h e_i) - f(x)}{h}$$

**Ornek:** f(x₁, x₂) = x₁² + 3x₁x₂ + x₂²

$$\frac{\partial f}{\partial x_1} = 2x_1 + 3x_2 \quad \text{(x₂'yi sabit tutuyoruz)}$$

$$\frac{\partial f}{\partial x_2} = 3x_1 + 2x_2 \quad \text{(x₁'i sabit tutuyoruz)}$$

### Gradient (Turevlerin Vektoru)

Tum kismi turevleri bir vektor icinde toplarsak **gradient** elde ederiz:

$$\nabla f(x) = \begin{pmatrix} \partial f / \partial x_1 \\ \partial f / \partial x_2 \\ \vdots \\ \partial f / \partial x_n \end{pmatrix}$$

**Yukardaki ornek icin:**

$$\nabla f(x) = \begin{pmatrix} 2x_1 + 3x_2 \\ 3x_1 + 2x_2 \end{pmatrix}$$

**Gradient ne ise yarar?**
- Gradient, fonksiyonun **en hizli arttigi yonu** gosterir
- **-∇f** (negatif gradient) ise **en hizli azaldigi yon** → minimuma gitmek icin bu yonde yuru!

### Yonlu Turev (Directional Derivative)

Gradient herhangi bir **p yonundeki** degisim hizini verir:

$$D(f(x), p) = \nabla f(x)^T p$$

Burada ||p|| = 1 (birim vektor).

---

## Hessian Matrisi

Hessian = **ikinci turevlerin matrisi**. Tek degiskende f''(x) ne ise, cok degiskende Hessian odur.

$$\nabla^2 f(x) = \begin{pmatrix} \frac{\partial^2 f}{\partial x_1^2} & \frac{\partial^2 f}{\partial x_1 \partial x_2} & \cdots \\ \frac{\partial^2 f}{\partial x_2 \partial x_1} & \frac{\partial^2 f}{\partial x_2^2} & \cdots \\ \vdots & \vdots & \ddots \end{pmatrix}$$

**Ornek:** f(x₁, x₂) = x₁² + 3x₁x₂ + x₂²

Onceki kismi turevlerden:
- ∂f/∂x₁ = 2x₁ + 3x₂
- ∂f/∂x₂ = 3x₁ + 2x₂

Simdi bunlarin da turevini alalim:

$$\nabla^2 f = \begin{pmatrix} 2 & 3 \\ 3 & 2 \end{pmatrix}$$

**Onemli:** f iki kez turevlenebilir ise Hessian **simetriktir** (sag ust = sol alt).

**Hessian ne ise yarar?**
- Fonksiyonun **egriligini** gosterir
- Hessian pozitif definit ise → o nokta **minimum** (cukur)
- Hessian negatif definit ise → o nokta **maksimum** (tepe)
- Karisik ise → **eyer noktasi** (ne min ne max)

---

## Taylor Teoremi

Tek degiskende biliyorsun:
$$f(x+h) \approx f(x) + f'(x)h + \frac{1}{2}f''(x)h^2$$

Cok degiskende **ayni mantik**, ama turev yerine gradient, f'' yerine Hessian kullanilir:

### Ortalama Deger Teoremi (Mean Value Theorem)
$$f(x+p) = f(x) + \nabla f(x + \alpha p)^T p \quad \text{, } \alpha \in (0,1)$$

### Taylor Acilimi (2. derece)
$$f(x+p) = f(x) + \nabla f(x)^T p + \frac{1}{2} p^T \nabla^2 f(x + \alpha p) \, p$$

**Neden onemli?** Optimizasyon algoritmalari fonksiyonu **Taylor acilimi ile yaklastirip** minimum bulur. Ornegin Newton metodu tam olarak bu 2. derece yaklasimi kullanir.

---

## Jacobian (Vektor Degerli Fonksiyonlar Icin)

Simdi f tek bir sayi dondermiyorsa, mesela r: R^n → R^m (n giris, m cikis):

$$r(x) = \begin{pmatrix} f_1(x_1, ..., x_n) \\ f_2(x_1, ..., x_n) \\ \vdots \\ f_m(x_1, ..., x_n) \end{pmatrix}$$

**Jacobian** = her bir f_i'nin gradientini satirlara yaz:

$$J(x) = \begin{pmatrix} \nabla f_1(x)^T \\ \nabla f_2(x)^T \\ \vdots \\ \nabla f_m(x)^T \end{pmatrix}$$

**Ornek:** r(x₁, x₂) = (x₁² + x₂, x₁x₂)

$$J = \begin{pmatrix} 2x_1 & 1 \\ x_2 & x_1 \end{pmatrix}$$

**Gradient vs Jacobian:**
- Gradient: skaler fonksiyon (R^n → R) icin, sonuc n×1 vektor
- Jacobian: vektor fonksiyon (R^n → R^m) icin, sonuc m×n matris
- Aslinda gradient, Jacobian'in ozel hali (m=1 durumu)
