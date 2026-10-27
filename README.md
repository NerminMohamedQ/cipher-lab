# Cipher Lab — تطبيق أندرويد

تطبيق يشفّر ويفك ويكسر **Caesar** و**Vigenère** و**Rail Fence** لأي لغة وأي حروف وأرقام ورموز ومسافات.
التطبيق بيشتغل بدون إنترنت. الكود كله في ملف واحد: `www/index.html`.

## المطلوب على جهازك

- Node.js (نسخة 20 أو أحدث)
- Android Studio (آخر نسخة) — فيه JDK 21 جاهز

## تشغيل التطبيق على موبايلك (خطوة بخطوة)

1. فك الضغط عن المجلد، وافتحي Terminal جواه، ونفّذي:

```bash
npm install
```

2. انسخي ملفات الويب جوه مشروع أندرويد:

```bash
npx cap sync android
```

3. افتحي المشروع في Android Studio:

```bash
npx cap open android
```

4. استني لحد ما Gradle يخلّص (أول مرة بياخد وقت لأنه بينزّل الملفات).
5. وصّلي الموبايل بالكابل وفعّلي **USB debugging** (من Developer options)، أو شغّلي Emulator من Device Manager.
6. اضغطي زر **Run ▶** فوق، واختاري جهازك.

## عمل ملف APK للتثبيت والمشاركة

من Android Studio: **Build ▸ Build Bundle(s) / APK(s) ▸ Build APK(s)**.
الملف بيظهر هنا:

```
android/app/build/outputs/apk/debug/app-debug.apk
```

ابعتيه لأي موبايل أندرويد وثبّتيه (لازم تسمحي بالتثبيت من مصدر غير معروف).

## تعديل التطبيق

عدّلي الملف `www/index.html`، وبعدها:

```bash
npx cap sync android
```

ثم شغّلي من Android Studio تاني.

## تغيير الاسم أو معرّف التطبيق

من ملف `capacitor.config.json`:

```json
{
  "appId": "com.cipherlab.app",
  "appName": "Cipher Lab",
  "webDir": "www"
}
```

لو هترفعيه على Google Play، لازم `appId` يكون فريد (مثلًا `com.yourname.cipherlab`).
بعد التغيير نفّذي `npx cap sync android`.

## آيفون (iOS)

محتاج جهاز Mac و Xcode:

```bash
npm install @capacitor/ios
npx cap add ios
npx cap open ios
```

## ملاحظات على الشفرات

- **Auto:** كل لغة بتدور داخل أبجديتها، والأرقام من 0 إلى 9، والمسافات والرموز بتفضل زي ما هي.
- **Full Unicode:** كل حرف أو رمز أو إيموجي بيتحرك في جدول Unicode.
- **Rail Fence:** بيشتغل على كل الأحرف والمسافات والرموز كما هي.
- **الكسر:** بيعتمد على تكرار الحروف في الإنجليزية والعربية والروسية، وبيدقّ أكتر مع النصوص الطويلة.

## بناء الـ APK بدون Android Studio (عن طريق GitHub)

الملف `.github/workflows/build-apk.yml` بيخلّي GitHub يبني الـ APK لوحده كل ما ترفعي المشروع.

1. اعملي حساب على github.com، واعملي Repository جديد فاضي (اسمه مثلًا `cipher-lab`)، من غير README.
2. من Terminal جوه مجلد المشروع (غيّري `USERNAME` باسم حسابك):

```bash
git init
git add .
git commit -m "Cipher Lab"
git branch -M main
git remote add origin https://github.com/USERNAME/cipher-lab.git
git push -u origin main
```

3. افتحي الـ Repository على GitHub ▸ تبويب **Actions** ▸ استني لحد ما يظهر علامة صح خضرا (حوالي 5 إلى 10 دقايق).
4. اضغطي على آخر تشغيل، ونزّلي **cipher-lab-apk** من قسم Artifacts. هيكون zip جواه `app-debug.apk`.
5. ابعتي الـ APK للموبايل وثبّتيه (فعّلي السماح بالتثبيت من مصدر غير معروف).

لو تشغيل Actions فشل، افتحيه وانسخي آخر سطور الخطأ وابعتيهالي.
