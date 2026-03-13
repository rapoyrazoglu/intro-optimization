# 2. Optimallik Kosullari

## Buyuk Soru

Elimde bir x* noktasi var. Bu noktanin **minimum** oldugunu nasil anlarim?

Cevap: **turev bilgisi**. Tek degiskende f'(x) = 0 ve f''(x) > 0 diye bakardik. Cok degiskende benzer seyler yapacagiz, ama matris versiyonlariyla.

---

## Taylor Teoremi — Her Seyin Temeli

Taylor teoremi, bir fonksiyonu **polinom** ile yaklastirmamizi saglar. Optimizasyondaki hemen hemen her sey Taylor acilimina dayanir.

### 1. Derece Taylor (Lineer Yaklasim)

$$f(x + p) \approx f(x) + \nabla f(x)^T p$$

"x noktasindayim, p kadar adim atarsam f ne olur?" sorusuna yaklasik cevap verir.

Geometrik anlam: Fonksiyonu **duz bir yuzey** (teget duzlem) ile yaklastiriyoruz.

### 2. Derece Taylor (Kuadratik Yaklasim)

$$f(x + p) \approx f(x) + \nabla f(x)^T p + \frac{1}{2} p^T \nabla^2 f(x) \, p$$

Bu sefer **egrilik** bilgisini de ekliyoruz. Duz yuzey yerine **kase seklinde** (paraboloid) bir yaklasim yapiyoruz.

- **∇f(x):** Gradient — egim bilgisi (1. turev)
- **∇²f(x):** Hessian — egrilik bilgisi (2. turev matrisi)
- **p:** Attigimiz adim

### Neden Onemli?

Optimizasyon algoritmalarinin cogu, fonksiyonu Taylor ile yaklastirip bu yaklasimi minimize eder:
- **Steepest descent:** 1. derece Taylor kullanir
- **Newton yontemi:** 2. derece Taylor kullanir

---

## Gerekli Kosullar (Necessary Conditions)

"Bu noktanin minimum olmasi icin **mutlaka** saglanmasi gereken seyler."

### 1. Derece Gerekli Kosul (FONC - First Order Necessary Condition)

> **Teorem 2.2:** x* lokal minimizer ve f surekli turevlenebilir ise:
> $$\nabla f(x^*) = 0$$

**Sezgisel anlam:** Minimum noktasinda egim sifir olmali. Eger herhangi bir yonde egim varsa, o yone dogru giderek f'yi daha da kucultebilirdik — yani orasi minimum olamaz.

**Dikkat:** Bu **gerekli** ama **yeterli** degil! ∇f = 0 olan noktalar minimum, maksimum veya eyer noktasi olabilir.

### 2. Derece Gerekli Kosul (SONC - Second Order Necessary Condition)

> **Teorem 2.3:** x* lokal minimizer, f iki kez surekli turevlenebilir ve ∇f(x*) = 0 ise:
> $$\nabla^2 f(x^*) \text{ pozitif semi-definit olmali}$$

Pozitif semi-definit ne demek? Her p yonu icin:

$$p^T \nabla^2 f(x^*) p \geq 0$$

**Sezgisel anlam:** Minimum noktasinda, **her yone** baktiginda egrilik yukariya dogru (veya duz) olmali. Eger herhangi bir yone baktiginda asagi egimli bir egrilik goruyorsan, orasi minimum degil.

**Tek degisken analojisi:** f''(x*) ≥ 0 olmali (asagi dogru bukum).

---

## Yeterli Kosullar (Sufficient Conditions)

"Bu kosullar saglaniyorsa, kesinlikle minimum."

### 2. Derece Yeterli Kosul (SOSC - Second Order Sufficient Condition)

> **Teorem 2.4:** ∇f(x*) = 0 **ve** ∇²f(x*) **pozitif definit** ise, x* kesinlikle **kati lokal minimizer**dir.

Pozitif definit ne demek? Her p ≠ 0 icin:

$$p^T \nabla^2 f(x^*) p > 0$$

(Semi-definitten farki: esitlik olmaz, kesinlikle buyuktur)

**Sezgisel anlam:** Her yone baktiginda egrilik **kesinlikle** yukariya dogru. Yani x*'in her tarafinda f degeri daha buyuk — gercekten bir "cukurun" dibindeyiz.

### Kosullar Tablosu

| Kontrol | Sonuc |
|---------|-------|
| ∇f(x*) ≠ 0 | Duragan nokta degil, minimum degil |
| ∇f(x*) = 0, ∇²f(x*) pozitif definit | **Kesinlikle lokal minimum** ✓ |
| ∇f(x*) = 0, ∇²f(x*) pozitif semi-definit | Minimum **olabilir** (emin degiliz) |
| ∇f(x*) = 0, ∇²f(x*) negatif definit | **Lokal maksimum** |
| ∇f(x*) = 0, ∇²f(x*) indefinit | **Eyer noktasi (saddle point)** |

---

## Dejenere Kritik Noktalar

Eger Hessian'in determinanti sifir ise (yani en az bir ozdegeri sifir), bu nokta **dejenere** (degenerate) noktadir.

Bu durumda 2. turev testi **kesin cevap veremez**. Daha yuksek dereceden turevlere bakmak gerekebilir.

**Ornek:** f(x,y) = x² + ay² + by⁴

Orijinde ∇f = 0 ve Hessian:
$$H = \begin{pmatrix} 2 & 0 \\ 0 & 6ay + 12by^2 \end{pmatrix}$$

Orijinde: H = [[2, 0], [0, 0]] — bir ozdeger sifir → dejenere.
Minimum olup olmadigi a ve b degerlerine baglidir.

---

## Konvekslik ve Optimallik

Konveks fonksiyonlarda isler muhtesem basitlesiyor:

### Teorem 2.5

> f konveks ise, her lokal minimizer ayni zamanda **global minimizer**dir.

**Ispat fikri:** Diyelim x* lokal ama global degil. O zaman baska bir z noktasi var ki f(z) < f(x*). Konvekslik geregi, x* ile z arasindaki her nokta da f(x*)'dan kucuk olmali. Ama bu, x*'in etrafinda daha iyi noktalar oldugu anlamina gelir — lokal minimum olamazdi. Celiskiye dustuk.

### Sonuc

> f konveks ve turevlenebilir ise, ∇f(x*) = 0 olan **her** x* **global minimumdur**.

Bu, konveks optimizasyonu cok guclendiren bir sonuc. Sadece gradientin sifir oldugu noktayi bul — o global minimumdur.

---

## Duz Olmayan (Nonsmooth) Problemler

Bazi fonksiyonlar her yerde turevlenebilir olmayabilir:

- **Kosede kirik:** f(x) = |x| gibi (x = 0'da turev yok)
- **Parcali fonksiyonlar:** Farkli bolgelerde farkli formul

Bu durumda gradient hesaplayamayiz. Bunun yerine:
- **Altgradient (subgradient):** Gradientin genellemesi
- **Genellestirilmis gradient:** Nonsmooth analiz araclari

Bu ders kapsaminda genellikle **duz (smooth)** fonksiyonlarla calisacagiz — yani 2. turev surekli olan fonksiyonlar.

---

## Ozet: Minimum Bulmak icin Yol Haritasi

```
1. ∇f(x*) = 0 coz → duragan noktalari bul
2. Her duragan noktada ∇²f(x*) hesapla
3. Hessian'in ozdegerlerine bak:
   - Hepsi > 0 → Pozitif definit → LOKAL MINIMUM ✓
   - Hepsi < 0 → Negatif definit → Lokal maksimum
   - Karisik isaret → Indefinit → Eyer noktasi
   - Bazi sifir → Dejenere → Karar verilemez
4. Konveks ise: lokal minimum = global minimum
```
