# 1. Line Search Yontemlerine Giris

## Bu Ders Neyi Kapsiyor?

Lecture 2'de iki ana stratejiden bahsetmistik: **Line Search** ve **Trust Region**. Bu derste line search yontemlerinin **pratik detaylarina** daliyoruz:

- Newton yonu calismayinca ne yapilir? (Modifiye Newton)
- Adim boyunu nasil seceriz? (Wolfe kosullari, backtracking)
- Algoritmanin yakinsakligini nasil garanti ederiz?

---

## Line Search Yonteminin Hatirlatmasi

Her iterasyonda iki sey belirliyoruz:

**yeni nokta = eski nokta + adim boyu x yon**

Matematik ile yazarsak:

**x_{k+1} = x_k + a_k * p_k**

Bu formulde ne var ne yok, tek tek aciklayalim:

| Sembol | Anlami | Detay |
|--------|--------|-------|
| **x_k** | Su anki nokta | k. iterasyondaki konumun. Ornegin (2, 3) gibi bir vektor. |
| **x_{k+1}** | Bir sonraki nokta | Adim attiktan sonra varacagin yer. |
| **p_k** | Arama yonu | "Hangi yone yuruyecegim?" sorusunun cevabi. Bir vektor. |
| **a_k** (alfa) | Adim boyu | "Bu yonde ne kadar yuruyecegim?" sorusunun cevabi. Pozitif bir sayi. |

---

## Inis Yonu (Descent Direction) Nedir?

Sectigin yon **inis yonu** olmak zorunda. Yani o yone dogru yuruyunce fonksiyon degeri **dusmeli**.

Bunu matematiksel olarak soyle kontrol ediyoruz:

**grad f(x_k)^T * p_k < 0**

Bu ifadeyi parcalayalim:

| Parca | Anlami |
|-------|--------|
| **grad f(x_k)** | x_k noktasindaki gradyan vektoru. Fonksiyonun en cok **arttigi** yonu gosteriyor. |
| **p_k** | Sectigimiz arama yonu. |
| **grad f(x_k)^T * p_k** | Bu ikisinin **ic carpimi** (dot product). Iki vektorun ne kadar ayni yone baktigini olcer. |
| **< 0** | Ic carpim negatif demek gradyan ile yon **birbirine zit** taraflara bakiyor. Gradyan yukari gosteriyorsa, biz asagi gidiyoruz. |

### Sezgisel Anlam

Bir tepede duruyorsun. Gradyan sana "en dik cikis bu tarafa" diyor. Sen onun **tersine** yuruyorsun — yani asagi iniyorsun. Ic carpim negatif cikiyorsa, gercekten asagi dogru yuruyorsun demektir.

### Neden Bu Kosul Gerekli?

Taylor acilimindan:

**f(x_k + a * p_k) ≈ f(x_k) + a * grad f(x_k)^T * p_k**

Eger `grad f(x_k)^T * p_k < 0` ise, `a` kucuk pozitif bir sayi oldugunda toplam **azalir**. Yani bir adim atinca fonksiyon degeri duser.

Eger `grad f(x_k)^T * p_k > 0` olsaydi, adim atinca fonksiyon **artardi** — yanlis tarafa gitmis olurduk.

---

## Yon Secenekleri Hatirlatmasi

| Yontem | Yon (p_k) | Ne Kullanir |
|--------|-----------|-------------|
| **Steepest Descent** | p_k = -grad f(x_k) | Sadece gradyan (1. turev) |
| **Newton** | p_k = -H^{-1} * grad f(x_k) | Gradyan + Hessian (1. ve 2. turev) |
| **Quasi-Newton (BFGS)** | p_k = -B^{-1} * grad f(x_k) | Gradyan + yaklasik Hessian |

Burada **H** = Hessian matrisi (2. turev matrisi), **B** = Hessian'in yaklasimi.

---

## Newton Yonu Hatirlatmasi

Newton yonteminde arama yonu:

**p_k = -H_k^{-1} * g_k**

Bu formulde:

| Sembol | Anlami |
|--------|--------|
| **H_k** | ∇²f(x_k), yani x_k noktasindaki Hessian matrisi. Fonksiyonun egriligini (2. turev bilgisini) tasiyor. |
| **g_k** | ∇f(x_k), yani x_k noktasindaki gradyan vektoru. |
| **H_k^{-1}** | Hessian'in tersi. |
| **-H_k^{-1} * g_k** | "Egrilik bilgisini kullanarak en iyi adresi hesapla" demek. |

### Newton Yonu Neden Inis Yonu?

Eger H_k **pozitif definit** ise (yani tum ozdegerleri pozitif ise):

**grad f(x_k)^T * p_k = -g_k^T * H_k^{-1} * g_k < 0**

Bu neden negatif? Cunku H_k pozitif definit oldugunda, tersi de pozitif definit. Herhangi bir v vektoru icin v^T * (pozitif definit matris) * v > 0 olur. Dolayisiyla g_k^T * H_k^{-1} * g_k > 0, basi eksi olunca negatif.

### Sorun Ne Zaman Cikar?

Eger Hessian **pozitif definit degilse** (indefinit, tekil, veya negatif ozdegerleri varsa):
- Newton yonu **inis yonu olmayabilir**
- Hessian'in tersi **mevcut olmayabilir** (tekil matris)

Iste bu durumda **Modifiye Newton** yontemlerine ihtiyacimiz var. Bunu bir sonraki notta gorecegiz.
