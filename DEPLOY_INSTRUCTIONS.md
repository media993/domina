# 🚀 تعليمات النشر السريع على Render

## 📦 الطريقة الأولى: النشر المباشر (بدون Git)

### 1. إنشاء حساب Render
- اذهب إلى: https://render.com
- سجل دخول مجاني

### 2. إنشاء Web Service
1. اضغط **"New +"** → **"Web Service"**
2. اختر **"Deploy an existing image or build from source code"**
3. اختر **"Public Git repository"**
4. استخدم هذا الرابط: `https://github.com/render-examples/express-hello-world`
5. أو ارفع الملفات يدوياً

### 3. إعدادات الخدمة
```
Name: domino-server
Runtime: Node
Build Command: npm install
Start Command: node basic-server.js
```

### 4. الملفات المطلوبة للرفع:
- `basic-server.js` (الخادم الرئيسي)
- `package.json` (التبعيات)
- `render.yaml` (إعدادات Render)

## 🌐 الطريقة الثانية: استخدام خدمة أخرى

### Railway (بديل سهل):
1. اذهب إلى: https://railway.app
2. سجل دخول مع GitHub
3. اضغط **"New Project"** → **"Deploy from GitHub repo"**
4. ارفع الملفات

### Heroku (بديل آخر):
1. اذهب إلى: https://heroku.com
2. إنشاء app جديد
3. استخدم Heroku CLI أو GitHub integration

## 🔧 الطريقة الثالثة: خادم مؤقت سريع

### استخدام ngrok (للاختبار):
1. حمل ngrok من: https://ngrok.com
2. شغل الخادم المحلي: `node basic-server.js`
3. في terminal آخر: `ngrok http 8080`
4. استخدم الرابط المؤقت

## 📝 تحديث إعدادات العميل

بعد الحصول على رابط الخادم، حدث الملف:
`client/src/hooks/useSocket.js`

```javascript
const serverUrl = window.location.hostname === 'localhost' 
  ? 'http://localhost:8080'
  : 'https://YOUR-SERVER-URL.onrender.com'; // ضع رابطك هنا
```

ثم:
```bash
cd client
npm run build
cd ..
firebase deploy --only hosting
```

## 🎯 الحل السريع الآن:

### للاختبار الفوري:
1. شغل الخادم محلياً: `node basic-server.js`
2. افتح: `http://localhost:8080`
3. العب مع الأصدقاء في نفس الشبكة

### للنشر العام:
1. اختر إحدى الطرق أعلاه
2. احصل على رابط الخادم
3. حدث إعدادات العميل
4. أعد نشر Firebase

---

**💡 نصيحة**: ابدأ بـ Railway أو ngrok للاختبار السريع!
