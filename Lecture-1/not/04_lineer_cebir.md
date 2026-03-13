# 4. Lineer Cebir Tekrari

## Vektor

Bir **kolon vektor** x ∈ R^n:

$$x = \begin{pmatrix} x_1 \\ x_2 \\ \vdots \\ x_n \end{pmatrix}$$

**Transpose (devrik):** Kolon vektoru satir vektore cevirir:

$$x^T = (x_1, x_2, \ldots, x_n)$$

### Ic Carpim (Inner Product / Dot Product)

$$x^T y = \sum_{i=1}^{n} x_i y_i = x_1 y_1 + x_2 y_2 + \cdots + x_n y_n$$

**Ornek:** x = (1, 2, 3)^T, y = (4, 5, 6)^T
- x^T y = 1·4 + 2·5 + 3·6 = 4 + 10 + 18 = 32

### Vektor Normlari (Buyukluk Olcusu)

Bir vektorun "uzunlugunu" olcmenin farkli yollari:

| Norm | Formul | Anlam | Ornek: x = (3, -4) |
|------|--------|-------|---------------------|
| 1-norm | $\|x\|_1 = \sum \|x_i\|$ | Mutlak degerlerin toplami | \|3\| + \|-4\| = 7 |
| 2-norm | $\|x\|_2 = \sqrt{\sum x_i^2}$ | Oklid uzunlugu (bildigin uzunluk) | √(9+16) = 5 |
| ∞-norm | $\|x\|_\infty = \max \|x_i\|$ | En buyuk eleman | max(3, 4) = 4 |

**2-norm en cok kullanilan.** "Vektorun uzunlugu" denince genelde budur.

---

## Matris

m×n boyutlu matris A:

$$A = \begin{pmatrix} A_{11} & A_{12} & \cdots & A_{1n} \\ A_{21} & A_{22} & \cdots & A_{2n} \\ \vdots & & & \vdots \\ A_{m1} & A_{m2} & \cdots & A_{mn} \end{pmatrix}$$

### Transpose (Devrik)
Satirlari ve sutunlari yer degistirir: $(A^T)_{ij} = A_{ji}$

### Simetrik Matris
$A^T = A$ ise matris **simetriktir**. Yani $A_{ij} = A_{ji}$.

**Ornek:**

$$A = \begin{pmatrix} 1 & 3 \\ 3 & 2 \end{pmatrix} \quad \text{simetriktir (sag ust = sol alt)}$$

### Matris Normu

$$\|A\|_p = \max_{\|x\|_p = 1} \|Ax\|_p$$

"A'nin bir birim vektoru ne kadar buyutebilecegi"

---

## Ozdeger ve Ozvektor (Eigenvalue & Eigenvector)

Bu kavram optimizasyonda **cok** onemli!

### Tanim
A bir n×n matris. Eger sifir olmayan bir x vektoru icin:

$$Ax = \lambda x$$

ise, **$\lambda$ ozdeger**, **x ozvektor**.

**Ne demek?** A matrisi x vektorunu carptdiginda, x'in **yonu degismiyor**, sadece $\lambda$ kati buyuyor/kuculuyor.

**Ornek:**

$$A = \begin{pmatrix} 2 & 1 \\ 1 & 2 \end{pmatrix}$$

x = (1, 1)^T deneyelim:

$$Ax = \begin{pmatrix} 2 & 1 \\ 1 & 2 \end{pmatrix} \begin{pmatrix} 1 \\ 1 \end{pmatrix} = \begin{pmatrix} 3 \\ 3 \end{pmatrix} = 3 \begin{pmatrix} 1 \\ 1 \end{pmatrix}$$

λ = 3, x = (1,1)^T bir ozdeger-ozvektor cifti!

x = (1, -1)^T deneyelim:

$$Ax = \begin{pmatrix} 2 & 1 \\ 1 & 2 \end{pmatrix} \begin{pmatrix} 1 \\ -1 \end{pmatrix} = \begin{pmatrix} 1 \\ -1 \end{pmatrix} = 1 \begin{pmatrix} 1 \\ -1 \end{pmatrix}$$

λ = 1, x = (1,-1)^T bir diger cift!

### Ozdegerleri Bulma
det(A - λI) = 0 denklemini coz.

Yukaridaki ornek icin:
- det([[2-λ, 1], [1, 2-λ]]) = (2-λ)² - 1 = 0
- λ² - 4λ + 3 = 0 → λ = 3, λ = 1 ✓

### Simetrik Pozitif Definit (SPD) Matris

A **simetrik pozitif definit** ise:
1. A^T = A (simetrik)
2. Tum ozdegerleri **pozitif** (λ > 0)

**Esdeger tanim:** Her sifir olmayan x icin: $x^T A x > 0$

**Neden onemli?** f(x)'in Hessian'i SPD ise → o nokta kesinlikle **minimum**!

### Eigen-Decomposition

A'nin n tane bagimsiz ozvektoru varsa:

$$A = X \Lambda X^{-1}$$

- X: ozvektorler (sutunlarda)
- Λ: ozdegerler (kosegen matris)

---

## Spectral Decomposition (Simetrik Matrisler Icin)

A **simetrik** ise, ozvektorler **ortogonal** secilir:

$$A = Q \Lambda Q^T$$

- Q: ortogonal matris (Q^T Q = QQ^T = I) → ozvektorler
- Λ: kosegen matris → ozdegerler

**Ortogonal matris** ne demek? Satirlari (ve sutunlari) birbirine dik ve birim uzunlukta.
Ters almak icin sadece transpose yeterli: $Q^{-1} = Q^T$ (hesap icin cok kolay!)

---

## Tekil Deger Ayrisimi (SVD)

**Herhangi** bir m×n matris A icin (simetrik olmak zorunda degil!):

$$A = U \Sigma V^T$$

- U: m×m ortogonal matris (sol tekil vektorler)
- Σ: m×n kosegen matris (tekil degerler, σ₁ ≥ σ₂ ≥ ... ≥ 0)
- V: n×n ortogonal matris (sag tekil vektorler)

**Tekil degerler =** A^T A'nin ozdegerlerinin karekokleri.

**Neden onemli?** SVD hemen hemen her yerde kullanilir: en kucuk kareler, boyut indirgeme, pseudo-inverse...

---

## LU Ayrisimi (LU Decomposition)

Ax = b lineer sistemi cozmek icin:

$$PA = LU$$

- P: permutasyon matrisi (satir degistirme)
- L: alt ucgensel matris (lower triangular)
- U: ust ucgensel matris (upper triangular)

**Cozum adim adim:**
1. PA = LU ayrisimini yap
2. Ly = Pb coz (ileri yerine koyma - kolay!)
3. Ux = y coz (geri yerine koyma - kolay!)

**Neden dogrudan A^(-1)b hesaplamiyoruz?** Ters matris hesaplamak cok pahali (O(n³)). LU ayrisimi da O(n³) ama daha verimli ve sayisal olarak daha kararli.

---

## Cholesky Ayrisimi

A **simetrik pozitif definit (SPD)** ise, LU'nun ozel hali:

$$P^T A P = L L^T$$

LU'ya gore **2 kat hizli** cunku simetriyi kullaniyor.

A SPD degilse **LBL ayrisimi** kullanilir:

$$P^T A P = L B L^T$$

B: 1×1 veya 2×2 bloklu kosegen matris.

---

## Alt Uzaylar ve QR Ayrisimi

### Null Uzayi (Null Space)
$$\text{Null}(A) = \{w \mid Aw = 0, w \neq 0\}$$
A'nin "yok ettigi" vektorler kumesi.

### Goruntu (Range)
$$\text{Range}(A) = \{w \mid w = Av, \forall v\}$$
A'nin "uretebilecegi" vektorler kumesi.

### Temel Teorem
$$\text{Null}(A) \oplus \text{Range}(A^T) = R^n$$

Yani R^n uzayi, Null(A) ve Range(A^T)'nin dogrudan toplamina esittir.

### QR Ayrisimi
$$AP = QR$$
- Q: ortogonal matris
- R: ust ucgensel matris
- P: permutasyon matrisi

En kucuk kareler problemlerinde cok kullanilir.

---

## Singularite ve Kosul Sayisi

### Singular (Tekil) Matris
A matrisi **tekil** (tersi yok) ise:
- En az bir ozdegeri 0
- En az bir tekil degeri 0
- Null uzayi bos degil
- det(A) = 0

### Kosul Sayisi (Condition Number)

$$\kappa(A) = \|A\| \cdot \|A^{-1}\|$$

- $\kappa(A)$ buyukse → A **kotukonumlanmis** (ill-conditioned)
- Kucuk hatalar bile sonucu cok degistirebilir
- $\kappa(A) = 1$ ideal (ortogonal matrisler)
- $\kappa(A) = \infty$ ise A tekil

---

## Sherman-Morrison-Woodbury Formulu

A'nin tersini biliyorsan ve A'ya **kucuk bir guncelleme** yaparsan, yeni tersi **hizlica** hesaplayabilirsin.

### Rank-1 Guncelleme
$\hat{A} = A + uv^T$ ise:

$$\hat{A}^{-1} = A^{-1} - \frac{A^{-1} u v^T A^{-1}}{1 + v^T A^{-1} u}$$

### Genel Durum
$\hat{A} = A + UV^T$ (U, V: n×p matris) ise:

$$\hat{A}^{-1} = A^{-1} - A^{-1} U (I + V^T A^{-1} U)^{-1} V^T A^{-1}$$

**Neden onemli?** Quasi-Newton optimizasyon yontemleri her adimda Hessian'a rank-1 veya rank-2 guncelleme yapar. Bu formul sayesinde her seferinde tersi sifirdan hesaplamaya gerek kalmaz!
