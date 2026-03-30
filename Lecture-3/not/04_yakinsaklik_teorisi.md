# 4. Line Search Yakinsaklik Teorisi

## Neden Yakinsaklik Onemli?

Bir algoritma yazdin, calistirdin, iterasyonlar ilerliyor. Ama soru su: **bu algoritma gercekten cozume ulasacak mi?** Yoksa sonsuza kadar doner mi?

Yakinsaklik teorisi, "dogru kosullar saglanirsa algoritma cozume gider" diyen matematik garantiler veriyor.

---

## Zoutendijk Teoremi

Bu teorem, line search algoritmalarinin yakinsakligini garanti eden en temel sonuctur.

### Varsayimlar

1. **f alttan sinirli**: Yani f sonsuza kadar kuculemez, bir yerlerde durmak zorunda.
2. **f surekli turevlenebilir**: Gradyan her yerde mevcut.
3. **Gradyan Lipschitz surekli**: Gradyan "aniden" degismez, yani ||grad f(x) - grad f(y)|| <= L * ||x - y|| bir L sabiti icin.
4. **Adim boyu Wolfe kosullarini sagliyor**.

### Bu Varsayimlar Ne Anlama Geliyor?

| Varsayim | Sezgisel Anlam |
|----------|---------------|
| f alttan sinirli | Sonsuz derin bir kuyu yok — bir yerlerde dip var |
| Surekli turevlenebilir | Fonksiyon "kose" veya "kirik" icermiyor |
| Lipschitz gradyan | Fonksiyon "aniden sarpmaz", egim yumusak degisiyor |
| Wolfe kosullari | Her adimda makul bir ilerleme var |

### Teorem

Bu varsayimlar altinda:

**Toplam_{k=0}^{sonsuz} cos^2(theta_k) * ||grad f(x_k)||^2 < sonsuz**

Bu formulu parcalayalim:

| Sembol | Anlami |
|--------|--------|
| **theta_k** | k. adimda arama yonu p_k ile negatif gradyan -grad f(x_k) arasindaki aci |
| **cos(theta_k)** | Bu acinin kosinusu. 1'e ne kadar yakinsa, yon o kadar "iyi" (gradyana yakin) |
| **\|\|grad f(x_k)\|\|** | k. adimda gradyanin buyuklugu. Sifira ne kadar yakinsa, cozume o kadar yakiniz |
| **Toplam < sonsuz** | Sonsuz terimin toplami sonlu bir sayi. Bu, terimlerin sifira gitmesini zorlar |

### Bu Ne Anlama Geliyor?

Sonsuz toplam sonlu ise, her terimin sonunda **sifira gitmesi** gerekir:

**cos^2(theta_k) * ||grad f(x_k)||^2 → 0**

Bu iki sekilde olabilir:

| Durum | Ne Oluyor? | Anlami |
|-------|-----------|--------|
| **\|\|grad f(x_k)\|\| → 0** | Gradyan sifira gidiyor | Duragan noktaya yaklasiyoruz — istedigimiz bu! |
| **cos(theta_k) → 0** | Aci 90 dereceye gidiyor | Yon gittikce "kotulasiyor", gradient'e neredeyse dik gidiyor |

### Iyi Algoritmada Ne Olmali?

Iyi bir algoritma **cos(theta_k)'nin sifira gitmesine izin vermez**. Yani yonu hep gradyana "yeterince yakin" tutar. Bu durumda sadece ||grad f(x_k)|| → 0 kalir — yani **algoritma yakinsar**.

---

## Farkli Yontemler icin Yakinsaklik

### Steepest Descent

Steepest descent'te p_k = -grad f(x_k), yani yon tam olarak negatif gradyan.

Bu durumda theta_k = 0 (aci sifir), cos(theta_k) = 1.

Zoutendijk sonucu:

**Toplam ||grad f(x_k)||^2 < sonsuz**

Bu kesinlikle ||grad f(x_k)|| → 0 demek. Yani **steepest descent + Wolfe her zaman yakinsir**.

Ama ne hizda? Lineer yakinsaklik — yavas olabilir.

### Newton Yontemi

Newton yonunde theta_k sifir olmak zorunda degil ama pozitif definit Hessian ile cos(theta_k) sinirli kalir.

Cozume yakin oldugunda: **kuadratik yakinsaklik** — muhtesem hizli.

### Quasi-Newton (BFGS)

cos(theta_k) sifira gitmiyor (Hessian yaklasimi pozitif definit tutulur).

Yakinsaklik: **superlineer** — lineerden hizli, kuadratikten yavas.

---

## Pratik Sonuclar

1. **Wolfe kosullari + inis yonu = yakinsaklik garantisi.** Formulleri duzgun uygularsan, algoritma cozume gider.

2. **Yon secimi yakinsaklik hizini belirler:**
   - Steepest descent: yavas ama garantili
   - Newton: hizli ama pahali ve bazi kosullar gerekli
   - BFGS: ikisinin arasi — iyi denge

3. **Adim boyu secimi onemli:** Wolfe kosullarini saglamayan bir adim boyu secimi, yakinsakligi bozabilir.

---

## Ozet Tablosu

| Yontem | cos(theta_k) | Yakinsaklik | Maliyet |
|--------|-------------|-------------|---------|
| Steepest Descent | = 1 (her zaman) | Lineer (yavas) | Dusuk |
| Newton | > 0 (sinirli) | Kuadratik (hizli) | Yuksek |
| BFGS | > 0 (sinirli) | Superlineer | Orta |
| Kotu yon secimi | → 0 | Garanti yok! | - |
