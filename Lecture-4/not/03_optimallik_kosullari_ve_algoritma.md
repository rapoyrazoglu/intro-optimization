# Optimallik Kosullari ve Trust Region Algoritması

## Trust Region Alt Probleminin Tam Cozumu

Trust region alt problemi suydu:

$$\min_{p} \quad m_k(p) = f_k + g_k^T p + \frac{1}{2} p^T B_k p \quad \text{kosul:} \quad \|p\| \leq \Delta_k$$

Bu kisitli optimizasyon probleminin **tam cozumu** ne zaman optimaldir? Bunu belirleyen kosullara **optimallik kosullari** denir.

---

## Teorem 1 (Optimallik Kosullari — Teorem 4.3)

p* vektoru trust region alt probleminin **global** (en iyi) cozumudur **ancak ve ancak** asagidaki kosullar saglanirsa:

### Kosul 1: (B + lambda I) p* = -g

$$(\mathbf{B}_k + \lambda \mathbf{I}) \, p^* = -g_k$$

**Bu formulun anlami:**

| Sembol | Anlami |
|--------|--------|
| **B_k** | Hessian matrisi (veya yaklasimi) — fonksiyonun egrilik bilgisi |
| **lambda** | Lagrange carpani — kisiti hesaba katan ekstra parametre (lambda >= 0) |
| **I** | Birim matris — kosegenleri 1, geri kalan 0 |
| **B_k + lambda I** | Hessian'a lambda kadar "ekleme" yapilmis hali |
| **p*** | Optimal adim vektoru — cozum |
| **-g_k** | Negatif gradyan — inis yonu |

**Sezgisel aciklama:** Bu denklem aslinda "modifiye edilmis bir Newton denklemi"dir.

- Siradan Newton denklemi: B_k p = -g_k (yani p = -B_k^(-1) g_k)
- Trust region denklemi: (B_k + lambda I) p = -g_k

lambda = 0 oldugunda bu tam Newton adimina donusur. lambda > 0 oldugunda Hessian'a lambda I eklenerek matris "daha pozitif tani" yapilir — bu da adimi kisaltir.

**Geometrik yorum:** lambda arttikca cozum p* kisalir (merkeze yaklasir). lambda = 0'da cozum en uzundur (Newton adimi). lambda'yi ayarlayarak cozumu tam guven bolgesi sinirina oturtabiliriz.

### Kosul 2: Tamamlayici Gevsetme (Complementary Slackness)

$$\lambda (\Delta_k - \|p^*\|) = 0$$

Bu cok onemli bir kosul. Iki faktor carpilmis ve sonuc sifir. Yani ya biri ya digeri (ya da ikisi de) sifir olmali:

**Durum A: lambda = 0**
- Kisit aktif degil — Newton adimi zaten guven bolgesi icinde
- ||p*|| < Delta_k (cozum kurenin icinde)
- Trust region kisiti etkisiz — serbest cozum yeterli

**Durum B: Delta_k - ||p*|| = 0, yani ||p*|| = Delta_k**
- Kisit aktif — cozum tam sinirda
- lambda > 0 (kisit bizi geriye cekiyor)
- Newton adimi cok buyuk oldugu icin budanmis

**Sezgisel aciklama:** "Ya kisit onemli degil (lambda = 0) ya da kisit tam sinirda aktif (||p*|| = Delta_k). Ikisi arasinda bir durum yok."

Bu, ekonomideki arz-talep dengesi gibi dusunulebilir: Ya kisitlama etkisiz (lambda = 0, yani kisit bedava) ya da kisitlama tam sinirda calisiyor (kaynak tam tukenmis).

### Kosul 3: Pozitif Yari-Tanilik

$$B_k + \lambda I \succeq 0 \quad \text{(pozitif yari-tanili)}$$

Bu, B_k + lambda I matrisinin **pozitif yari-tanili** (positive semidefinite) olmasi gerektigini soyler.

**Ne demek pozitif yari-tanili?** Herhangi bir v vektoru icin:

$$v^T (B_k + \lambda I) v \geq 0$$

Yani bu matris hicbir yonde "negatif egrilik" gostermez. Bu, bulunan p*'nin gercekten bir minimum olmasi icin gereklidir (maksimum veya eyer noktasi degil).

**Onemli:** B_k'nin kendisi pozitif tanili olmak zorunda degil! lambda yeterince buyuk olursa B_k + lambda I pozitif tanili olur. Bu, Trust Region'un Newton yontemine gore buyuk avantajidir — negatif egrilikli (konveks olmayan) bolgelerde bile calisabilir.

---

## Iki Farkli Durum: Geometrik Anlami

### Durum 1: Kisitsiz Cozum Icerde (lambda = 0)

Eger B_k pozitif tanili ise ve ||B_k^(-1) g_k|| <= Delta_k ise:

$$p^* = -B_k^{-1} g_k \quad \text{(tam Newton adimi)}$$

Bu durumda:
- Newton adimi zaten guven bolgesi icinde
- Kisit etkisiz, lambda = 0
- Trust region metodu Newton metodu gibi davranir

### Durum 2: Cozum Sinirda (lambda > 0)

Eger ||B_k^(-1) g_k|| > Delta_k ise (Newton adimi cok buyuk):

$$p^* = -(B_k + \lambda I)^{-1} g_k \quad \text{ve} \quad \|p^*\| = \Delta_k$$

Bu durumda:
- lambda > 0 bulunarak cozum tam sinira oturtulur
- Adim Newton adimindan kisa ama yonu benzer
- lambda'yi bulmak icin ||-(B_k + lambda I)^(-1) g_k|| = Delta_k denklemini cozmemiz gerekir

---

## lambda'yi Bulmak: Pratik Yaklasim

Kisit aktif oldugunda (Durum 2), su denklemi cozmemiz gerekir:

$$\phi(\lambda) = \|-(B_k + \lambda I)^{-1} g_k\| - \Delta_k = 0$$

Bu, **tek degiskenli dogrusal olmayan bir denklem**dir. lambda'nin fonksiyonu olan phi(lambda)'yi sifir yapan lambda'yi ariyoruz.

### Eger B_k Diyagonal Ise (veya Diyagonallestirilebiliyorsa)

B_k matrisinin ozdegerleri b_1, b_2, ..., b_n ve g_k'nin bu ozvektorlerdeki bilesenleri gamma_1, gamma_2, ..., gamma_n ise:

$$\|p(\lambda)\|^2 = \sum_{i=1}^{n} \frac{\gamma_i^2}{(b_i + \lambda)^2}$$

Bu toplami Delta_k^2'ye esitleyerek lambda bulunabilir. Bu genelde Newton yontemi veya bisection ile sayisal olarak cozulur.

### Ornek: 2x2 Diyagonal Durum

B_k = [[120, 0], [0, 36]], g_k = [152, 28], Delta_k = 1 oldugunda:

$$(B + \lambda I) p = -g \implies p = \begin{pmatrix} \frac{-152}{120+\lambda} \\ \frac{-28}{36+\lambda} \end{pmatrix}$$

||p|| = Delta_k = 1 kosulu:

$$\left(\frac{152}{120+\lambda}\right)^2 + \left(\frac{28}{36+\lambda}\right)^2 = 1$$

Bu denklemi lambda icin cozersek lambda ≈ 42.655 buluruz.

---

## Global Yakinsaklik: Teorem 4.5

Trust Region yonteminin en onemli teorik garantisi **global yakinsaklik**tir.

### Teorem 4.5'in Kosullari

Asagidaki sartlar saglansin:

1. **||B_k|| sinirli**: Hessian yaklasimlarinin normlari bir ust sinirla kısıtlı
2. **f altta sinirli**: Level set S = {x | f(x) <= f(x_0)} uzerinde f altta sinirli
3. **Lipschitz surekli turev**: f, S'nin bir komsulugunda surekli tureve sahip ve turev Lipschitz surekli

4. **Yeterli azalma kosulu**: Her adimda model azalmasi su alt siniri saglar:
   $$m_k(0) - m_k(p_k) \geq c_1 \|g_k\| \min\left(\Delta_k, \frac{\|g_k\|}{\|B_k\|}\right)$$

5. **||p_k|| <= gamma Delta_k**: Adim boyutu guven bolgesiyle orantili (gamma >= 1, c_1 in (0,1])

### Sonuc

$$\lim_{k \to \infty} \inf \|g_k\| = 0$$

**Bu ne demek?** Iterasyonlar ilerledikce, gradyanin normu eninde sonunda sifira yaklasir. Yani algoritma bir **kritik noktaya** (gradyanin sifir oldugu nokta) yakinsar.

### Sezgisel Aciklama

"Eger modelimiz makul derecede iyi (kosullar 1-5) ve fonksiyon cok cildirmiyorsa (Lipschitz kosulu), o zaman Trust Region algoritması eninde sonunda bir kritik noktaya ulasir."

Bu, Trust Region'un en buyuk guclerinden biri: **Baslangic noktasindan bagimsiz olarak** global yakinsaklik garantisi verir (line search yontemlerinde bu her zaman garanti degildir).

---

## Yeterli Azalma Kosulunun Anlami

$$m_k(0) - m_k(p_k) \geq c_1 \|g_k\| \min\left(\Delta_k, \frac{\|g_k\|}{\|B_k\|}\right)$$

Bu formulun sol ve sag tarafini inceleyelim:

**Sol taraf: m_k(0) - m_k(p_k)**
- Modeldeki azalma miktari
- p_k adimi modeli ne kadar iyilestirdi?

**Sag taraf: c_1 ||g_k|| min(Delta_k, ||g_k|| / ||B_k||)**
- Bir **alt sinir** — en az bu kadar azalma olmali
- ||g_k||: Gradyanin buyuklugu — gradyan buyukse daha fazla azalma beklenir
- min(Delta_k, ||g_k|| / ||B_k||): Iki olcekten kucuk olani
  - Delta_k: Guven bolgesi yaricapi
  - ||g_k|| / ||B_k||: Gradyanin Hessian'a oranla buyuklugu (Cauchy adiminin yaklasik boyutu)

**Anlami:** "Her adimda en azindan Cauchy noktasinin saglayacagi kadar azalma olsun." Bu kosul, Cauchy noktasi ve dogleg gibi yaklasik yontemlerin hepsinin sagladigi bir kosuldur.

---

## Onemli Gozlemler: Optimallik Kosullarinin Geometrik Yorumu

Farkli Delta_k degerleri icin cozum p* nasil degisir?

### Kucuk Delta_k (Delta_k << 1)

- Guven bolgesi cok kucuk
- Model yaklasik olarak lineer: m_k(p) ≈ f_k + g_k^T p
- Cozum: p* ≈ -Delta_k * g_k / ||g_k|| (steepest descent yonunde, tam sinirda)
- Trust region metodu **en dik inis** gibi davranir

### Buyuk Delta_k (Delta_k >> 1)

- Guven bolgesi cok buyuk — kisit etkisiz
- Cozum: p* = -B_k^(-1) g_k (Newton adimi)
- Trust region metodu **Newton metodu** gibi davranir

### Orta Delta_k

- Cozum, steepest descent ile Newton adimi arasinda bir yerdedir
- lambda, bu iki ucun arasinda interpolasyon yapar
- Delta_k kuculdukce steepest descent'e, buyudukce Newton'a yaklasir

Bu gozlem cok onemli: Trust Region, otomatik olarak steepest descent (guvenli ama yavas) ile Newton (hizli ama riskli) arasinda gecis yapar!

---

## Ozet

| Kavram | Formul/Kosul | Anlami |
|--------|-------------|--------|
| Optimallik kosulu 1 | (B+lambda I)p* = -g | Modifiye Newton denklemi |
| Tamamlayici gevsetme | lambda(Delta - \|\|p*\|\|) = 0 | Ya kisit pasif ya da aktif |
| Pozitif yari-tanilik | B + lambda I >= 0 | Cozumun minimum olmasi garanti |
| lambda = 0 | Newton adimi icerde | Kisitsiz cozum yeterli |
| lambda > 0 | Cozum sinirda | Newton adimi budanmis |
| Global yakinsaklik | lim inf \|\|g_k\|\| = 0 | Algoritma kritik noktaya yakinsar |
| Yeterli azalma | m_k(0)-m_k(p_k) >= c_1\|\|g\|\| min(...) | Her adimda minimum ilerleme |
