# 2. Konveks Kavramlar (Affine, Cone, Convex)

## Kombinasyonlar - Neden Onemli?

Optimizasyonda "cozum uzayinin sekli" cok onemli. Eger cozum uzayin konveks ise,
isimiz cok kolaylasiyor cunku lokal minimum = global minimum olur.

Oncelikle **kombinasyon** kavramindan baslayalim.

---

## Lineer Kombinasyon

Elimizde vektorler var: x₁, x₂, ..., xₚ (bunlar R^n'de noktalar)

$$x = \lambda_1 x_1 + \lambda_2 x_2 + \cdots + \lambda_p x_p$$

Katsayilar ($\lambda_i$) herhangi bir reel sayi olabilir: pozitif, negatif, sifir...

**Ornek (2D'de):** x₁ = (1, 0), x₂ = (0, 1)
- 3x₁ + 2x₂ = (3, 2) ✓ lineer kombinasyon
- -x₁ + 5x₂ = (-1, 5) ✓ lineer kombinasyon
- Sonuc: Tum R² duzlemini kapsarsin

---

## Affine Kombinasyon

Lineer kombinasyonla ayni, AMA katsayilarin toplami 1 olmali:

$$\sum_{i=1}^{p} \lambda_i = 1$$

**Ornek:** x₁ = (1, 0), x₂ = (0, 1)
- 0.5·x₁ + 0.5·x₂ = (0.5, 0.5) ✓ (0.5 + 0.5 = 1)
- 2·x₁ + (-1)·x₂ = (2, -1) ✓ (2 + (-1) = 1)
- 3·x₁ + 2·x₂ = (3, 2) ✗ (3 + 2 = 5 ≠ 1)

**Geometrik anlami:** Iki nokta arasindaki **dogru** (ve onun uzantisi). Yani iki noktadan gecen sonsuz dogru.

---

## Konik (Conical) Kombinasyon

Katsayilar **negatif olamaz:**

$$\lambda_i \geq 0$$

**Ornek:** x₁ = (1, 0), x₂ = (0, 1)
- 3·x₁ + 2·x₂ = (3, 2) ✓ (ikisi de >= 0)
- -1·x₁ + 5·x₂ = (-1, 5) ✗ (-1 < 0)

**Geometrik anlami:** Orijinden baslayan bir **koni** (uc) seklinde bolge.

---

## Konveks (Convex) Kombinasyon

**Hem** katsayilarin toplami 1, **hem** hepsi >= 0:

$$\sum_{i=1}^{p} \lambda_i = 1 \quad \text{ve} \quad \lambda_i \geq 0$$

**Ornek:** x₁ = (1, 0), x₂ = (0, 1)
- 0.3·x₁ + 0.7·x₂ = (0.3, 0.7) ✓
- 0.5·x₁ + 0.5·x₂ = (0.5, 0.5) ✓ (tam orta nokta)
- 2·x₁ + (-1)·x₂ ✗ (-1 < 0)

**Geometrik anlami:** Iki nokta arasindaki **dogu parcasi**. Uc nokta icin ucu birlestiren **ucgen**.

---

## Ozet Tablosu

| Kombinasyon | Kosul | Geometrik Anlam |
|---|---|---|
| Lineer | yok | Tum uzay |
| Affine | Σλᵢ = 1 | Noktalardan gecen dogru/duzlem |
| Konik | λᵢ ≥ 0 | Orijinden koni |
| Konveks | Σλᵢ = 1 ve λᵢ ≥ 0 | Noktalarin icindeki bolge |

---

## Konveks Fonksiyon

Bir fonksiyon f **konveks** ise, herhangi iki noktasi arasina cizdigin dogru,
fonksiyonun **ustunde** kalir:

$$f(\alpha x + (1-\alpha)y) \leq \alpha f(x) + (1-\alpha)f(y) \quad \forall \alpha \in [0,1]$$

**Basitce:** Cukur seklinde (U harfi gibi). Herhangi iki noktayi birlesitren dogru, egrinin altina dusmez.

**Ornekler:**
- f(x) = x² → konveks ✓ (parabol yukari bakiyor)
- f(x) = |x| → konveks ✓ (V seklinde)
- f(x) = eˣ → konveks ✓
- f(x) = -x² → konveks degil, **konkav** (tepe noktasi var)

**Konkav fonksiyon:** -f konveks ise f konkavdir. (Tepe seklinde, ters U)

**Neden onemli?** Konveks fonksiyonun minimumunu bulursan, o **kesinlikle global minimumdur**. Baska bir yerde daha kucuk deger yoktur!
