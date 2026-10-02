# داوو مرضاكم بالصدقة - برويش

دفتر تبرعات ومصروفات (PWA).
- **الواجهة:** `index.html` على GitHub Pages
- **السيرفر:** Cloudflare Worker + KV في فولدر `worker/` (بدل Firebase)

## 1) السيرفر (Cloudflare)
1. dash.cloudflare.com ← **Storage & Databases ← KV ← Create** باسم `daawo-db`.
2. **Workers & Pages ← Create ← Worker** باسم `daawo-api` ← Deploy ← **Edit code**، امسح الكود والصق محتوى `worker/worker.js` ← Deploy.
3. من الـ Worker ← **Settings ← Bindings ← Add ← KV namespace**: الاسم `DB` والـ namespace هو `daawo-db`.
4. **Settings ← Variables and Secrets ← Add** نوع **Secret**، وضيف اتنين:
   - `SECRET` وقيمته أي نص عشوائي طويل (30 حرف أو أكتر).
   - `SETUP_CODE` وقيمته كود سري تختاره انت (ده اللي بيسمح بإنشاء حساب المدير، متقولوش لحد).
5. انسخ رابط الـ Worker (شكله `https://daawo-api.XXXX.workers.dev`).

## 2) الواجهة (GitHub Pages)
1. افتح `index.html` وغيّر السطر:
   `var API_URL = "PUT_WORKER_URL_HERE";` ← حط رابط الـ Worker.
2. ارفع الملفات على GitHub ← **Settings ← Pages ← Deploy from a branch ← main / root**.

## أول مرة
افتح الرابط، هتظهر شاشة "إعداد حساب المدير": اكتب `SETUP_CODE` وبيانات المدير. الحساب ده بيتعمل **مرة واحدة بس**، وبعدها مفيش أي شاشة تسجيل جديد: المشرفين والعاملين بيضيفهم المدير من تاب "العاملين".

## تغيير الموبايل / تغيير المدير
- **موبايل جديد لنفس المدير:** سجّل دخول بنفس اسم المستخدم وكلمة السر، والبيانات كلها على السيرفر.
- **نسيت كلمة السر أو عايز مدير تاني:** من شاشة الدخول اضغط "نسيت كلمة سر المدير / عايز أغيّر المدير" واكتب `SETUP_CODE` وبيانات المدير الجديد. البيانات بتفضل زي ما هي، والمدير القديم بيتطلّع من كل الأجهزة.
- لو `SETUP_CODE` ضاع: غيّره من Cloudflare (Settings ← Variables and Secrets).
