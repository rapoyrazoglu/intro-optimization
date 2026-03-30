# Trust Region Temel Formulasyonu

## Kuadratik Model: Kalbin Detaylari

Trust Region yonteminde her iterasyonda gercek fonksiyonumuzu bir **kuadratik modelle** yaklasik olarak temsil ediyoruz. Bu modeli tekrar yazalim ve her parcasini derinlemesine inceleyelim:

$$m_k(p) = f_k + g_k^T p + \frac{1}{2} p^T B_k p$$

### Formuldeki Her Terimin Fiziksel Anlami

**1. Sabit terim: f_k = f(x_k)**

Bu, "su an neredeyiz?" sorusunun cevabi. Mevcut noktamizdaki fonksiyon degeri. Ornegin f(x_k) = 141 ise, optimizasyona baslarken fonksiyonumuzun degeri 141.

**2. Lineer terim: g_k^T p**

$$g_k^T p = \nabla f(x_k)^T p = \begin{pmatrix} \frac{\partial f}{\partial x_1} \\ \frac{\partial f}{\partial x_2} \\ \vdots \end{pmatrix}^T \begin{pmatrix} p_1 \\ p_2 \\ \vdots \end{pmatrix} = \frac{\partial f}{\partial x_1} p_1 + \frac{\partial f}{\partial x_2} p_2 + \cdots$$

Bu terim fonksiyonun **birinci dereceden degisimini** temsil eder. "p yonunde kucuk bir adim atarsam, fonksiyon yaklasik olarak ne kadar degisir?"

- Eger g_k^T p < 0 ise: Bu yonde ilerlemek fonksiyonu **azaltir** (iyi!)
- Eger g_k^T p > 0 ise: Bu yonde ilerlemek fonksiyonu **arttirir** (kotu!)

**3. Kuadratik terim: (1/2) p^T B_k p**

$$\frac{1}{2} p^T B_k p = \frac{1}{2} \begin{pmatrix} p_1 & p_2 \end{pmatrix} \begin{pmatrix} b_{11} & b_{12} \\ b_{21} & b_{22} \end{pmatrix} \begin{pmatrix} p_1 \\ p_2 \end{pmatrix}$$

Bu terim fonksiyonun **egriligini** (ikinci derece davranisini) yakalar. Bir vadide yuruyorsun diyelim:
- Egrilik buyukse: Vadi dar ve dik — fonksiyon hizla degisir
- Egrilik kucukse: Vadi genis ve yayvan — fonksiyon yavas degisir

B_k genelde **Hessian matrisi** nabla^2 f(x_k) veya onun bir yaklasimi olur.

---

## Trust Region Alt Problemi (Detayli)

$$\min_{p \in \mathbb{R}^n} \quad m_k(p) = f_k + g_k^T p + \frac{1}{2} p^T B_k p$$
$$\text{kosul:} \quad \|p\| \leq \Delta_k$$

### Bu Formulun Her Parcasi

**Sol taraf — Amac:**
- "p vektorunu oyle sec ki m_k(p) en kucuk olsun."
- Yani kuadratik modeli minimize edecek en iyi adimi bul.

**Sag taraf — Kisit:**
- ||p|| vektorun **Oklid normu** (uzunlugu): ||p|| = sqrt(p_1^2 + p_2^2 + ... + p_n^2)
- Delta_k **guven bolgesi yaricapi**: Ne kadar uzaga gidebilecegimizin siniri
- ||p|| <= Delta_k: "Adimin uzunlugu yaricapi asamaz" — yani merkezi x_k olan Delta_k yaricapli topun icinde kal

### Onemli Gozlem: Bu Kisitli Bir Optimizasyon Problemidir

Line Search'ta "bir dogrultuda en iyi noktayi bul" diyorduk — bu 1 boyutlu bir problemdi.

Trust Region'da ise "bir kure icinde en iyi noktayi bul" diyoruz — bu n boyutlu, **kisitli** bir problem. Cozumu daha karmasik ama daha guclü.

---

## Kisit Aktif mi, Pasif mi?

Cozum p* bulundugunda iki durum olabilir:

### Durum 1: Kisit Pasif (||p*|| < Delta_k)

Cozum kurenin **icinde** kaldi. Bu, sanki kisit yokmus gibi serbest minimizasyonun cozumu zaten kurenin icindeydi demek.

- Bu durumda cozum **kisitsiz Newton adimina** esittir: p* = -B^(-1) g
- Model fonksiyonun minimumu zaten guven bolgesinin icinde

**Sezgisel anlam:** "Modelimiz diyor ki en iyi nokta yakin — guven bolgesinin disina cikmaya gerek yok."

### Durum 2: Kisit Aktif (||p*|| = Delta_k)

Cozum tam kurenin **sinirinda**. Bu, serbest cozumun kurenin disinda kalacagi anlamina gelir; kisit bizi geriye cekiyor.

- Newton adimi cok buyuk oldugu icin "budandi"
- Adimimiz guven bolgesinin sinirina yapisti

**Sezgisel anlam:** "Model daha uzaga gitmemizi istiyor ama biz o kadar uzaga guvenemiyoruz. Bolge sinirina kadar gidiyoruz."

---

## Degerlendirme Fonksiyonu: rho_k

Bir adim attiktan sonra, modelin gercek fonksiyonu ne kadar iyi temsil ettigini olcmemiz gerekir. Bunun icin **degerlendirme orani** rho_k kullanilir:

$$\rho_k = \frac{f(x_k) - f(x_k + p_k)}{m_k(0) - m_k(p_k)}$$

### Bu Formulun Parcalari

**Pay (ust kisim): f(x_k) - f(x_k + p_k) = Gercek Azalma**

- f(x_k): Eski noktadaki gercek fonksiyon degeri
- f(x_k + p_k): Yeni noktadaki gercek fonksiyon degeri
- Farklari: p_k adimini attiktan sonra fonksiyon **gercekte** ne kadar azaldi?
- Pozitifse: Fonksiyon gercekten azaldi (iyi!)
- Negatifse: Fonksiyon artti (kotu — model bizi yaniltti!)

**Payda (alt kisim): m_k(0) - m_k(p_k) = Tahmin Edilen Azalma**

- m_k(0): Model fonksiyonun p=0'daki degeri = f_k (yani simdiki deger)
- m_k(p_k): Model fonksiyonun p_k adimindaki degeri
- Farklari: Modele gore fonksiyon ne kadar azalmali**ydi**?
- Bu her zaman >= 0 olur (cunku p_k modeli minimize etmek icin secilmisti)

**Oran: rho_k = Gercek Azalma / Tahmin Edilen Azalma**

| rho_k Degeri | Anlami | Yorum |
|-------------|---------|-------|
| **rho_k ≈ 1** | Gercek azalma ≈ Tahmin edilen azalma | Model cok iyi! Guven bolgesi buyutulmeli |
| **rho_k > 0 ama kucuk** | Gercek azalma var ama tahminden az | Model idare eder, bolge kucultulebilir |
| **rho_k < 0** | Fonksiyon artti! | Model cok kotu — adimi reddet, bolgeyi daralt |
| **rho_k > 0.75** | Gercek azalma tahminin %75'inden fazla | Cok iyi — bolgeyi buyutebiliriz |
| **rho_k < 0.25** | Gercek azalma tahminin %25'inden az | Kotu — bolgeyi kucultelim |

---

## Guven Bolgesi Yaricapinin Guncellenmesi

rho_k degerine gore Delta_k su sekilde guncellenir:

### Eger rho_k < 1/4 (Kotu Adim)

$$\Delta_{k+1} = \frac{1}{4} \Delta_k$$

Model kotu tahmin etti — bolgeyi **dort kat kuculT**. Modele daha az guven, daha kucuk adimlar at.

### Eger rho_k > 3/4 VE ||p_k|| = Delta_k (Cok Iyi Adim + Sinirda)

$$\Delta_{k+1} = \min(2\Delta_k, \hat{\Delta})$$

Model iyi tahmin etti ve biz sinira dayanmistik — bolgeyi **iki katina cikar** (ama maksimum yaricap Delta_hat'i gecme).

### Diger Durumlar

$$\Delta_{k+1} = \Delta_k$$

Orta hallerde bolgeyi oldugu gibi birak.

---

## Adimi Kabul Etme veya Reddetme

rho_k degerine gore adimin kendisi de kabul veya reddedilir:

### Eger rho_k > eta (tipik olarak eta = 1/4 veya daha kucuk)

$$x_{k+1} = x_k + p_k \quad \text{(adimi kabul et)}$$

Yeterli ilerleme var — yeni noktaya git.

### Eger rho_k <= eta

$$x_{k+1} = x_k \quad \text{(adimi reddet)}$$

Yeterli ilerleme yok — yerinde kal, ama bolgeyi kucultup tekrar dene.

**Onemli:** Adim reddedilse bile bolge kucultulur ve bir sonraki iterasyonda yeni (daha kucuk) bir adim hesaplanir. Algoritma takılip kalmaz.

---

## Trust Region Algoritmasinin Tam Akisi (Algorithm 4.1)

**Girdi:** Delta_hat > 0 (maksimum yaricap), Delta_0 in (0, Delta_hat) (baslangic yaricapi), eta in [0, 1/4) (kabul esigi)

**Her k = 0, 1, 2, ... icin:**

1. **Alt problemi coz:** ||p|| <= Delta_k kisiti altinda m_k(p)'yi (yaklasik olarak) minimize ederek p_k'yi bul.

2. **Degerlendirme oranini hesapla:**
   $$\rho_k = \frac{f(x_k) - f(x_k + p_k)}{m_k(0) - m_k(p_k)}$$

3. **Yaricapi guncelle:**
   - Eger rho_k < 1/4: Delta_{k+1} = (1/4) Delta_k
   - Eger rho_k > 3/4 ve ||p_k|| = Delta_k: Delta_{k+1} = min(2 Delta_k, Delta_hat)
   - Diger durumda: Delta_{k+1} = Delta_k

4. **Noktayi guncelle:**
   - Eger rho_k > eta: x_{k+1} = x_k + p_k (kabul)
   - Yoksa: x_{k+1} = x_k (red)

---

## Olcekleme (Scaling) Problemi

Bazi fonksiyonlar **kotu olceklenmiS** olabilir. Ornegin:

$$f(x, y) = 10^9 x^2 + y^2$$

Bu fonksiyonda x yonundeki degisim y yonundekinden milyar kat daha hassas. Daire seklindeki bir guven bolgesi bu durumda iyi calismaz — x yonunde cok kucuk, y yonunde cok buyuk adimlar gerekir.

### Cozum 1: Degiskenleri Yeniden Olcekle

Eger cozumun olcegini biliyorsak, degiskenleri donusturebiliriz.

### Cozum 2: Eliptik Guven Bolgesi

Daire yerine **elips** seklinde bir guven bolgesi kullan:

$$\min_{\|Dp\| \leq \Delta_k} m_k(p) = f_k + g_k^T p + \frac{1}{2} p^T B_k p$$

Burada D bir **diyagonal matris** — her degisken icin farkli bir olcek faktoru uygular.

Bu sayede bazi yonlerde daha buyuk, bazi yonlerde daha kucuk adimlar atilebilir.

---

## Ozet Tablosu

| Kavram | Formul | Anlami |
|--------|--------|--------|
| Model | m_k(p) = f_k + g_k^T p + (1/2) p^T B_k p | Gercek fonksiyonun kuadratik yaklasimi |
| Alt problem | min m_k(p), ||p|| <= Delta_k | Guven bolgesi icinde modeli minimize et |
| Degerlendirme | rho_k = (gercek azalma) / (tahmin edilen azalma) | Modelin kalitesini olc |
| Yaricap guncelle | rho_k'ya gore buyut/kucult/koru | Modele olan guveni ayarla |
| Adim kabul | rho_k > eta ise x_{k+1} = x_k + p_k | Yeterli ilerleme varsa ilerle |
