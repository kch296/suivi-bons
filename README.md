# 🚀 صفحة تحميل التطبيق — GitHub Pages

صفحة تحم��ل واحدة، مجانية، تعمل من الهاتف مباشرة.
**لا تحتاج أي خادم، لا استضافة مدفوعة، لا حساب Play Store.**

---

## 📁 محتويات المجلد

```
PUBLICATION-GITHUB/
├── index.html          ← الصفحة (جاهزة)
├── downloads/          ← ملفات APK (ضعها هنا)
│   ├── Suivi-des-Bons-v1.0-arm64.apk      (يُبنى)
│   ├── Suivi-des-Bons-v1.0-arm32.apk      (يُبنى)
│   ├── Suivi-des-Bons-v1.0-universal.apk
│   └── icone-512x512.png
├── shots/              ← لقطات الشاشة (اختياري)
└── README.md
```

---

## 🚀 النشر — الطريقة الأسهل (بدون git)

### 1. أنشئ المستودع
1. افتح <https://github.com/new>
2. **Repository name**: `suivi-bons`
3. **Public** ⚠️ (Pages مجانية للمستودعات العامة فقط)
4. **Add a README file** ← ضع علامة ✅
5. **Create repository**

### 2. ارفع الملفات
1. في المستودع: **Add file → Upload files**
2. اسحب **محتوى مجلد `PUBLICATION-GITHUB` كاملًا** إلى النافذة
3. ⚠️ **مهم:** تأكد أن `index.html` موجود في **الجذر** (ليس داخل مجلد فرعي)
4. **Commit changes**

### 3. فعّل GitHub Pages
1. **Settings** (أعلى اليمين) → **Pages** (قائمة يسار)
2. **Source**: `Deploy from a branch`
3. **Branch**: `main` / `(root)`
4. **Save**
5. انتظر 1–2 دقيقة ⏳

### 4. الرابط
```
https://kch296.github.io/suivi-bons/
```

**هذا رابطك الدائم. مجاني إلى الأبد، ما دام المستودع موجود.**

---

## 🎨 مميزات الصفحة

| الميزة | التفاصيل |
|---|---|
| 🌍 **عربي + فرنسي** | الواجهة عربية RTL، مع شرح التثبيت بالفرنسية |
| 📱 **كشف المعمارية** | يختار `arm64` أو `arm32` تلقائيًا حسب الهاتف |
| 🌗 **وضع ليلي** | يتكيّف مع إعداد الهاتف (`prefers-color-scheme`) |
| 🎨 **هوية التطبيق** | نفس ألوان `colors.xml` تمامًا |
| 📦 **بلا تبعيات** | لا CDN، لا خطوط خارجية، لا تتبع — سريع حتى على شبكة ضعيفة |
| 📴 **يعمل بلا إنترنت** | بعد أول زيارة، الصفحة محفوظة في المتصفح |
| 🔒 **الخصوصية** | قسم خاص بها، بلا روابط تتبّع |

---

## 🔄 نشر إصدار جديد

1. في `app/build.gradle.kts`:
   ```kotlin
   versionCode = 2     // ⚠️ إجباري
   versionName = "1.1"
   ```
2. ابنِ:
   ```powershell
   .\build_aab.ps1
   .\gradlew assembleRelease -PenableAbiSplits=true
   ```
3. انسخ الملفات الجديدة إلى `downloads/` وسمِّها `v1.1`
4. حدّث في `index.html`:
   ```js
   const ARMB64 = "downloads/Suivi-des-Bons-v1.1-arm64.apk";
   const ARM32  = "downloads/Suivi-des-Bons-v1.1-arm32.apk";
   const UNIV   = "downloads/Suivi-des-Bons-v1.1-universal.apk";
   ```
5. `Add file → Upload files` → Commit

**حدود GitHub:** 100 ميغا للملف ✅ (ملفك ~18)، 1 غيغابايت للمستودع ✅

---

## ⚠️ قبل النشر — قائمة تحقق

- [ ] ملف APK في `downloads/` باسم صحيح
- [ ] `icone-512x512.png` في `downloads/`
- [ ] `index.html` في **جذر** المستودع
- [ ] جرّبت الرابط من هاتفك فعليًا
- [ ] **لقطات الشاشة** (اختياري لكن أقوى بكثير)

### لقطات الشاشة
```powershell
& "$env:LOCALAPPDATA\Android\sdk\platform-tools\adb.exe" exec-out `
  screencap -p > "PUBLICATION-GITHUB\shots\01-accueil.png"
```
Then استبدل المربعات الفارغة في `index.html` بـ:
```html
<img src="shots/01-accueil.png" alt="...">
```

---

## 🔐 تحذير أمني

**لا تضع في هذا المجلد أبدًا:**

| ❌ ممنوع | السبب |
|---|---|
| `*.jks` / `*.keystore` | مفتاح توقيع التطبيق — تسريبه = كارثة |
| `gradle.properties` | فيه كلمات المرور |
| `local.properties` | فيه مسار جهازك |

`.gitignore` في جذر المشروع يحمي نسخة منه تلقائيًا.
**مفتاح التوقيع الحقيقي في:** `C:\Users\Drop\.play-secrets\` (خارج هذا المجلد).
