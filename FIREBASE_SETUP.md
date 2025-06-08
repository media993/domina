# 🔥 دليل إعداد Firebase للعبة الدومينو

## 📋 الخطوات المطلوبة

### 1. إنشاء مشروع Firebase

1. اذهب إلى [Firebase Console](https://console.firebase.google.com/)
2. اضغط على "إنشاء مشروع" (Create a project)
3. أدخل اسم المشروع: `domino-game` أو أي اسم تفضله
4. اختر إعدادات Google Analytics (اختياري)
5. اضغط "إنشاء مشروع"

### 2. إعداد Authentication

1. في لوحة تحكم Firebase، اذهب إلى **Authentication**
2. اضغط على **Get started**
3. اذهب إلى تبويب **Sign-in method**
4. فعّل الطرق التالية:
   - **Email/Password** ✅
   - **Anonymous** ✅ (للضيوف)

### 3. إعداد Firestore Database

1. اذهب إلى **Firestore Database**
2. اضغط **Create database**
3. اختر **Start in test mode** (للتطوير)
4. اختر موقع قاعدة البيانات (أقرب منطقة لك)

### 4. إعداد Storage

1. اذهب إلى **Storage**
2. اضغط **Get started**
3. اختر **Start in test mode**
4. اختر نفس موقع قاعدة البيانات

### 5. إعداد Hosting

1. اذهب إلى **Hosting**
2. اضغط **Get started**
3. اتبع التعليمات لتثبيت Firebase CLI

### 6. الحصول على إعدادات المشروع

1. اذهب إلى **Project Settings** (⚙️)
2. في تبويب **General**، انزل إلى **Your apps**
3. اضغط على أيقونة الويب `</>`
4. أدخل اسم التطبيق: `domino-game-web`
5. فعّل **Firebase Hosting**
6. انسخ إعدادات `firebaseConfig`

### 7. تحديث إعدادات المشروع

افتح ملف `client/src/config/firebase.js` وحدث الإعدادات:

```javascript
const firebaseConfig = {
  apiKey: "your-api-key-here",
  authDomain: "your-project-id.firebaseapp.com",
  projectId: "your-project-id",
  storageBucket: "your-project-id.appspot.com",
  messagingSenderId: "your-sender-id",
  appId: "your-app-id",
  measurementId: "your-measurement-id"
};
```

## 🛠️ تثبيت Firebase CLI

```bash
# تثبيت Firebase CLI عالمياً
npm install -g firebase-tools

# تسجيل الدخول
firebase login

# تهيئة المشروع
firebase init
```

عند تشغيل `firebase init`، اختر:
- ✅ Firestore
- ✅ Functions
- ✅ Hosting
- ✅ Storage

## 🚀 النشر على Firebase

### بناء المشروع
```bash
cd client
npm run build
```

### النشر
```bash
# من المجلد الجذر
firebase deploy
```

## 🔧 إعداد Firebase Functions (اختياري)

إذا كنت تريد استخدام Firebase Functions بدلاً من الخادم المحلي:

```bash
# إنشاء مجلد Functions
firebase init functions

# تثبيت التبعيات
cd functions
npm install express cors socket.io
```

## 📊 هيكل قاعدة البيانات

### Collections المطلوبة:

#### `users`
```javascript
{
  displayName: "اسم اللاعب",
  email: "email@example.com",
  createdAt: timestamp,
  lastLoginAt: timestamp,
  gamesPlayed: 0,
  gamesWon: 0,
  totalScore: 0,
  level: 1,
  experience: 0
}
```

#### `rooms`
```javascript
{
  hostId: "user-id",
  hostName: "اسم المضيف",
  players: [
    {
      id: "user-id",
      name: "اسم اللاعب",
      isReady: false,
      isHost: true
    }
  ],
  gameState: "waiting", // waiting, playing, finished
  maxPlayers: 4,
  isPrivate: false,
  createdAt: timestamp,
  updatedAt: timestamp
}
```

#### `gameStats`
```javascript
{
  roomId: "room-id",
  players: [
    {
      id: "user-id",
      name: "اسم اللاعب",
      score: 100,
      isWinner: true
    }
  ],
  duration: 1200, // بالثواني
  createdAt: timestamp
}
```

## 🔐 قواعد الأمان

تم إعداد قواعد الأمان في الملفات التالية:
- `firestore.rules` - قواعد Firestore
- `storage.rules` - قواعد Storage

## 🧪 الاختبار المحلي

لاختبار Firebase محلياً:

```bash
# تشغيل Firebase Emulators
firebase emulators:start

# أو تشغيل خدمات محددة
firebase emulators:start --only firestore,auth,storage
```

## 📱 المميزات الجديدة مع Firebase

### 1. المصادقة
- تسجيل دخول بالبريد الإلكتروني
- إنشاء حساب جديد
- دخول كضيف (Anonymous)

### 2. حفظ البيانات
- حفظ إحصائيات اللاعبين
- تاريخ الألعاب
- لوحة المتصدرين

### 3. الاستضافة
- استضافة مجانية على Firebase
- SSL مجاني
- CDN عالمي

### 4. التزامن المباشر
- تحديث البيانات في الوقت الفعلي
- مزامنة حالة اللعبة
- رسائل فورية

## 🔧 استكشاف الأخطاء

### خطأ في الاتصال
```javascript
// تأكد من صحة إعدادات Firebase
console.log(firebaseConfig);
```

### خطأ في قواعد الأمان
```javascript
// تحقق من قواعد Firestore
// تأكد من تسجيل دخول المستخدم
```

### خطأ في النشر
```bash
# تأكد من بناء المشروع أولاً
npm run build

# تحقق من إعدادات firebase.json
```

## 📞 الدعم

إذا واجهت أي مشاكل:
1. تحقق من [وثائق Firebase](https://firebase.google.com/docs)
2. راجع [Firebase Console](https://console.firebase.google.com/)
3. تحقق من وحدة التحكم في المتصفح للأخطاء

---

**ملاحظة**: تأكد من تحديث إعدادات Firebase في ملف `firebase.js` قبل تشغيل المشروع!
