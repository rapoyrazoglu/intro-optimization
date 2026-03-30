# Yaklasik Cozum Yontemleri

## Neden Yaklasik Cozum?

Trust region alt problemini **tam olarak** cozmek (yani optimality kosullarini saglayan lambda'yi kesin olarak bulmak) genelde zordur:

- phi(lambda) = ||-(B+lambda I)^(-1) g|| - Delta = 0 denklemini cozmek gerekir
- Bu, her adimda bir dogrusal denklem sistemi cozmeyi ve iteratif bir arama yapmayi gerektirir
- Degisken sayisi az oldugunda mumkun, ama buyuk problemlerde cok pahali

Ustelik model m_k zaten gercek fonksiyon f'nin sadece bir **yaklasimi**. Bu yaklasimi tam olarak cozmeye gerek var mi? Cogu zaman **yaklasik bir cozum** yeterli olur.

### Dort Yaklasik Yontem

1. **Cauchy Noktasi** — En basit, ama en yavas
2. **Dogleg Yontemi** — Cauchy ile Newton'u birlestir
3. **2 Boyutlu Alt-uzay Minimizasyonu** — Daha sofistike
4. **Steihaug Algoritmasi** — En genel (buyuk problemler icin)

---

## 1. Cauchy Noktasi

### Temel Fikir

Cauchy noktasi, en basit yaklasik cozumdur. Fikir su:

1. **Yon olarak steepest descent (en dik inis) yonunu sec**: -g_k
2. **Bu yon uzerinde, guven bolgesi icinde en iyi noktayi bul**

Yani n boyutlu bir optimizasyon problemini **1 boyutlu bir probleme** indirgemis oluyoruz.

### Formul

Cauchy noktasi p_k^C su sekilde hesaplanir:

**Adim 1:** Steepest descent yonundeki birim vektoru bul ve olcekle:

$$p_k^S = -\frac{\Delta_k}{\|g_k\|} g_k$$

**Bu ne demek?**
- -g_k: Negatif gradyan yonu (en dik inis)
- g_k / ||g_k||: Birim vektor (yonu koruyor, uzunlugu 1 yapiyoruz)
- Delta_k / ||g_k||: Uzunlugu tam Delta_k yapiyoruz
- Sonuc: Guven bolgesi sinirinda, steepest descent yonundeki nokta

**Adim 2:** Bu yon uzerinde modeli minimize eden olcek faktorunu bul:

$$\tau_k = \underset{0 \leq \tau \leq 1}{\arg\min} \; m_k(\tau \, p_k^S)$$

tau = 0'dan (merkezde kal) tau = 1'e (sinira git) kadar model fonksiyonunu minimize eden tau'yu sec.

**Adim 3:** Cauchy noktasi:

$$p_k^C = \tau_k \, p_k^S$$

### tau_k'nin Hesaplanmasi

m_k(tau p_k^S) ifadesi tau'nun **kuadratik** bir fonksiyonudur. Iki durum var:

**Durum 1: g_k^T B_k g_k <= 0 (negatif veya sifir egrilik)**

$$\tau_k = 1$$

Gradyan yonunde egrilik negatif veya sifir — model bu yonde surekli azaliyor. Sinira kadar git!

**Neden?** Eger g_k^T B_k g_k <= 0 ise, kuadratik terim bu yonde fonksiyonu artirmiyor (hatta azaltiyor). Dolayisiyla en iyi strateji mumkun oldugunca uzaga gitmek.

**Durum 2: g_k^T B_k g_k > 0 (pozitif egrilik)**

$$\tau_k = \min\left(\frac{\|g_k\|^3}{\Delta_k \, g_k^T B_k g_k}, \; 1\right)$$

Pozitif egrilik var — model bu yonde bir minimuma sahip. Minimumun yeri sinirin icindeyse oraya git, disindaysa sinira git.

**Bu formuldeki parcalar:**
- ||g_k||^3: Gradyanin kupunun normu — gradyan buyudukce daha uzaga gitmek ister
- Delta_k * g_k^T B_k g_k: Guven bolgesi yaricapi carpi egrilik — buyuk egrilik ve buyuk bolge daha kisa adim demek
- min(..., 1): Siniri asmamak icin 1'de kesilir

### Cauchy Noktasinin Ozellikleri

| Ozellik | Deger |
|---------|-------|
| **Hesaplama maliyeti** | Cok dusuk — sadece bir ic carpim ve bolme |
| **Yakinsaklik hizi** | Yavas — steepest descent ile ayni (lineer yakinsaklik) |
| **Kullanim** | Referans noktasi olarak; diger yontemlerin en az bu kadar iyi olmasi beklenir |
| **Avantaj** | Hessian'in pozitif tanili olmasini gerektirmez |

### Geometrik Yorum

Cauchy noktasi, trust region dairesinin icinde **sadece gradyan dogrultusu uzerinde** arama yapar. Diger yonleri tamamen gormezden gelir. Bu yuzden "dar goruslu" ama "guvenli" bir yontemdir.

---

## 2. Dogleg Yontemi

### Temel Fikir

Dogleg ("kopek bacagi") yontemi, Cauchy noktasinin yavasligi ile Newton adiminin riskini birlestirmeye calisir. Iki uc noktayi birlestirir:

- **p^U (Unconstrained Cauchy)**: Kisitsiz Cauchy noktasi (steepest descent yonunde optimal)
- **p^B (Newton adimi)**: Tam Newton adimi p^B = -B^(-1) g

Ve bunlar arasinda parcali-lineer bir yol cizip, bu yol uzerinde guven bolgesi siniriyla kesisen noktayi bulur.

### Kosul: B_k Pozitif Tanili Olmali

Dogleg yontemi **B_k'nin pozitif tanili oldugunu** varsayar. Yoksa Newton yonu tanimli olmaz veya inis yonu olmayabilir.

### p^U: Kisitsiz Cauchy Noktasi

$$p^U = -\frac{g^T g}{g^T B g} \, g$$

**Bu formulun anlami:**
- -g: Steepest descent yonu
- g^T g / (g^T B g): Optimal adim boyu — steepest descent yonunde modeli minimize eden katsayi
- Sonuc: Kisitilamasiz olarak, gradient yonunde modeli en cok azaltan nokta

**Geometrik yorum:** g^T g / (g^T B g) degeri, gradyan yonundeki "en iyi mesafe"dir. Eger egrilik (g^T B g) buyukse kisa adim, kucukse uzun adim.

### p^B: Newton Adimi

$$p^B = -B^{-1} g$$

Bu, modelin kisitsiz minimumu. Eger guven bolgesi icindeyse ideal cozumdur.

### Dogleg Yolu: p(tau)

Dogleg yontemi iki parcadan olusan bir yol tanimlar:

$$p(\tau) = \begin{cases} \tau \, p^U & 0 \leq \tau \leq 1 \\ p^U + (\tau - 1)(p^B - p^U) & 1 < \tau \leq 2 \end{cases}$$

**Birinci parca (0 <= tau <= 1):** Orijinden p^U'ya (Cauchy noktasina) dogru ilerle.
- tau = 0: Hic adim atma (p = 0)
- tau = 1: Cauchy noktasina gel (p = p^U)

**Ikinci parca (1 < tau <= 2):** p^U'dan p^B'ye (Newton adimina) dogru ilerle.
- tau = 1: Cauchy noktasindasin
- tau = 2: Newton adimina geldin (p = p^B)

### Dogleg Algoritmasi

1. Newton adimini hesapla: p^B = -B^(-1) g
2. Eger ||p^B|| <= Delta_k: Newton adimini kullan (zaten guven bolgesi icinde)
3. Cauchy noktasini hesapla: p^U
4. Eger ||p^U|| >= Delta_k: Cauchy noktasini olcekleyip sinira oturt
5. Yoksa: Dogleg yolu uzerinde ||p(tau)|| = Delta_k olan tau'yu bul

### p(tau) ile Sinirin Kesisimi

||p(tau)|| = Delta_k denklemini cozmek icin:

Ikinci parcada (1 < tau <= 2):

$$\|p^U + (\tau-1)(p^B - p^U)\|^2 = \Delta_k^2$$

Bu, tau icin bir kuadratik denklemdir — kolayca cozulur.

### Dogleg'in Ozellikleri

| Ozellik | Deger |
|---------|-------|
| **Hesaplama maliyeti** | Dusuk — bir Newton adimi + bir Cauchy noktasi |
| **Yakinsaklik hizi** | Cauchy'den iyi, Newton'a yakin (superlineer olabilir) |
| **Kosul** | B_k pozitif tanili olmali |
| **Avantaj** | Newton bilgisini kullanir ama guvenli kalir |

### Geometrik Yorum

Guven bolgesi (daire) icinde iki parcali bir "kopek bacagi" yolu var:
1. Orijinden Cauchy noktasina (steepest descent yonu)
2. Cauchy noktasindan Newton noktasina (kestirme yol)

Guven bolgesi kucukse: Yol erken kesilir, Cauchy'ye yakin bir cozum bulunur.
Guven bolgesi buyukse: Yol Newton noktasina kadar uzanir.

---

## 3. 2 Boyutlu Alt-Uzay Minimizasyonu

### Temel Fikir

n boyutlu problemi **2 boyutlu** bir alt-uzayda cozeriz. Bu alt-uzay, iki onemli yonun gerdigi uzaydir:

- **g**: Gradyan yonu (steepest descent bilgisi)
- **B^(-1) g**: Newton yonu (ikinci turev bilgisi)

### Formul

$$\min_{\|p\| \leq \Delta_k} \; m_k(p) = f_k + g_k^T p + \frac{1}{2} p^T B_k p \quad \text{kosul:} \quad p \in \text{span}\{g, B^{-1}g\}$$

**span{g, B^(-1)g} ne demek?**
- g ve B^(-1)g vektorlerinin lineer kombinasyonlari
- p = alpha * g + beta * B^(-1)g seklinde yazilabilir
- Bu, n boyutlu uzayi 2 boyuta indirir

### Avantaj

- B pozitif tanili olmak zorunda degil (dogleg'den farkli!)
- B belirsiz (indefinite) ise: alpha oyle bulunur ki (B + alpha I) pozitif tanili olsun
  - ||( B + alpha I)^(-1) g|| <= Delta_k ise: p = -(B + alpha I)^(-1) g + v (v^T(B + alpha I)^(-1) g <= 0 kosulu ile)
  - Degilse: p in span{g, (B + alpha I)^(-1) g}
- Dogleg'e gore daha iyi cozum bulur, cunku 2 boyutlu uzayda tam optimizasyon yapar

### Dogleg ile Karsilastirma

| Ozellik | Dogleg | 2D Alt-uzay |
|---------|--------|-------------|
| B pozitif tanili gerekli mi? | Evet | Hayir |
| Cozum kalitesi | Iyi (yaklasik) | Daha iyi (2D'de tam) |
| Hesaplama maliyeti | Dusuk | Orta |

---

## 4. Steihaug Algoritmasi

Steihaug algoritmasi buyuk olcekli problemler icin tasarlanmistir (Chapter 7'de detayli islenecek). Temel fikir:

- **Conjugate Gradient (CG)** iterasyonlarini trust region kisiti altinda calistir
- CG iterasyonlari guven bolgesinin disina cikinca dur
- B pozitif tanili olmak zorunda degil

Bu yontem buyuk boyutlu problemlerde (n >> 1000) en pratik yaklasimdir cunku B matrisini acikca olusturmaya veya tersini almaya gerek yoktur.

---

## Yontemlerin Genel Karsilastirmasi

| Yontem | Hiz | Maliyet | B pozitif tanili? | Kullanim Alani |
|--------|-----|---------|-------------------|----------------|
| **Cauchy** | Yavas (lineer) | Cok dusuk | Gerekmez | Referans; basit problemler |
| **Dogleg** | Iyi (superlineer) | Dusuk | **Evet, gerekli** | Kucuk-orta problemler |
| **2D Alt-uzay** | Cok iyi | Orta | Gerekmez | Orta problemler |
| **Steihaug** | Iyi | Dusuk (buyuk n icin) | Gerekmez | Buyuk olcekli problemler |

---

## Cauchy Noktasi ve Global Yakinsaklik

Cauchy noktasi onemli bir teorik role sahiptir. Global yakinsaklik icin yeterli olan kosul sudur:

$$m_k(0) - m_k(p_k) \geq c \cdot \left(m_k(0) - m_k(p_k^C)\right) \quad \text{burada } c > 0$$

**Anlami:** Secilen adim p_k, modeli en azindan Cauchy noktasinin bir sabitle carpilmis hali kadar azaltmalidir.

Bu kosulu:
- Cauchy noktasi: Dogal olarak saglar (c = 1)
- Dogleg: Saglar (Cauchy'den daha iyi)
- 2D Alt-uzay: Saglar (Cauchy'den daha iyi)
- Steihaug: Saglar

Dolayisiyla tum bu yaklasik yontemler **global yakinsaklik** garantisi tasir.

---

## Ozet

| Kavram | Aciklama |
|--------|----------|
| **Cauchy noktasi** | Gradyan yonunde, guven bolgesi icinde modeli minimize eden nokta |
| **Dogleg** | Cauchy ve Newton noktalarini parcali-lineer yolla birlestiren yontem |
| **2D alt-uzay** | g ve B^(-1)g yonlerinin gerdigi 2 boyutlu uzayda tam optimizasyon |
| **Steihaug** | CG iterasyonlarini trust region kisiti altinda calistiran buyuk olcekli yontem |
| **Hepsinin ortak ozelligi** | Global yakinsaklik icin yeterli azalma kosulunu saglarlar |
