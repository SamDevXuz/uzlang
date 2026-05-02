# 🇺🇿 UzLang — O‘zbekcha dasturlash tili

**UzLang** — bu yangi boshlovchilar uchun mo‘ljallangan, o‘zbek tilida yoziladigan, minimalist va xavfsiz dasturlash tili. Rust tilida yozilgan bo‘lib, u tezkorlik va xavfsizlikni ta'minlaydi.

---

## 🚀 Xususiyatlari

- **Milliy sintaksis:** Dasturlashni ona tilida o‘rganish imkoniyati.
- **SSRF Himoyasi:** Tarmoq so‘rovlari uchun o‘rnatilgan xavfsizlik filtrlari (loopback va shaxsiy IP-larni bloklash).
- **Sodda va tushunarli:** Python’ga o‘xshash oson sintaksis.
- **Tezkorlik:** Rust dvigateli yordamida ishlaydi.

---

## 🛠 O‘rnatish

1. **Rustni o‘rnating:** [rust-lang.org](https://www.rust-lang.org/) orqali.
2. **Repozitoriyani klonlang:**
   ```bash
   git clone https://github.com/foydalanuvchi/uzlang.git
   cd uzlang/uzlang
   ```
3. **Loyihani quring:**
   ```bash
   cargo build --release
   ```

---

## 🔤 Sintaksis

### O‘zgaruvchilar va Shartlar
```uzlang
agar raqam > 10 {
    yoz "Raqam 10 dan katta"
}
```

### Takrorlanish (Loop)
```uzlang
toki raqam < 10 {
    yoz raqam
    raqam = raqam + 1
}
```

### Funksiyalar
```uzlang
funksiya salom_ber(ism) {
    yoz "Salom, " + ism
}

salom_ber("Dunyo")
```

### Kalit so‘zlar lug‘ati
- `agar` — if
- `toki` — while
- `yoz` — print
- `funksiya` — function
- `qaytar` — return
- `uchun` — for
- `ichida` — in
- `so'ra` — input

---

## 🛡 Xavfsizlik (SSRF Protection)

UzLang tarmoq xavfsizligiga alohida e'tibor beradi. U ichki tarmoqlarga (`127.0.0.1`, `192.168.x.x` va h.k.) kirishni cheklaydigan o‘rnatilgan mexanizmga ega.

---

## 🤝 Hissa qo‘shish

Loyihani yaxshilash bo‘yicha takliflaringiz bo‘lsa, Pull Request yuboring yoki Issue oching!

---

## 📄 Litsenziya

MIT Litsenziyasi ostida tarqatiladi.
