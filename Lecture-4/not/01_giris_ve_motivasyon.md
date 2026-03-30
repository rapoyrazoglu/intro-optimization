# Trust Region Yontemlerine Giris ve Motivasyon

## Onceki Derslerin Kisa Ozeti

Onceki derslerde **kisitsiz optimizasyon** icin iteratif yontemleri gorduk. Genel yaklasim suydu:

$$x_{k+1} = x_k + \alpha_k \cdot p_k$$

Burada:
- **x_k**: Simdi bulundugumuz nokta (k. iterasyondaki tahminimiz)
- **p_k**: Arama yonu (hangi yone gidecegiz?)
- **alpha_k**: Adim boyu (ne kadar ileri gidecegiz?)

### Onceki Yontemler

| Yontem | B_k matrisi | Aciklama |
|--------|-------------|----------|
| **Steepest Descent** | B_k = I (birim matris) | En dik inis: sadece gradyanin ters yonunde git |
| **Newton's Method** | B_k = nabla^2 f(x_k) (Hessian) | Ikinci turev bilgisini kullanarak daha akilli adim at |
| **Quasi-Newton** | B_k ≈ nabla^2 f(x_k) | Hessian'i yaklasik olarak hesapla |

Bu yontemlerin hepsinde strateji ayni:
1. **Once yon belirle** (p_k)
2. **Sonra adim boyunu sec** (alpha_k) — buna **Line Search** diyorduk

---

## Trust Region: Farkli Bir Felsefe

**Trust Region (Guven Bolgesi)** yontemi tamamen farkli bir stratejiyle calisir:

1. **Once adim boyunu (bolgeyi) belirle**
2. **Sonra o bolge icinde en iyi yonu bul**

Bu, Line Search'un tam tersidir!

### Line Search vs Trust Region Karsilastirmasi

| Ozellik | Line Search | Trust Region |
|---------|-------------|-------------|
| **Once ne belirlenir?** | Yon (p_k) | Bolge buyuklugu (Delta_k) |
| **Sonra ne belirlenir?** | Adim boyu (alpha_k) | Yon ve adim (p_k) |
| **Temel soru** | "Bu yonde ne kadar ilerleyelim?" | "Bu bolge icinde en iyi nereye gidelim?" |
| **Kisit** | Yok (sadece yon sabit) | ||p|| <= Delta_k (bolge disina cikma) |

### Sezgisel Aciklama

Trust Region'u su sekilde dusunebilirsin:

Bir dagda gece karanligi icinde inmeye calisiyorsun. Elinde bir fener var.

- **Line Search yaklasimi**: Bir yon sec, sonra o yonde ne kadar yuruyecegin karar ver.
- **Trust Region yaklasimi**: Fenerinle etrafindaki belirli bir alanis aydinlat. O aydinlik alan icinde en iyi yere git. Eger aydinlattiklarin seni iyi yonlendirdiyse, bir sonraki adimda feneri daha genis tut. Yanildiysan, feneri daralt.

Burada:
- **Fener** = Trust region (guven bolgesi)
- **Aydinlik alanin buyuklugu** = Delta_k (guven bolgesi yaricapi)
- **"Aydinlattiklarin seni iyi yonlendirdi mi?"** = Model fonksiyonumuz gercek fonksiyonu ne kadar iyi temsil etti?

---

## Neden Trust Region?

### Line Search'un Sorunlari

1. **Newton yonu her zaman inis yonu olmayabilir**: Eger Hessian matrisi pozitif tani degilse, Newton yonu bizi yukari cikarabilir.
2. **Adim boyu secimi zor olabilir**: Wolfe kosullari vs. cok sayida fonksiyon degerlendirmesi gerektirebilir.
3. **Konveks olmayan problemlerde sorunlu**: Fonksiyon yerel olarak "tuhaf" davraniyorsa, bir yonde sonsuza kadar gitmek tehlikeli.

### Trust Region'un Avantajlari

1. **Dogal koruma mekanizmasi**: Bolge sinirliyken cok buyuk (tehlikeli) adimlar atilmaz.
2. **Hessian pozitif tani olmak zorunda degil**: Negatif ozdegerlere sahip Hessian bile kullanilabilir.
3. **Adaptif**: Bolge otomatik olarak buyur veya kuculur — model iyi calisiyorsa buyut, kotu calisiyorsa daralt.
4. **Global yakinsaklik garantisi**: Belirli kosullar altinda her zaman bir kritik noktaya yakinsar.

---

## Temel Fikir: Model Fonksiyonu

Trust Region yonteminin kalbinde bir **model fonksiyonu** vardir. Gercek fonksiyonumuz f(x) karmasik olabilir, ama biz onu mevcut noktamizin etrafinda basit bir fonksiyonla **yaklasik olarak temsil ederiz**.

Bu yaklasik fonksiyona **kuadratik model** diyoruz:

$$m_k(p) = f_k + g_k^T p + \frac{1}{2} p^T B_k p$$

Bu formuldeki her seyi tek tek aciklayalim:

| Sembol | Anlami | Aciklama |
|--------|--------|----------|
| **m_k(p)** | Model fonksiyonunun p adimindaki degeri | "p kadar adim atarsam, fonksiyonum yaklasik olarak ne olur?" |
| **f_k** | f(x_k), yani simdiki noktadaki fonksiyon degeri | Bilinen baslangic degeri |
| **g_k** | nabla f(x_k), yani gradyan vektoru | Fonksiyonun hangi yonde ne kadar hizli degistigi |
| **g_k^T p** | Gradyanin p ile ic carpimi | Lineer (birinci derece) yaklasim — "bu yonde ne kadar degisir?" |
| **B_k** | Hessian matrisi (veya yaklasimi) | Ikinci turev bilgisi — fonksiyonun egriligini temsil eder |
| **(1/2) p^T B_k p** | Kuadratik terim | Ikinci derece yaklasim — "egrilik ne kadar etkili?" |
| **p** | Adim vektoru (ne kadar ve hangi yone) | Bulmaya calistigimiz bilinmeyen |

Bu model aslinda Taylor serisinin ikinci dereceye kadar olan acilimi:

$$f(x_k + p) \approx f(x_k) + \nabla f(x_k)^T p + \frac{1}{2} p^T \nabla^2 f(x_k) p$$

---

## Trust Region Alt Problemi

Trust Region yonteminde her iterasyonda cozmemiz gereken problem su:

$$\min_{p} \quad m_k(p) = f_k + g_k^T p + \frac{1}{2} p^T B_k p$$
$$\text{kisit:} \quad \|p\| \leq \Delta_k$$

Bu formulun anlami:

- **Sol taraf (amac fonksiyonu)**: Model fonksiyonunu minimize et — yani en kucuk degeri veren p'yi bul.
- **Sag taraf (kisit)**: Ama p'nin uzunlugu (normu) Delta_k'yi asamaz — yani guven bolgesi disina cikma!

Bu bir **kisitli optimizasyon** problemidir. Line Search'taki gibi sinirsiz bir yonde gitmiyoruz; belirli bir top (kure) icinde en iyi noktayi ariyoruz.

### Geometrik Gorsellestirme

2 boyutlu uzayda dusunelim:
- Mevcut noktamiz x_k, merkez noktasi
- Delta_k yaricapli bir daire ciziyoruz (guven bolgesi)
- Bu daire icinde modeli en kucuk yapan noktayi ariyoruz
- Bulunan nokta p_k, yeni adimimiz oluyor

---

## Genel Algoritma Akisi

Trust Region algoritmasinin her iterasyonunda su iki is yapilir:

1. **Model problemini coz**: Guven bolgesi icinde en iyi p_k'yi bul.
2. **Degerlendirme yap ve bolgeyi guncelle**: p_k iyi miydi? Bolgeyi buyutelim mi, kucultelim mi?

Bir sonraki notta bu adimlarin her birini detayli olarak inceleyecegiz.

---

## Ozet

| Kavram | Aciklama |
|--------|----------|
| **Trust Region** | Fonksiyonu yerel bir modelle temsil edip, sinirli bir bolge icinde optimize etme stratejisi |
| **Delta_k** | Guven bolgesi yaricapi — "modelimize ne kadar guveniyoruz?" |
| **m_k(p)** | Kuadratik model fonksiyonu — gercek fonksiyonun yerel yaklasimi |
| **Alt problem** | min m_k(p) s.t. ||p|| <= Delta_k — her iterasyonda cozmemiz gereken kisitli problem |
| **Temel fark** | Line Search once yon, sonra adim secer; Trust Region once bolge, sonra yon ve adimi birlikte secer |
