# تشغيل موقع T.M مع لوحة المدير (Firebase)

الخطة المجانية (Spark) تكفي، ولا تحتاج بطاقة دفع. أسماء الأزرار بموقع Firebase ممكن تختلف شوية، بس الفكرة نفسها.

## 1) سوي مشروع Firebase
1. ادخل على console.firebase.google.com بحساب Gmail.
2. اضغط **Create a project**، اكتب أي اسم (مثل tm-shop)، وكمّل.

## 2) أضف تطبيق ويب وخذ الإعدادات
1. داخل المشروع اضغط أيقونة الويب `</>`.
2. سمّه أي اسم واضغط Register.
3. راح يطلع لك كود فيه `firebaseConfig`. انسخ هالقيم: `apiKey` و `authDomain` و `projectId` و `appId`.

## 3) فعّل تسجيل الدخول وسوي حساب المدير
1. من القائمة: **Authentication** ثم **Get started**.
2. فعّل **Email/Password**.
3. من تبويب **Users** اضغط **Add user** واكتب إيميلك وكلمة مرور قوية. هذا حساب المدير.

## 4) سوي قاعدة البيانات وحط القواعد
1. من القائمة: **Firestore Database** ثم **Create database** (اختار أي مكان قريب، وضع Production).
2. افتح تبويب **Rules**، امسح اللي موجود والصق هذا، وبدّل الإيميل بإيميلك:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read: if true;
      allow write: if request.auth != null
                   && request.auth.token.email == "ايميلك@gmail.com";
    }
  }
}
```

3. اضغط **Publish**. هذي القواعد تخلي الكل يشوف المتجر، وإنت بس تعدّل.

## 5) عبّي الإعدادات بالملف
1. افتح الملف `tm-shop-firebase.html` بـ Notepad.
2. ابحث عن `{FB_CONFI(2005)}.
3. ابحث عن `ADMIN_EMAIL` (SMART.VF549@GMAIL.COM).

## 6) انشره
1. ارفع الملف على Netlify Drop (أو GitHub Pages) وخذ الرابط.
2. ارجع لـ Firebase: **Authentication** ثم **Settings** ثم **Authorized domains**، وأضف دومين موقعك (مثل اسم-موقعك.netlify.app).

## 7) استخدمه
1. افتح الموقع واضغط **دخول المدير** تحت، واكتب الإيميل وكلمة المرور.
2. تظهر ⚙️ وأزرار **تعديل** و **حذف** على كل جهاز.
3. من ⚙️ تضيف ماركات وأجهزة وصور، وتحط رقم الواتساب، وتحذف ماركات.
