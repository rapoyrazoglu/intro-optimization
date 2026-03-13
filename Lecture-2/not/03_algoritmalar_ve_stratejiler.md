# 3. Algoritmalar ve Stratejiler

## Genel Resim

Gercek hayatta ∇f(x) = 0 denklemini **kalem kagitla** cozmek genellikle imkansiz. Fonksiyonlar cok karmasik, degisken sayisi binlerce, hatta milyonlarca olabilir.

Bu yuzden **iteratif algoritmalar** kullaniyoruz: Bir baslangic noktasindan baslayip, adim adim cozume yaklasiyoruz.

---

## Iteratif Algoritmalarin Genel Yapisi

```
1. Baslangic noktasi x₀ sec
2. k = 0, 1, 2, ... icin tekrarla:
   a. x_k noktasinda fonksiyon hakkinda bilgi topla
   b. Bu bilgiye dayanarak x_{k+1} hesapla
   c. Eger "yeterince iyi" ise dur
```

"Yeterince iyi" genellikle soyle tanimlaniyor:

$$\|\nabla f(x_k)\| < \varepsilon$$

yani gradient neredeyse sifir (mesela ε = 10⁻⁶).

---

## Strateji 1: Line Search (Dogru Arama)

### Temel Fikir

Her iterasyonda iki sey belirliyoruz:
1. **Yon** p_k — "nereye gideyim?"
2. **Adim boyu** α_k — "ne kadar gideyim?"

$$x_{k+1} = x_k + \alpha_k p_k$$

Bu iki bilgiyi sirayla belirliyoruz: once yon, sonra adim boyu.

### Adim Boyu Nasil Secilir?

α_k'yi secmek aslinda **tek degiskenli** bir minimizasyon problemi:

$$\min_{\alpha > 0} f(x_k + \alpha p_k)$$

Bunu φ(α) = f(x_k + α p_k) olarak yazarsak, φ: R → R fonksiyonunu minimize ediyoruz.

#### Exact Line Search (Tam Dogru Arama)

φ(α)'nin **gercek minimumunu** bul:

$$\phi'(\alpha) = 0 \quad \Rightarrow \quad \nabla f(x_k + \alpha p_k)^T p_k = 0$$

Bu genelde pahalı bir islem. Ama **kuadratik fonksiyonlar** icin kapali formulu var (bunu orneklerde gorecegiz).

#### Inexact Line Search (Yaklasik Dogru Arama)

Gercek minimumu bulmak yerine, "yeterince iyi" bir α sec. Pratikte daha cok bu kullanilir. Wolfe kosullari, Armijo kurali gibi yontemler var (ilerideki derslerde detaylandirilacak).

### Descent Direction (Inis Yonu)

p_k yonunun **inis yonu** (descent direction) olmasi sarttir:

$$p_k^T \nabla f(x_k) < 0$$

Bu ne demek? Gradient ile arama yonu arasindaki aci 90°'den buyuk. Yani gradient "yukariya" isaret ederken, biz "asagiya" dogru yuruyoruz.

**Neden gerekli?** Taylor acilimindan:

$$f(x_k + \alpha p_k) \approx f(x_k) + \alpha \nabla f(x_k)^T p_k$$

Eger p_k^T ∇f(x_k) < 0 ise, kucuk α > 0 icin f **azalir**. Yani bir miktar yuruyunce daha iyi bir noktaya geliyoruz.

**Sezgisel:** Eger bir yon inis yonu degilse, o yone yurudugunde fonksiyon artar — yanlis yone gitmis olursun!

---

## Strateji 2: Trust Region (Guven Bolgesi)

### Temel Fikir

Fonksiyonu x_k etrafinda bir **model** m_k(p) ile yaklastir, sonra bu modeli bir **guven bolgesi** icinde minimize et:

$$\min_p m_k(x_k + p) \quad \text{oyle ki } \|p\| \leq \Delta_k$$

- **m_k:** Genellikle 2. derece Taylor (kuadratik model)
- **Δ_k:** Guven bolgesi yaricapi

### Kuadratik Model

$$m_k(p) = f_k + \nabla f_k^T p + \frac{1}{2} p^T B_k p$$

Burada:
- f_k = f(x_k): su anki fonksiyon degeri
- ∇f_k: su anki gradient
- B_k: Hessian veya bir yaklasimi

### Nasil Calisir?

1. Model m_k'yi Δ_k topu icinde minimize et → aday noktayi bul
2. Gercek f degerini kontrol et: f(x_k + p) gercekten azaldi mi?
3. **Evet, cok azaldi** → x_{k+1} = x_k + p, Δ_k'yi buyut (modele guveniyorum)
4. **Evet, biraz azaldi** → x_{k+1} = x_k + p, Δ_k'yi degistirme
5. **Hayir, azalmadi** → x_{k+1} = x_k (yerinde kal), Δ_k'yi kucult (modele az guveniyorum)

### Sezgisel Anlam

Trust region'u soyle dusun: Bir sisli dagda yuruyorsun. Etrafinda sadece belirli bir mesafeye kadar gorebiliyorsun (guven bolgesi). Gorunen alan icinde en dik yokusu bulup oraya yuruyorsun. Eger iyi sonuc veriyorsa, gorusunu genisletiyorsun (yaricapi buyut). Kotuye gidiyorsa, daha kisa mesafe icinde daha dikkatli bakiyorsun (yaricapi kucult).

---

## Line Search vs Trust Region Karsilastirmasi

### Ornek ile Farki Anlama

f(x₁, x₂) fonksiyonunu minimize etmek istiyorsun. x_k = (3, 4) noktasindasin.

**Line Search yaklasimiyla:**
1. Yon sec: p_k = (-1, -2) (mesela steepest descent)
2. Bu yon uzerinde en iyi α'yi ara: α* = 0.5
3. x_{k+1} = (3, 4) + 0.5(-1, -2) = (2.5, 3)

**Trust Region yaklasimiyla:**
1. Δ_k = 1 yaricapli bir daire tanimla (||p|| ≤ 1)
2. Bu daire icinde kuadratik modeli minimize et → p* = (-0.4, -0.9)
3. x_{k+1} = (3, 4) + (-0.4, -0.9) = (2.6, 3.1)

### Avantajlar/Dezavantajlar

| | Line Search | Trust Region |
|--|------------|--------------|
| **Avantaj** | Daha basit uygulanir | Daha saglam (robust) |
| **Avantaj** | Az bellek gerektirir | Hessian indefinit olsa bile calisir |
| **Dezavantaj** | α aramasi pahali olabilir | Alt-problem cozmek gerekir |
| **Kullanim** | Buyuk olcekli problemler | Orta olcek, hassas cozum |

---

## Yakinsaklik (Convergence) Turleri

Algoritma calisirken, cozume ne hizda yaklastigini bilmek onemli.

### Lineer (Dogrusal) Yakinsaklik

$$\|x_{k+1} - x^*\| \leq c \|x_k - x^*\| \quad (0 < c < 1)$$

Her adimda hatayi sabit bir oranla carpiyorsun. Ornegin c = 0.5 ise, her adimda hata yarilaniyor.

**Ornek:** Steepest descent genellikle lineer yakinsaktir.

### Kuadratik Yakinsaklik

$$\|x_{k+1} - x^*\| \leq M \|x_k - x^*\|^2$$

Her adimda hatanin **karesi** alinir. Muhtesem hizli!

- Hata = 0.1 → sonraki hata ≈ 0.01
- Hata = 0.01 → sonraki hata ≈ 0.0001

**Ornek:** Newton yontemi (cozume yakin) kuadratik yakinsaktir.

### Superlineer Yakinsaklik

Lineerden hizli ama kuadratikten yavas. Quasi-Newton yontemleri genellikle superlineer yakinsaktir.

### Neden Onemli?

- Lineer yakinsaklik: cozume ulasmak **cok fazla** iterasyon alabilir
- Kuadratik yakinsaklik: birkac iterasyonda muhtesem hassasiyete ulasirsin
- Ancak kuadratik yakinsaklik genellikle **cozume yakin** oldugunda gecerli

---

## Olcekleme (Scaling) Problemi

### Problem

Degiskenler farkli buyukluk mertebesinde olabilir:

$$f(x_1, x_2) \quad \text{ile} \quad x_1 \approx 10^{-10}, \quad x_2 \approx 10^5$$

Bu durumda steepest descent gibi algoritmalar cok kotu calisir cunku gradient bir degiskende cok buyuk, digerinde cok kucuk olabilir.

### Cozum: Degisken Olcekleme

Yeni degisken z tanimla:

$$z_i = \frac{x_i}{d_i}$$

oyle ki z'nin tum bilesenleri benzer buyuklukte olsun. Buna **kosegen olcekleme (diagonal scaling)** denir.

### Ornek

Kimyasal reaksiyon sabitleri: k₁ = 10⁻¹⁰, k₂ = 1, k₃ = 10⁵

D = diag(10⁻¹⁰, 1, 10⁵) ile olcekleyince, yeni degiskenler z₁, z₂, z₃ ≈ 1 mertebesinde olur.

### Hangi Algoritmalar Olceklemeye Duyarli?

- **Steepest descent:** Cok duyarli — kotu olcekleme = cok yavas yakinsaklik
- **Newton yontemi:** Olceklemeye **duyarsiz** — Hessian bilgisini kullandigindan, olcegi otomatik duzeltir
- **Quasi-Newton:** Genellikle olceklemeye dayanikli
