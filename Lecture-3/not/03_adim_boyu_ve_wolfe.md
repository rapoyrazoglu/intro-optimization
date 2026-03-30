# 3. Adim Boyu Secimi ve Wolfe Kosullari

## Buyuk Soru

Yonu sectik (p_k). Simdi soru su: **o yonde ne kadar yuruyecegiz?**

Matematiksel olarak, su tek degiskenli problemi cozuyoruz:

**min_{a>0} phi(a) = f(x_k + a * p_k)**

Bu formulde:

| Sembol | Anlami |
|--------|--------|
| **a** (alfa) | Adim boyu. Ne kadar yuruyecegimizi belirleyen pozitif sayi. |
| **phi(a)** | "a kadar yurursem f ne olur?" fonksiyonu. Orijinal cok degiskenli f'yi, tek degiskenli bir fonksiyona ceviriyoruz. |
| **x_k** | Su anki nokta |
| **p_k** | Secilen arama yonu |
| **x_k + a * p_k** | a kadar yurudukten sonra varacagimiz nokta |

---

## Exact Line Search (Tam Arama)

phi(a)'nin **tam minimumunu** bul. Yani:

**phi'(a) = 0 coz**

Bu, grad f(x_k + a * p_k)^T * p_k = 0 demek.

- **Kuadratik fonksiyonlarda** kapali formul var (Lecture 2'de gorduk)
- **Genel fonksiyonlarda** bunu cozmek pahali ve zor

---

## Inexact Line Search (Yaklasik Arama)

Pratikte tam minimumu bulmak yerine, **"yeterince iyi" bir alfa** seciyoruz. Ama "yeterince iyi" ne demek? Bunu tanimlamak icin **kosullar** koyuyoruz.

Iki ana kosul ailesi var:
1. **Wolfe kosullari** (en yaygin)
2. **Goldstein kosullari** (daha az yaygin)

---

## Goldstein Kosullari

0 < c < 1/2 icin:

**f(x_k) + (1-c) * a * grad f_k^T * p_k  <=  f(x_k + a * p_k)  <=  f(x_k) + c * a * grad f_k^T * p_k**

Bu bir **sandvic**: fonksiyon degeri iki sinirin arasinda olmali.

- **Sag taraf (ust sinir):** Fonksiyon yeterince dusmeli
- **Sol taraf (alt sinir):** Fonksiyon cok fazla dusmemeli (minimum'u atlamamali)

Goldstein kosullari Newton-tipi yontemler icin uygun, ama quasi-Newton yontemleri icin iyi degildir. Bu yuzden pratikte daha cok Wolfe kosullari tercih edilir.

**Not:** Bu yontem derste detayli islenmemistir.

---

## Wolfe Kosullari — Detayli Aciklama

Wolfe kosullari iki parcadan olusur: **Sufficient Decrease (Yeterli Azalma)** ve **Curvature Condition (Egrilik Kosulu)**.

---

### Kosul 1: Sufficient Decrease (Armijo Kosulu)

**f(x_k + a * p_k)  <=  f(x_k) + c_1 * a * grad f(x_k)^T * p_k**

Bu formul ilk bakista korkutucu gorunuyor ama aslinda cok basit bir sey soylyor. **Adim adim parcalayalim:**

#### Sol Taraf: f(x_k + a * p_k)

"Alfa kadar yurudukten sonra fonksiyonun degeri."

Yani adimi attin, yeni noktayi hesapladin, fonksiyona koydun, degere baktin.

#### Sag Taraf: f(x_k) + c_1 * a * grad f(x_k)^T * p_k

Bu kisim birkac parcadan olusuyor:

| Parca | Anlami |
|-------|--------|
| **f(x_k)** | Adim atmadan onceki fonksiyon degeri. "Simdi neredeyim?" |
| **grad f(x_k)^T * p_k** | Yonlu turev (directional derivative). Fonksiyonun p_k yonundeki degisim hizi. Inis yonu sectiysek bu **negatif** bir sayi. |
| **a * grad f(x_k)^T * p_k** | "a kadar yurursen, lineer model sana ne kadar dusus vaat ediyor?" Negatif bir sayi cunku inis yonundeyiz. |
| **c_1** | 0 ile 1 arasinda bir sabit (genellikle c_1 = 10^{-4}). "Lineer modelin vaat ettigi dususun ne kadarina raziyim?" Kucuk bir sayi secersen, az bir dusus bile kabul. |
| **c_1 * a * grad f(x_k)^T * p_k** | Vaat edilen dususun c_1 kati. c_1 = 10^{-4} ise, vaat edilen dususun binde biri bile yeterli. |

#### Bu Esitsizlik Ne Diyor?

"Adim attiktan sonra fonksiyonun degeri, **lineer modelin ongordugunun en az c_1 kati kadar** dusmeli."

Baska bir deyisle: "En azindan **biraz** dusus olsun, tamamen bos bir adim atma."

#### Somut Ornek

f(2, 3) = 10, grad f^T * p = -32, c_1 = 0.5 olsun.

alfa = 0.25 icin:
- Sol taraf: f(yeni nokta) = 8 diyelim
- Sag taraf: 10 + 0.5 * 0.25 * (-32) = 10 - 4 = 6

8 <= 6 mi? **Hayir!** Armijo saglanmiyor — bu alfa cok buyuk veya yon kotu.

alfa = 0.1 icin:
- Sol taraf: f(yeni nokta) = 7 diyelim
- Sag taraf: 10 + 0.5 * 0.1 * (-32) = 10 - 1.6 = 8.4

7 <= 8.4 mi? **Evet!** Armijo saglaniyor.

#### c_1 Neden Kucuk Secilir?

c_1 = 10^{-4} gibi kucuk bir deger, neredeyse her adimi kabul eder. Amac sadece "fonksiyon en azindan biraz dussun" garantisi. Asil isi curvature kosulu yapar.

---

### Kosul 2: Curvature Condition (Egrilik Kosulu)

**grad f(x_k + a * p_k)^T * p_k  >=  c_2 * grad f(x_k)^T * p_k**

Bu kosul biraz daha incelikli. **Parcalayalim:**

#### Sol Taraf: grad f(x_k + a * p_k)^T * p_k

"Yeni noktadaki yonlu turev." Yani alfa kadar yurudukten sonra, p_k yonundeki egim ne?

- Eger bu deger **cok negatif** ise: "Hala cok dik bir inis var, daha fazla yuruyebilirdim." → Adim cok kisa.
- Eger bu deger **sifira yakin** ise: "Duzluge geldim, tam dogru yerdeyim."
- Eger bu deger **pozitif** ise: "Artik yukari cikiyorum, biraz gectim ama sorun degil."

#### Sag Taraf: c_2 * grad f(x_k)^T * p_k

"Baslangictaki yonlu turevin c_2 kati."

Baslangicta grad f(x_k)^T * p_k negatif bir sayi (inis yonundeyiz). c_2 ile carpinca hala negatif ama **daha az negatif** (cunku 0 < c_2 < 1).

#### Bu Esitsizlik Ne Diyor?

"Yeni noktadaki egim, baslangictaki egimin c_2 kati kadar **daha az dik** (veya daha fazla) olmali."

Baska bir deyisle: **"Cok kisa adim atma!"**

Eger cok kisa adim atarsan, yeni noktadaki egim hala baslangictaki kadar dik olur. Bu kosul, "biraz ilerleme kaydet" diyor.

#### c_2 Degerleri

| Yontem | c_2 | Neden? |
|--------|-----|--------|
| **Newton** | 0.9 | Genis kabul araligi — Newton yonu zaten iyi, fazla kisitlamaya gerek yok |
| **Conjugate Gradient** | 0.1 | Dar kabul araligi — hassas adim boyu gerekiyor |

#### Somut Ornek

Baslangicta: grad f(x_0)^T * p = -32, c_2 = 0.1

Curvature kosulu: yeni noktadaki yonlu turev >= 0.1 * (-32) = -3.2

- Yeni noktada yonlu turev = -20 ise: -20 >= -3.2? **Hayir!** Hala cok dik, adim cok kisa.
- Yeni noktada yonlu turev = -2 ise: -2 >= -3.2? **Evet!** Yeterince ilerlemisiz.
- Yeni noktada yonlu turev = 5 ise: 5 >= -3.2? **Evet!** Biraz gecmisiz ama sorun degil.

---

### Iki Kosul Birlikte

**Armijo:** "Fonksiyon yeterince dustu mu?" → Cok buyuk adim atmayi onler.

**Curvature:** "Yeterince ileri gittim mi?" → Cok kucuk adim atmayi onler.

Ikisi birlikte, alfa icin bir **aralik** tanimlar:

```
|-------|=====================|--------|
0    cok kisa              tam iyi         cok uzun
     (curvature red)       (ikisi de ok)   (armijo red)
```

---

## Strong Wolfe Kosullari

Normal curvature kosulu pozitif yonlu turevleri de kabul eder (yani biraz gecmen sorun degil). **Strong Wolfe**, bunu da kisitlar:

**|grad f(x_k + a * p_k)^T * p_k|  <=  c_2 * |grad f(x_k)^T * p_k|**

Fark: mutlak deger eklendi. Artik yonlu turevin buyuklugu sinirli — ne cok negatif ne cok pozitif olabilir.

Bu ne ise yarar? Lokal minimum'a daha yakin bir alfa secilmesini zorlar.

| | Wolfe | Strong Wolfe |
|--|-------|-------------|
| Curvature | grad f^T p >= c_2 * grad f_0^T p | \|grad f^T p\| <= c_2 * \|grad f_0^T p\| |
| Kabul ettigi alan | Tek tarafli (asagi sinir) | Iki tarafli (dar aralik) |
| Ne zaman? | Genel kullanim | Hassas adim boyu gerekince |

---

## Backtracking Line Search (Geri Adim Yontemi)

Pratikte en basit ve en yaygin inexact line search yontemi. Sadece **Armijo kosulunu** kullanir (curvature kontrol etmez).

### Algoritma 3.1

```
Girdi: alfa_hat > 0 (baslangic adim boyu)
       rho ∈ (0, 1)   (kucultme orani, mesela 0.5 veya 0.2)
       c ∈ (0, 1)      (Armijo sabiti, mesela 10^{-4})

alfa = alfa_hat

Tekrarla:
    Eger f(x_k + alfa * p_k) <= f(x_k) + c * alfa * grad f_k^T * p_k ise:
        DUR → alfa'yi kabul et
    Degilse:
        alfa = rho * alfa   (alfa'yi kucult)
```

### Sezgisel Anlam

1. Buyuk bir adimla basla (alfa_hat)
2. Armijo kosulunu kontrol et
3. Saglamiyorsa → adimi kuculterek (rho ile carparak) tekrar dene
4. Saglayincaya kadar devam et

### Neden Calisiyor?

Alfa sifira yaklastikca, Armijo kosulu **kesinlikle saglanir** (Taylor acilimi nedeniyle). Yani algoritma sonunda duracak.

### Parametre Secimleri

| Parametre | Tipik Deger | Anlami |
|-----------|-------------|--------|
| **alfa_hat** | 1 (Newton icin) | Baslangic adim boyu. Newton icin 1 dogal secim cunku Newton adimi kendisi tam adim. |
| **rho** | 0.5 veya 0.2 | Her basarisiz denemede alfa'yi ne kadar kucultuyorsun. 0.5 = yarilama. |
| **c** | 10^{-4} | Armijo sabiti. Kucuk = kolay kabul. |
