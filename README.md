# 💊 Dori-narxi

Kerakli dorini eng yaqin va eng arzon narxda topishga yordam beruvchi mobil ilova.

## 📋 Mundarija

- [Loyiha haqida](#loyiha-haqida)
- [Muammo va yechim](#muammo-va-yechim)
- [Asosiy funksiyalar](#asosiy-funksiyalar)
- [Loyiha tuzilishi](#loyiha-tuzilishi)
- [Jamoa](#jamoa)
- [Texnologiyalar](#texnologiyalar)
- [O'rnatish va ishga tushirish](#ornatish-va-ishga-tushirish)
- [Ma'lumotlar bazasi tuzilishi](#malumotlar-bazasi-tuzilishi)
- [Rivojlanish rejasi](#rivojlanish-rejasi)
- [Qanday hissa qo'shish mumkin](#qanday-hissa-qoshish-mumkin)

---

## Loyiha haqida

**Dori-narxi** — foydalanuvchilarga kerakli dorini qidirish, uning turli dorixonalardagi narxini solishtirish va eng yaqin/eng arzon variantni topishga yordam beruvchi mobil ilova.

Loyiha ijtimoiy foyda ko'zlab yaratilgan bepul, ochiq (open-source) tashabbus sifatida boshlangan. Maqsad — dastlab bitta tuman doirasida sinab ko'rish, keyin butun shahar va boshqa hududlarga kengaytirish.

## Muammo va yechim

**Muammo:**
- Bir xil dori turli dorixonalarda har xil narxda sotiladi (farq 30-50% gacha yetishi mumkin)
- Odamlar narxlarni solishtirish imkoniyatiga ega emas
- Ko'pincha kerakli dori bir necha dorixonada bo'lmay, vaqt va transport sarflanadi
- Ayniqsa surunkali kasalligi bor odamlar (diabet, yurak-qon tomir kasalliklari) uchun bu doimiy xarajat muammosi

**Yechim:**
Ilova orqali foydalanuvchi bir necha soniyada:
1. Kerakli dorini qidiradi
2. Yaqin atrofdagi dorixonalardagi narxlarni ko'radi
3. Eng arzon yoki eng yaqin variantni tanlab boradi

## Asosiy funksiyalar

### MVP (birinchi versiya)
- 🔍 Dori nomi bo'yicha qidiruv
- 🏥 Yaqin dorixonalar ro'yxati (narx va mavjudlik bilan)
- 🗺️ Xaritada dorixonani ko'rish

### Kelajakdagi funksiyalar
- 🔔 "Dori mavjud bo'lganda xabar ber" bildirishnomasi
- 💊 Arzonroq analog dorilarni taklif qilish
- ⭐ Foydalanuvchilar tomonidan dorixonalarni baholash
- 🏪 Dorixonalar uchun o'z panelidan narx yangilash imkoniyati

## Loyiha tuzilishi

```
dori-narxi/
├── README.md              # Ushbu fayl
├── .gitignore              # Git tomonidan e'tiborga olinmaydigan fayllar
│
├── backend/                 # Server va ma'lumotlar bazasi
│   ├── src/
│   │   ├── routes/          # API yo'nalishlari (masalan: /search, /pharmacies)
│   │   └── models/          # Ma'lumotlar bazasi modellari
│   ├── package.json
│   └── .env.example         # Muhit o'zgaruvchilari namunasi
│
└── mobile/                  # Flutter mobil ilova
    ├── lib/
    │   ├── screens/          # Ilova ekranlari (qidiruv, natijalar, xarita)
    │   ├── models/           # Ma'lumot modellari (Dorixona, Dori)
    │   └── services/         # Backend bilan bog'lanish kodi
    ├── pubspec.yaml
    └── assets/               # Rasmlar, ikonkalar
```

## Jamoa

| Ism | Rol | Vazifalar |
|---|---|---|
| Dasturchi 1 | Backend dasturchi | Server, ma'lumotlar bazasi, API |
| Dasturchi 2 | Mobil dasturchi | Flutter ilova, UI/UX dizayn |

> *Eslatma: jadvaldagi ismlarni o'z va do'stingizning ismiga almashtiring.*

## Texnologiyalar

| Qism | Texnologiya | Izoh |
|---|---|---|
| Mobil ilova | Flutter | Android va iOS uchun bitta kod |
| Backend | Node.js + Express | Yengil, tez o'rganiladigan, JavaScript asosida |
| Ma'lumotlar bazasi | SQLite | Sozlash talab qilmaydi, MVP uchun yetarli. Keyinchalik PostgreSQL'ga o'tish mumkin |
| Xarita | Yandex Maps API | O'zbekistonda yaxshi ishlaydi |
| Versiya nazorati | Git + GitHub | Kod tarixi va hamkorlik |

## O'rnatish va ishga tushirish

### Talablar
- Node.js (v18+)
- Flutter SDK (3.0+)
- Git

### Backend'ni ishga tushirish

```bash
cd backend
npm install              # kerakli paketlarni o'rnatish
cp .env.example .env     # muhit o'zgaruvchilarini sozlash
npm start                 # serverni ishga tushirish
```

### Mobil ilovani ishga tushirish

```bash
cd mobile
flutter pub get           # kerakli paketlarni o'rnatish
flutter run                # ilovani telefon/emulyatorda ishga tushirish
```

## Ma'lumotlar bazasi tuzilishi

Loyiha 3 ta asosiy jadvaldan iborat:

**pharmacies** (dorixonalar)
| Ustun | Turi | Izoh |
|---|---|---|
| id | INTEGER (PK) | Noyob raqam |
| name | TEXT | Dorixona nomi |
| address | TEXT | Manzil |
| latitude | FLOAT | Xarita koordinatasi |
| longitude | FLOAT | Xarita koordinatasi |
| phone | TEXT | Telefon raqami |

**medicines** (dorilar)
| Ustun | Turi | Izoh |
|---|---|---|
| id | INTEGER (PK) | Noyob raqam |
| name | TEXT | Dori nomi (masalan "Paracetamol") |
| description | TEXT | Qisqa tavsif (ixtiyoriy) |

**prices** (narxlar — bog'lovchi jadval)
| Ustun | Turi | Izoh |
|---|---|---|
| id | INTEGER (PK) | Noyob raqam |
| pharmacy_id | INTEGER (FK) | Qaysi dorixona |
| medicine_id | INTEGER (FK) | Qaysi dori |
| price | DECIMAL | Narxi (so'mda) |
| in_stock | BOOLEAN | Mavjudmi yoki yo'q |
| updated_at | TIMESTAMP | Oxirgi yangilangan vaqt |

## Rivojlanish rejasi

- [x] Loyiha tuzilishini yaratish (GitHub repository, papkalar)
- [ ] Ma'lumotlar bazasini sozlash (jadvallar yaratish)
- [ ] Backend API yozish (dori qidirish, dorixonalarni topish)
- [ ] Mobil ilova interfeysini yasash (qidiruv, natijalar, xarita ekranlari)
- [ ] Bitta tumanda 15-20 dorixona ma'lumotini qo'lda yig'ish
- [ ] Ilovani backend bilan ulash
- [ ] Do'stlar va oila a'zolarida sinovdan o'tkazish
- [ ] Xatolarni tuzatish va yaxshilash
- [ ] Keyingi hududlarga kengaytirish

## Qanday hissa qo'shish mumkin

Bu loyiha hozircha ikki nafar dasturchi tomonidan olib borilmoqda. Agar boshqalar ham yordam bermoqchi bo'lsa:

1. Loyihani "fork" qiling
2. O'z branch'ingizni yarating (`git checkout -b yangi-funksiya`)
3. O'zgarishlaringizni saqlang (`git commit -m "Nimadir qo'shdim"`)
4. Branch'ni yuklang (`git push origin yangi-funksiya`)
5. Pull Request oching

## Litsenziya

Ushbu loyiha MIT License asosida tarqatiladi.
