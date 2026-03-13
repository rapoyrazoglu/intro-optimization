# 5. Cozulmus Ornekler

---

## Ornek 1: Steepest Descent + Exact Line Search (Kuadratik)

**Soru:** f(x,y) = 4x² - 4xy + 2y² fonksiyonunu steepest descent ile minimize et. Baslangic noktasi x₀ = (2, 3). Ilk iterasyonu exact line search ile yap.

**Cozum:**

**Adim 1: Gradient hesapla**

$$\nabla f(x,y) = \begin{pmatrix} 8x - 4y \\ -4x + 4y \end{pmatrix}$$

x₀ = (2, 3) noktasinda:

$$\nabla f(2,3) = \begin{pmatrix} 16 - 12 \\ -8 + 12 \end{pmatrix} = \begin{pmatrix} 4 \\ 4 \end{pmatrix}$$

**Adim 2: Arama yonu**

$$p_0 = -\nabla f(2,3) = \begin{pmatrix} -4 \\ -4 \end{pmatrix}$$

**Adim 3: Exact line search — α'yi bul**

Bu fonksiyon kuadratik: f(x) = (1/2)x^T Q x + ... seklinde yazilabilir.

Q matrisini bulalim. f = 4x² - 4xy + 2y² ifadesini (1/2)x^T Q x formuna getirelim:

$$Q = \begin{pmatrix} 8 & -4 \\ -4 & 4 \end{pmatrix}$$

Kuadratik fonksiyonlarda exact line search formulu:

$$\alpha = \frac{p^T \nabla f}{p^T Q \, p}$$

Pay: p₀^T ∇f = (-4)(4) + (-4)(4) = -16 - 16 = -32

Bu formuldeki pay aslinda -∇f^T ∇f = -(16+16) = -32. Mutlak deger alacagiz:

$$\alpha = \frac{\nabla f^T \nabla f}{\nabla f^T Q \, \nabla f}$$

$$\nabla f^T \nabla f = 4² + 4² = 32$$

$$Q \nabla f = \begin{pmatrix} 8 & -4 \\ -4 & 4 \end{pmatrix} \begin{pmatrix} 4 \\ 4 \end{pmatrix} = \begin{pmatrix} 16 \\ 0 \end{pmatrix}$$

$$\nabla f^T Q \nabla f = (4)(16) + (4)(0) = 64$$

$$\alpha_0 = \frac{32}{64} = \frac{1}{2}$$

**Adim 4: Yeni noktayi hesapla**

$$x_1 = x_0 + \alpha_0 p_0 = \begin{pmatrix} 2 \\ 3 \end{pmatrix} + \frac{1}{2} \begin{pmatrix} -4 \\ -4 \end{pmatrix} = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$$

**Kontrol:** f(2,3) = 4(4) - 4(6) + 2(9) = 16 - 24 + 18 = 10

f(0,1) = 0 - 0 + 2 = 2

Fonksiyon 10'dan 2'ye dustu ✓

---

## Ornek 2: Steepest Descent — Sifirdan Baslama

**Soru:** f(x₁, x₂) = 2x₁² + 2x₁x₂ + x₂² fonksiyonunu x₀ = (1, -1) noktasindan steepest descent ile 1 iterasyon uygula. Exact line search kullan.

**Cozum:**

Bu fonksiyon kuadratik: f = (1/2)x^T Q x formunda yazilabilir.

$$Q = \begin{pmatrix} 4 & 2 \\ 2 & 2 \end{pmatrix}$$

**Adim 1: Gradient hesapla**

$$\nabla f(x) = Q \cdot x$$

$$\nabla f(1,-1) = \begin{pmatrix} 4 & 2 \\ 2 & 2 \end{pmatrix} \begin{pmatrix} 1 \\ -1 \end{pmatrix} = \begin{pmatrix} 4 - 2 \\ 2 - 2 \end{pmatrix} = \begin{pmatrix} 2 \\ 0 \end{pmatrix}$$

**Adim 2: Arama yonu**

$$p_0 = -\nabla f(1,-1) = \begin{pmatrix} -2 \\ 0 \end{pmatrix}$$

**Adim 3: Exact line search — α'yi bul**

Kuadratik fonksiyonlarda exact line search formulu:

$$\alpha = \frac{\nabla f^T \nabla f}{\nabla f^T Q \, \nabla f}$$

$$\nabla f^T \nabla f = 2^2 + 0^2 = 4$$

$$Q \nabla f = \begin{pmatrix} 4 & 2 \\ 2 & 2 \end{pmatrix} \begin{pmatrix} 2 \\ 0 \end{pmatrix} = \begin{pmatrix} 8 \\ 4 \end{pmatrix}$$

$$\nabla f^T Q \nabla f = (2)(8) + (0)(4) = 16$$

$$\alpha_0 = \frac{4}{16} = \frac{1}{4}$$

**Adim 4: Yeni noktayi hesapla**

$$x_1 = x_0 + \alpha_0 p_0 = \begin{pmatrix} 1 \\ -1 \end{pmatrix} + \frac{1}{4} \begin{pmatrix} -2 \\ 0 \end{pmatrix} = \begin{pmatrix} 0.5 \\ -1 \end{pmatrix}$$

**Kontrol:**

$$f(1,-1) = 2(1)^2 + 2(1)(-1) + (-1)^2 = 2 - 2 + 1 = 1$$

$$f(0.5,-1) = 2(0.25) + 2(0.5)(-1) + 1 = 0.5 - 1 + 1 = 0.5$$

Azalis: 1 → 0.5 ✓

---

## Ornek 3: Kritik Nokta Siniflandirmasi

**Soru:** f(x₁, x₂) = x₁³x₂ - x₁x₂ fonksiyonunun tum kritik noktalarini bul ve siniflandir.

**Cozum:**

**Adim 1: ∇f = 0**

$$\nabla f = \begin{pmatrix} 3x_1^2 x_2 - x_2 \\ x_1^3 - x_1 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}$$

Ikinci denklem: x₁³ - x₁ = x₁(x₁² - 1) = 0

→ x₁ = 0 veya x₁ = 1 veya x₁ = -1

Birinci denklem: x₂(3x₁² - 1) = 0

**x₁ = 0:** x₂(0 - 1) = -x₂ = 0 → x₂ = 0. Kritik nokta: **(0, 0)**

**x₁ = 1:** x₂(3 - 1) = 2x₂ = 0 → x₂ = 0. Kritik nokta: **(1, 0)**

**x₁ = -1:** x₂(3 - 1) = 2x₂ = 0 → x₂ = 0. Kritik nokta: **(-1, 0)**

**Adim 2: Hessian hesapla**

$$\nabla^2 f = \begin{pmatrix} 6x_1 x_2 & 3x_1^2 - 1 \\ 3x_1^2 - 1 & 0 \end{pmatrix}$$

**(0, 0) noktasinda:**

$$H = \begin{pmatrix} 0 & -1 \\ -1 & 0 \end{pmatrix}$$

Ozdegerler: λ² - 1 = 0 → λ = ±1. Bir pozitif, bir negatif → **indefinit** → **eyer noktasi**

**(1, 0) noktasinda:**

$$H = \begin{pmatrix} 0 & 2 \\ 2 & 0 \end{pmatrix}$$

Ozdegerler: λ² - 4 = 0 → λ = ±2. Indefinit → **eyer noktasi**

**(-1, 0) noktasinda:**

$$H = \begin{pmatrix} 0 & 2 \\ 2 & 0 \end{pmatrix}$$

Ayni Hessian → **eyer noktasi**

**Sonuc:** Bu fonksiyonun lokal minimumu yok! Tum kritik noktalar eyer noktasi.

---

## Ornek 4: Newton Yonu Hesaplama

**Soru:** f(x₁, x₂) = x₁² + x₁x₂ + x₂² fonksiyonu icin x₀ = (1, 1) noktasinda Newton yonunu bul.

**Cozum:**

$$\nabla f = \begin{pmatrix} 2x_1 + x_2 \\ x_1 + 2x_2 \end{pmatrix}, \quad \nabla f(1,1) = \begin{pmatrix} 3 \\ 3 \end{pmatrix}$$

$$\nabla^2 f = \begin{pmatrix} 2 & 1 \\ 1 & 2 \end{pmatrix}$$

Newton yonu: p^N = -(∇²f)⁻¹ ∇f

Tersi:

$$(\nabla^2 f)^{-1} = \frac{1}{4-1} \begin{pmatrix} 2 & -1 \\ -1 & 2 \end{pmatrix} = \frac{1}{3} \begin{pmatrix} 2 & -1 \\ -1 & 2 \end{pmatrix}$$

$$p^N = -\frac{1}{3} \begin{pmatrix} 2 & -1 \\ -1 & 2 \end{pmatrix} \begin{pmatrix} 3 \\ 3 \end{pmatrix} = -\frac{1}{3} \begin{pmatrix} 3 \\ 3 \end{pmatrix} = \begin{pmatrix} -1 \\ -1 \end{pmatrix}$$

$$x_1 = x_0 + p^N = (1,1) + (-1,-1) = (0, 0)$$

**Kontrol:** ∇f(0,0) = (0, 0). Gradient sifir — **tek adimda cozumu bulduk!**

Bu beklenen bir sonuc cunku f kuadratik ve Newton yontemi kuadratik fonksiyonlari 1 adimda cozer.

---

## Ornek 5: Wolfe Kosullari Kontrolu

**Soru:** f(x) = x² fonksiyonunda x₀ = 2, p₀ = -1 (steepest descent yonu). α = 0.5 adim uzunlugu Wolfe kosullarini sagliyor mu? (c₁ = 10⁻⁴, c₂ = 0.9)

**Cozum:**

Bilinen degerler:

$$f(x_0) = f(2) = 4, \quad f'(x_0) = 2x_0 = 4, \quad p_0 = -1$$

$$\varphi(\alpha) = f(x_0 + \alpha p_0) = f(2 - \alpha) = (2 - \alpha)^2$$

**Wolfe Kosulu 1 — Armijo (sufficient decrease):**

$$f(x_0 + \alpha p_0) \leq f(x_0) + c_1 \alpha \nabla f^T p$$

$$f(2 - 0.5) = f(1.5) = 2.25$$

$$f(x_0) + c_1 \alpha \nabla f^T p = 4 + 10^{-4} \cdot 0.5 \cdot (4)(-1) = 4 - 0.0002 = 3.9998$$

$$2.25 \leq 3.9998 \quad \checkmark$$

**Wolfe Kosulu 2 — Curvature condition:**

$$\nabla f(x_0 + \alpha p_0)^T p \geq c_2 \nabla f(x_0)^T p$$

$$f'(1.5) \cdot (-1) = 2(1.5) \cdot (-1) = 3 \cdot (-1) = -3$$

$$c_2 \nabla f(x_0)^T p = 0.9 \cdot (4)(-1) = -3.6$$

$$-3 \geq -3.6 \quad \checkmark$$

Her iki kosul da saglaniyor → α = 0.5 kabul edilebilir bir adim uzunlugudur.

**Yorum:** Armijo kosulu adimin "yeterince" azalma sagladigini kontrol eder. Curvature kosulu ise adimin "cok kisa" olmadigini garanti eder (gradient yeterince azalmis olmali).

---

## Ornek 6: Konveks Fonksiyonda Global Minimum

**Soru:** f(x,y) = x² + 2xy + y² fonksiyonunun konveks oldugunu goster. Kritik noktalarini bul.

**Cozum:**

f(x,y) = (x + y)² ≥ 0 (tam kare!)

**Hessian:**

$$\nabla f = \begin{pmatrix} 2x + 2y \\ 2x + 2y \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}$$

→ x + y = 0 → y = -x. Yani **sonsuz kritik nokta** var: {(t, -t) : t ∈ R}

$$\nabla^2 f = \begin{pmatrix} 2 & 2 \\ 2 & 2 \end{pmatrix}$$

Ozdegerler: λ₁ = 4, λ₂ = 0. Pozitif **semi-definit** (sifir ozdeger var).

Fonksiyon konveks cunku Hessian pozitif semi-definit. Tum kritik noktalar global minimum: f(t,-t) = 0.

**Not:** Sifir ozdeger "duz yon" demek — (1,-1) yonunde fonksiyon ne artar ne azalir.

---

## Ornek 7: Eyer Noktasi Ornegi

**Soru:** f(x₁, x₂) = x₁² - x₂² fonksiyonunun (0,0) noktasindaki turunu belirle.

**Cozum:**

$$\nabla f = \begin{pmatrix} 2x_1 \\ -2x_2 \end{pmatrix}, \quad \nabla f(0,0) = \begin{pmatrix} 0 \\ 0 \end{pmatrix}$$

Duragan nokta ✓

$$\nabla^2 f = \begin{pmatrix} 2 & 0 \\ 0 & -2 \end{pmatrix}$$

Ozdegerler: λ₁ = 2 > 0, λ₂ = -2 < 0 → **indefinit** → **eyer noktasi**

**Sezgisel:** x₁ yonunde yukari bakiyor (minimum benzeri), x₂ yonunde asagi bakiyor (maksimum benzeri). Tam bir at eyeri!

---

## Ornek 8: Rosenbrock Fonksiyonu — Gradient ve Hessian

**Soru:** Rosenbrock fonksiyonu f(x₁, x₂) = 100(x₂ - x₁²)² + (1 - x₁)² icin gradient ve Hessiani hesapla.

**Cozum:**

**Gradient:**

$$\frac{\partial f}{\partial x_1} = 100 \cdot 2(x_2 - x_1^2)(-2x_1) + 2(1-x_1)(-1) = -400x_1(x_2 - x_1^2) - 2(1 - x_1)$$

$$\frac{\partial f}{\partial x_2} = 100 \cdot 2(x_2 - x_1^2) = 200(x_2 - x_1^2)$$

$$\nabla f = \begin{pmatrix} -400x_1(x_2 - x_1^2) - 2(1-x_1) \\ 200(x_2 - x_1^2) \end{pmatrix}$$

**Minimumu bulalim:** ∇f = 0

Ikinci denklem: x₂ - x₁² = 0 → x₂ = x₁²

Birinci denklem: 0 - 2(1 - x₁) = 0 → x₁ = 1, x₂ = 1

Minimum: **(1, 1)**, f(1,1) = 0.

**Hessian:**

$$\nabla^2 f = \begin{pmatrix} -400(x_2 - 3x_1^2) + 2 & -400x_1 \\ -400x_1 & 200 \end{pmatrix}$$

(1,1) noktasinda:

$$\nabla^2 f(1,1) = \begin{pmatrix} -400(1-3) + 2 & -400 \\ -400 & 200 \end{pmatrix} = \begin{pmatrix} 802 & -400 \\ -400 & 200 \end{pmatrix}$$

Ozdegerleri: det = 802·200 - 160000 = 400 > 0 ve iz = 1002 > 0 → **pozitif definit** ✓

---

## Ornek 9: Descent Direction Kontrolu

**Soru:** f(x₁, x₂) = x₁² + 4x₂² fonksiyonu icin x = (2, 1) noktasinda asagidaki yonlerin inis yonu olup olmadigini belirle:
- a) p = (-1, 0)
- b) p = (0, 1)
- c) p = (-1, -1)

**Cozum:**

$$\nabla f(2,1) = \begin{pmatrix} 2(2) \\ 8(1) \end{pmatrix} = \begin{pmatrix} 4 \\ 8 \end{pmatrix}$$

Inis yonu kosulu: p^T ∇f < 0

**a) p = (-1, 0):**
p^T ∇f = (-1)(4) + (0)(8) = -4 < 0 → **Inis yonu** ✓

**b) p = (0, 1):**
p^T ∇f = (0)(4) + (1)(8) = 8 > 0 → **Inis yonu degil** ✗ (cikis yonu)

**c) p = (-1, -1):**
p^T ∇f = (-1)(4) + (-1)(8) = -12 < 0 → **Inis yonu** ✓

**Yorum:** b yonu gradient ile ayni tarafa isaret ediyor (yukari), yani o yone yurursek f artar. a ve c yonleri gradientin karsi tarafinda, yani f azalir.

---

## Ornek 10: Kuadratik Fonksiyonda Newton vs Steepest Descent

**Soru:** f(x₁, x₂) = 3x₁² + 2x₂² - 2x₁x₂ - 4x₁ fonksiyonunu (0, 0) noktasindan baslayarak hem Newton hem steepest descent ile 1'er iterasyon uygula. Karsilastir.

**Cozum:**

$$\nabla f = \begin{pmatrix} 6x_1 - 2x_2 - 4 \\ 4x_2 - 2x_1 \end{pmatrix}, \quad \nabla f(0,0) = \begin{pmatrix} -4 \\ 0 \end{pmatrix}$$

$$\nabla^2 f = \begin{pmatrix} 6 & -2 \\ -2 & 4 \end{pmatrix}$$

### Newton Yontemi:

$$p^N = -(\nabla^2 f)^{-1} \nabla f$$

$$(\nabla^2 f)^{-1} = \frac{1}{24-4} \begin{pmatrix} 4 & 2 \\ 2 & 6 \end{pmatrix} = \frac{1}{20} \begin{pmatrix} 4 & 2 \\ 2 & 6 \end{pmatrix}$$

$$p^N = -\frac{1}{20} \begin{pmatrix} 4 & 2 \\ 2 & 6 \end{pmatrix} \begin{pmatrix} -4 \\ 0 \end{pmatrix} = -\frac{1}{20} \begin{pmatrix} -16 \\ -8 \end{pmatrix} = \begin{pmatrix} 0.8 \\ 0.4 \end{pmatrix}$$

$$x_1^{Newton} = (0,0) + (0.8, 0.4) = (0.8, 0.4)$$

f(0.8, 0.4) = 3(0.64) + 2(0.16) - 2(0.32) - 4(0.8) = 1.92 + 0.32 - 0.64 - 3.2 = **-1.6**

∇f(0.8, 0.4) = (6(0.8) - 2(0.4) - 4, 4(0.4) - 2(0.8)) = (0, 0) → **Tam cozum!**

### Steepest Descent:

p₀ = -∇f(0,0) = (4, 0)

Q = [[6,-2],[-2,4]] → Q p₀ = [24, -8]^T

$$\alpha_0 = \frac{p_0^T p_0}{p_0^T Q p_0} = \frac{16}{(4)(24) + (0)(-8)} = \frac{16}{96} = \frac{1}{6}$$

$$x_1^{SD} = (0,0) + \frac{1}{6}(4, 0) = (0.667, 0)$$

f(0.667, 0) = 3(0.444) - 4(0.667) = 1.333 - 2.667 = **-1.333**

∇f(0.667, 0) = (6(0.667) - 4, -2(0.667)) = (0, -1.333) ≠ 0 → Henuz bitmedi.

### Karsilastirma

| | Newton | Steepest Descent |
|--|--------|-----------------|
| x₁ | (0.8, 0.4) | (0.667, 0) |
| f(x₁) | -1.6 | -1.333 |
| ∇f(x₁) | (0, 0) ✓ | (0, -1.33) |
| Bitti mi? | **Evet** | Hayir |

Newton 1 adimda bitirdi, steepest descent devam etmeli.

---

## Ornek 11: Dejenere Kritik Nokta

**Soru:** f(x,y) = x² + ay² + by⁴ fonksiyonu. Orijinin kritik noktasini siniflandir (a ve b genel).

**Cozum:**

$$\nabla f = \begin{pmatrix} 2x \\ 2ay + 4by^3 \end{pmatrix}, \quad \nabla f(0,0) = \begin{pmatrix} 0 \\ 0 \end{pmatrix}$$

Duragan nokta ✓

$$\nabla^2 f = \begin{pmatrix} 2 & 0 \\ 0 & 2a + 12by^2 \end{pmatrix}$$

Orijinde:

$$\nabla^2 f(0,0) = \begin{pmatrix} 2 & 0 \\ 0 & 2a \end{pmatrix}$$

- **a > 0:** Ozdegerler 2 ve 2a, ikisi de pozitif → **lokal minimum**
- **a < 0:** Ozdegerler 2 ve 2a (negatif) → **eyer noktasi**
- **a = 0:** Hessian = [[2,0],[0,0]]. Ozdegerler 2 ve 0 → **dejenere**. 4. turev bilgisi lazim:
  - b > 0 ise: y⁴ terimi sonunda yukari ceker → **minimum**
  - b < 0 ise: y⁴ terimi asagiya ceker → eyer noktasi
  - b = 0 ise: f = x² → y ekseninde sabit, minimum olarak kabul edilebilir

---

## Ornek 12: Cok Degiskenli Kritik Nokta Bulma

**Soru:** f(x₁, x₂) = x₁²x₂ - x₁x₂ fonksiyonunun tum extremum (maksimum/minimum) noktalarini bul.

**Cozum:**

**Adim 1: ∇f = 0**

$$\frac{\partial f}{\partial x_1} = 2x_1 x_2 - x_2 = x_2(2x_1 - 1) = 0$$

$$\frac{\partial f}{\partial x_2} = x_1^2 - x_1 = x_1(x_1 - 1) = 0$$

Ikinci denklem: x₁ = 0 veya x₁ = 1

Birinci denklem: x₂ = 0 veya x₁ = 1/2

Kombinasyonlar:
- x₁ = 0, x₂ = 0 → **(0, 0)**
- x₁ = 0, x₁ = 1/2 → celiskili (x₁ ayni anda 0 ve 1/2 olamaz)
- x₁ = 1, x₂ = 0 → **(1, 0)**
- x₁ = 1, x₁ = 1/2 → celiskili

Kritik noktalar: **(0, 0)** ve **(1, 0)**

**Adim 2: Hessian**

$$\nabla^2 f = \begin{pmatrix} 2x_2 & 2x_1 - 1 \\ 2x_1 - 1 & 0 \end{pmatrix}$$

**(0, 0):**

$$H = \begin{pmatrix} 0 & -1 \\ -1 & 0 \end{pmatrix}$$

det(H) = 0 - 1 = -1 < 0 → **eyer noktasi**

**(1, 0):**

$$H = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}$$

det(H) = 0 - 1 = -1 < 0 → **eyer noktasi**

**Sonuc:** Bu fonksiyonun lokal minimumu veya maksimumu yok. Tum kritik noktalar eyer noktasi.

---

## Ornek 13: Exact Line Search Formulu — Kuadratik Dogrulama

**Soru:** f(x) = (1/2)x^T Q x - b^T x ile Q = [[4,2],[2,2]], b = [0,0]. x₀ = (2, -2) noktasindan steepest descent uygula. α icin kapali formulu dogrula.

**Cozum:**

∇f(x) = Qx - b = Qx

$$\nabla f(2,-2) = \begin{pmatrix} 4 & 2 \\ 2 & 2 \end{pmatrix} \begin{pmatrix} 2 \\ -2 \end{pmatrix} = \begin{pmatrix} 4 \\ 0 \end{pmatrix}$$

p₀ = -(4, 0)

**Formul ile:**

$$\alpha = \frac{\nabla f^T \nabla f}{\nabla f^T Q \nabla f} = \frac{16}{(4, 0) \begin{pmatrix} 4 & 2 \\ 2 & 2 \end{pmatrix} \begin{pmatrix} 4 \\ 0 \end{pmatrix}} = \frac{16}{(4,0)(16, 8)^T} = \frac{16}{64} = \frac{1}{4}$$

**Dogrudan hesapla:**

φ(α) = f(x₀ + α p₀) = f(2 - 4α, -2)

= (1/2)[(2-4α), -2] Q [(2-4α), -2]^T

= (1/2)[(2-4α)²·4 + 2(2-4α)(-2)·2 + (-2)²·2]

Bu biraz karisik, ama φ'(α) = 0 cozuldugunde α = 1/4 cikacaktir ✓

$$x_1 = (2,-2) + \frac{1}{4}(-4, 0) = (1, -2)$$

f(2,-2) = (1/2)[4·4 + 2·2·(-2)·2 + 2·4] = (1/2)[16 - 8·2 + 8]... Daha basit hesaplayalim:

f(x) = (1/2)x^T Qx = (1/2)[4(4) + 2(2)(-2) + 2(2)(-2) + 2(4)] = (1/2)[16 - 8 - 8 + 8] = 4

f(1,-2) = (1/2)[4(1) + 2(1)(-2) + 2(1)(-2) + 2(4)] = (1/2)[4 - 4 - 4 + 8] = 2

f: 4 → 2. Azalis var ✓

---

## Ornek 14: Armijo Kosulu (Backtracking Line Search)

**Soru:** f(x₁, x₂) = x₁² + 4x₂² fonksiyonunda x₀ = (4, 1), p₀ = -∇f = (-8, -8). Backtracking line search ile uygun α'yi bul (c₁ = 0.5, ρ = 0.5, α̂ = 1).

**Cozum:**

Oncelikle gradient ve fonksiyon degerini hesaplayalim:

$$\nabla f = \begin{pmatrix} 2x_1 \\ 8x_2 \end{pmatrix}, \quad \nabla f(4,1) = \begin{pmatrix} 8 \\ 8 \end{pmatrix}$$

$$f(x_0) = f(4,1) = 16 + 4 = 20$$

$$p_0 = -\nabla f = (-8, -8)$$

Armijo kosulunda kullanilacak yonlu turev:

$$\nabla f^T p = (8)(-8) + (8)(-8) = -64 - 64 = -128$$

Armijo kosulu: $f(x_0 + \alpha p_0) \leq f(x_0) + c_1 \alpha \nabla f^T p$

**α = 1:** $x = (4-8, 1-8) = (-4, -7)$

$$f(-4,-7) = 16 + 196 = 212$$

$$20 + 0.5(1)(-128) = 20 - 64 = -44$$

$$212 \leq -44 \text{ ?} \quad \text{Hayir} \quad \times$$

**α = 0.5:** $x = (4-4, 1-4) = (0, -3)$

$$f(0,-3) = 0 + 36 = 36$$

$$20 + 0.5(0.5)(-128) = 20 - 32 = -12$$

$$36 \leq -12 \text{ ?} \quad \text{Hayir} \quad \times$$

**α = 0.25:** $x = (4-2, 1-2) = (2, -1)$

$$f(2,-1) = 4 + 4 = 8$$

$$20 + 0.5(0.25)(-128) = 20 - 16 = 4$$

$$8 \leq 4 \text{ ?} \quad \text{Hayir} \quad \times$$

**α = 0.125:** $x = (4-1, 1-1) = (3, 0)$

$$f(3,0) = 9 + 0 = 9$$

$$20 + 0.5(0.125)(-128) = 20 - 8 = 12$$

$$9 \leq 12 \text{ ?} \quad \text{Evet} \quad \checkmark$$

α = 0.125 kabul edildi. f degeri 20'den 9'a dustu.

**Yorum:** Steepest descent yonu (-8, -8) bu problemde iyi bir yon degil cunku fonksiyonun x₁ ve x₂ yonlerindeki egrilikleri farkli (1 ve 4). Bu yuzden buyuk adimlar basarisiz oluyor ve backtracking birden fazla kuculme yapiyor.

---

## Ornek 15: Trust Region Alt Problemi (2D)

**Soru:** f(x) ≈ m(p) = f₀ + g^T p + (1/2)p^T B p ile f₀ = 10, g = [2, 4]^T, B = [[2, 0],[0, 2]]. Trust region yaricapi Δ = 1. Cauchy noktasini bul.

**Cozum:**

Cauchy noktasi, steepest descent yonunde trust region sinirinda veya oncesinde bulunan noktadir.

**Adim 1: Steepest descent yonu**

$$p^{SD} = -g = \begin{pmatrix} -2 \\ -4 \end{pmatrix}$$

$$\|p^{SD}\| = \sqrt{4 + 16} = \sqrt{20} \approx 4.47$$

Bu deger Δ = 1'den buyuk, yani tam steepest descent adimi trust region disina cikiyor.

**Adim 2: Cauchy noktasini hesapla**

Trust region sinirinda, gradient yonunde keselim:

$$p^C = -\Delta \cdot \frac{g}{\|g\|} = -1 \cdot \frac{1}{\sqrt{20}} \begin{pmatrix} 2 \\ 4 \end{pmatrix} = \begin{pmatrix} -2/\sqrt{20} \\ -4/\sqrt{20} \end{pmatrix} \approx \begin{pmatrix} -0.447 \\ -0.894 \end{pmatrix}$$

**Adim 3: Model degerini hesapla**

$$g^T p^C = (2)(-0.447) + (4)(-0.894) = -0.894 - 3.578 = -4.472$$

B = 2I oldugu icin:

$$\frac{1}{2} (p^C)^T B \, p^C = \frac{1}{2} \cdot 2 \cdot \|p^C\|^2 = \|p^C\|^2 = 1$$

$$m(p^C) = 10 + (-4.472) + 1 = 6.528$$

**Adim 4: Kisitlanmamis Newton adimi ile karsilastir**

$$p^N = -B^{-1} g = -\frac{1}{2} \begin{pmatrix} 2 \\ 4 \end{pmatrix} = \begin{pmatrix} -1 \\ -2 \end{pmatrix}$$

$$\|p^N\| = \sqrt{1 + 4} = \sqrt{5} \approx 2.24 > \Delta = 1$$

Newton adimi da trust region disinda! Bu nedenle kisitli cozum gerekiyor.

$$m(p^N) = 10 + (2)(-1) + (4)(-2) + \frac{1}{2} \cdot 2 \cdot (1 + 4) = 10 - 2 - 8 + 5 = 5$$

Cauchy noktasi m = 6.528, Newton m = 5. Newton daha iyi ama trust region disinda. Gercek trust region alt problemi cozumu bu ikisi arasinda, sinir uzerinde bir noktada olacaktir.

---

## Ornek 16: BFGS Guncelleme

**Soru:** BFGS yontemiyle H₀ = I (2×2 birim matris) baslangicindan ilk guncellemeyi yap.
x₀ = (2, 1), x₁ = (1, 0.5), ∇f(x₀) = (6, 4), ∇f(x₁) = (1, 1).

**Cozum:**

**Adim 1: s ve y vektorlerini hesapla**

$$s = x_1 - x_0 = \begin{pmatrix} 1 - 2 \\ 0.5 - 1 \end{pmatrix} = \begin{pmatrix} -1 \\ -0.5 \end{pmatrix}$$

$$y = \nabla f_1 - \nabla f_0 = \begin{pmatrix} 1 - 6 \\ 1 - 4 \end{pmatrix} = \begin{pmatrix} -5 \\ -3 \end{pmatrix}$$

**Adim 2: ρ'yu hesapla**

$$\rho = \frac{1}{y^T s} = \frac{1}{(-5)(-1) + (-3)(-0.5)} = \frac{1}{5 + 1.5} = \frac{1}{6.5} = \frac{2}{13}$$

**Adim 3: BFGS formulunu uygula**

$$H_1 = (I - \rho \, s \, y^T) \, H_0 \, (I - \rho \, y \, s^T) + \rho \, s \, s^T$$

Ara matrisleri hesaplayalim:

$$\rho \, s \, y^T = \frac{2}{13} \begin{pmatrix} -1 \\ -0.5 \end{pmatrix} \begin{pmatrix} -5 & -3 \end{pmatrix} = \frac{2}{13} \begin{pmatrix} 5 & 3 \\ 2.5 & 1.5 \end{pmatrix} = \begin{pmatrix} 10/13 & 6/13 \\ 5/13 & 3/13 \end{pmatrix}$$

$$I - \rho \, s \, y^T = \begin{pmatrix} 1 - 10/13 & -6/13 \\ -5/13 & 1 - 3/13 \end{pmatrix} = \begin{pmatrix} 3/13 & -6/13 \\ -5/13 & 10/13 \end{pmatrix}$$

$$\rho \, y \, s^T = \frac{2}{13} \begin{pmatrix} -5 \\ -3 \end{pmatrix} \begin{pmatrix} -1 & -0.5 \end{pmatrix} = \frac{2}{13} \begin{pmatrix} 5 & 2.5 \\ 3 & 1.5 \end{pmatrix} = \begin{pmatrix} 10/13 & 5/13 \\ 6/13 & 3/13 \end{pmatrix}$$

$$I - \rho \, y \, s^T = \begin{pmatrix} 3/13 & -5/13 \\ -6/13 & 10/13 \end{pmatrix}$$

H₀ = I oldugu icin:

$$(I - \rho \, s \, y^T) \, H_0 \, (I - \rho \, y \, s^T) = \begin{pmatrix} 3/13 & -6/13 \\ -5/13 & 10/13 \end{pmatrix} \begin{pmatrix} 3/13 & -5/13 \\ -6/13 & 10/13 \end{pmatrix}$$

$$= \begin{pmatrix} 9/169 + 36/169 & -15/169 - 60/169 \\ -15/169 - 60/169 & 25/169 + 100/169 \end{pmatrix} = \begin{pmatrix} 45/169 & -75/169 \\ -75/169 & 125/169 \end{pmatrix}$$

$$\rho \, s \, s^T = \frac{2}{13} \begin{pmatrix} 1 & 0.5 \\ 0.5 & 0.25 \end{pmatrix} = \begin{pmatrix} 2/13 & 1/13 \\ 1/13 & 0.5/13 \end{pmatrix}$$

$$H_1 = \begin{pmatrix} 45/169 & -75/169 \\ -75/169 & 125/169 \end{pmatrix} + \begin{pmatrix} 26/169 & 13/169 \\ 13/169 & 6.5/169 \end{pmatrix} = \begin{pmatrix} 71/169 & -62/169 \\ -62/169 & 131.5/169 \end{pmatrix}$$

$$H_1 \approx \begin{pmatrix} 0.420 & -0.367 \\ -0.367 & 0.778 \end{pmatrix}$$

**Dogrulama:** H₁ simetrik olmali ✓ ve pozitif definit olmali. det(H₁) ≈ 0.420 · 0.778 - 0.367² ≈ 0.327 - 0.135 = 0.192 > 0, iz > 0 → pozitif definit ✓

**Not:** BFGS guncelleme formulu, ters Hessian yaklasimini her iterasyonda rank-2 duzelme ile gunceller. y^T s > 0 kosulunun saglanmasi (burada 6.5 > 0 ✓) pozitif definitligin korunmasini garanti eder.

---

## Ornek 17: Conjugate Gradient (Kuadratik)

**Soru:** Ax = b sistemi icin conjugate gradient uygula. A = [[2, 1],[1, 2]], b = [3, 3]^T. x₀ = (0, 0).

**Cozum:**

Conjugate gradient (CG) yontemi Ax = b lineer sistemini (veya esdeger olarak f(x) = (1/2)x^T A x - b^T x minimizasyonunu) cozer.

**Iterasyon 0:**

Residual (kalinti) hesapla:

$$r_0 = b - A x_0 = \begin{pmatrix} 3 \\ 3 \end{pmatrix} - \begin{pmatrix} 0 \\ 0 \end{pmatrix} = \begin{pmatrix} 3 \\ 3 \end{pmatrix}$$

Ilk arama yonu:

$$p_0 = r_0 = \begin{pmatrix} 3 \\ 3 \end{pmatrix}$$

Adim uzunlugu:

$$\alpha_0 = \frac{r_0^T r_0}{p_0^T A p_0}$$

$$r_0^T r_0 = 9 + 9 = 18$$

$$A p_0 = \begin{pmatrix} 2 & 1 \\ 1 & 2 \end{pmatrix} \begin{pmatrix} 3 \\ 3 \end{pmatrix} = \begin{pmatrix} 9 \\ 9 \end{pmatrix}$$

$$p_0^T A p_0 = (3)(9) + (3)(9) = 27 + 27 = 54$$

$$\alpha_0 = \frac{18}{54} = \frac{1}{3}$$

Yeni nokta:

$$x_1 = x_0 + \alpha_0 p_0 = \begin{pmatrix} 0 \\ 0 \end{pmatrix} + \frac{1}{3} \begin{pmatrix} 3 \\ 3 \end{pmatrix} = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$$

Yeni residual:

$$r_1 = r_0 - \alpha_0 A p_0 = \begin{pmatrix} 3 \\ 3 \end{pmatrix} - \frac{1}{3} \begin{pmatrix} 9 \\ 9 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}$$

r₁ = 0 → **Yakinlasti!** x* = (1, 1)

**Dogrulama:**

$$A x^* = \begin{pmatrix} 2 & 1 \\ 1 & 2 \end{pmatrix} \begin{pmatrix} 1 \\ 1 \end{pmatrix} = \begin{pmatrix} 3 \\ 3 \end{pmatrix} = b \quad \checkmark$$

**Not:** CG yontemi n×n boyutlu bir sistem icin en fazla n iterasyonda yakinsasin garanti eder. Burada n = 2 idi ama 1 iterasyonda cozum bulundu. Bunun nedeni r₀ ve p₀'in A'nin bir ozvektoru yonunde olmasi: A · [1,1]^T = 3 · [1,1]^T yani [1,1] ozdeger 3'e karsilik gelen ozvektordur.

---

## Ornek 18: Yakinlasma Hizi Karsilastirmasi

**Soru:** f(x, y) = 50x² + y² fonksiyonunu x₀ = (1, 1) noktasindan minimize ederken steepest descent ve Newton yonteminin yakinlasma davranisini karsilastir.

**Cozum:**

Bu fonksiyon kotu kosullanmis (ill-conditioned): κ = λ_max / λ_min = 100 / 2 = 50.

$$\nabla f = \begin{pmatrix} 100x \\ 2y \end{pmatrix}, \quad \nabla^2 f = H = \begin{pmatrix} 100 & 0 \\ 0 & 2 \end{pmatrix}$$

### Newton Yontemi:

$$p^N = -H^{-1} \nabla f(1,1) = -\begin{pmatrix} 1/100 & 0 \\ 0 & 1/2 \end{pmatrix} \begin{pmatrix} 100 \\ 2 \end{pmatrix} = -\begin{pmatrix} 1 \\ 1 \end{pmatrix}$$

$$x_1 = (1,1) + (-1,-1) = (0, 0)$$

**1 adimda bitti!** f(0,0) = 0. Bu beklenen bir sonuctur: Newton kuadratik fonksiyonlari tek iterasyonda cozer.

### Steepest Descent:

**Iterasyon 0:**

$$\nabla f(1,1) = \begin{pmatrix} 100 \\ 2 \end{pmatrix}, \quad p_0 = \begin{pmatrix} -100 \\ -2 \end{pmatrix}$$

Q = [[100, 0], [0, 2]] icin exact line search:

$$\alpha_0 = \frac{\nabla f^T \nabla f}{\nabla f^T Q \nabla f} = \frac{100^2 + 2^2}{100^2 \cdot 100 + 2^2 \cdot 2} = \frac{10004}{1000004} \approx 0.01$$

$$x_1 = \begin{pmatrix} 1 \\ 1 \end{pmatrix} + 0.01 \begin{pmatrix} -100 \\ -2 \end{pmatrix} = \begin{pmatrix} 0 \\ 0.98 \end{pmatrix}$$

$$f(0, 0.98) = 0 + 0.96 = 0.96$$

**Iterasyon 1:**

$$\nabla f(0, 0.98) = \begin{pmatrix} 0 \\ 1.96 \end{pmatrix}, \quad p_1 = \begin{pmatrix} 0 \\ -1.96 \end{pmatrix}$$

$$\alpha_1 = \frac{1.96^2}{1.96^2 \cdot 2} = \frac{1}{2} = 0.5$$

$$x_2 = \begin{pmatrix} 0 \\ 0.98 \end{pmatrix} + 0.5 \begin{pmatrix} 0 \\ -1.96 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}$$

$$f(0, 0) = 0$$

Bu ornekte steepest descent 2 adimda yakinsadi (baslangic noktasi uygun oldugu icin). Ancak genel durumda, kotu kosullanmis problemlerde steepest descent **zigzag** yapar ve cok yavas yakinsir.

### Karsilastirma Tablosu

| | Newton | Steepest Descent |
|--|--------|-----------------|
| Iterasyon sayisi | **1** | 2 (bu ornekte) |
| Her iterasyonun maliyeti | H⁻¹ hesapla (pahali) | Sadece gradient (ucuz) |
| Kosul sayisina duyarlilik | **Yok** | Cok yuksek |
| Yakinlasma hizi | Kuadratik | Lineer |

**Sonuc:** Newton yontemi kosul sayisindan etkilenmez cunku Hessian bilgisi ile yonleri duzelttir. Steepest descent ise sadece gradient kullanir ve kotu kosullanmis problemlerde zigzag yaparak cok yavas yakinsir. Ornegin κ = 50 oldugunda steepest descent'in yakinlasma orani en kotu durumda ((κ-1)/(κ+1))² = (49/51)² ≈ 0.923 olur, yani her iterasyonda hatayi sadece %7.7 azaltir.
