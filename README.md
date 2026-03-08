# 🎤 יקיר כהן Productions — Voucher Engine

מערכת שוברי מתנה דיגיטליים. שני קבצי HTML, ללא backend, מוכן להעלאה ל-GitHub + Cloudflare Pages.

---

## 📁 מבנה הקבצים

```
yakir-voucher/
├── admin.html      ← ממשק ניהול (ליקיר בלבד)
├── voucher.html    ← ממשק לקוח (נשלח ללקוחות)
├── _headers        ← Cloudflare headers (iframe + security)
├── _redirects      ← Cloudflare redirects
└── README.md
```

---

## ⚙️ הגדרות ראשוניות (שנה לפני העלאה)

### `admin.html` — שורה 1 בסקריפט:

```javascript
const ADMIN_PASS = 'yakir2026';         // ← סיסמת כניסה לממשק ניהול
const PAY_LINKS = {
  basic:  'https://...',                // ← לינק חשבונית ירוקה — בסיס ₪990
  silver: 'https://...',                // ← לינק חשבונית ירוקה — Silver ₪1,480
  vip:    'https://...',                // ← לינק חשבונית ירוקה — VIP ₪2,380
};
const WA_NUMBER = '972501234567';       // ← מספר הווטסאפ שלך
```

### `voucher.html` — שורה 1 בסקריפט:

```javascript
const WA_YAKIR = '972501234567';        // ← מספר הווטסאפ שלך (ללא +)
```

---

## 🚀 העלאה ל-Cloudflare Pages

### אופציה א' — Direct Upload (הכי מהיר):
1. היכנס ל-[Cloudflare Dashboard](https://dash.cloudflare.com) → Pages → Create Project
2. בחר **"Direct Upload"**
3. גרור את **כל 5 הקבצים** יחד
4. Build settings: השאר ריק (סטטי לחלוטין)
5. לחץ **Deploy**

### אופציה ב' — דרך GitHub (לעדכונים קלים בעתיד):
1. צור ריפו חדש: `yakir-voucher`
2. העלה את הקבצים
3. ב-Cloudflare Pages: **Connect to Git** → בחר את הריפו
4. הגדרות build: הכל ריק, Output directory: `/`

### הגדרת Subdomain:
```
Pages Project → Settings → Custom Domains:
  voucher.yakircohen.com
```
Cloudflare יפעיל SSL אוטומטית ✅

---

## 🔄 זרימת עבודה יומיומית

### 1. יוצרים שובר:
```
admin.html → בחר עיצוב → מלא פרטים → כתוב מכתב → בחר חבילה
```

### 2. שולחים לתשלום:
```
לחץ "שלח לתשלום" → נפתח חשבונית ירוקה ← לקוח משלם
```

### 3. מאשרים תשלום:
```
חזור ל-admin → לחץ "אשר — שולם בכרטיס" → נוצרת סיסמה: NOY-2026-K4X
```

### 4. שולחים ללקוח:
```
לחץ "שלח בWA" → הלקוח מקבל: קישור + סיסמה
```

### 5. לקוח פותח:
```
voucher.html → מזין סיסמה → פתח את המכתב → קורא → תואם סשן בוויז
```

### 6. אחרי הסשן (אופציונלי):
```
admin.html → הוסף תמונות + הקלטה סופית → עדכן קישור → לקוח רואה גלריה
```

---

## 🎤 Speech to Text

בממשק ניהול, לחץ על כפתור 🎤 ליד שדה המכתב.
- עובד ב-Chrome/Edge בלבד
- שפה: עברית (he-IL)
- מקליט בצורה רציפה עד שלוחצים שוב
- טקסט מצטבר ישירות בשדה המכתב
- בצד הלקוח מוצג כ"בועת דיבור" מעוצבת אם הטקסט מסומן עם 🎤:

```javascript
// בממשק הניהול, אם רוצים לסמן שהברכה הוקלטה בקול:
// הוסף 🎤: בתחילת הטקסט לפני הקידוד
```

---

## 💳 הגדרת לינקי תשלום

### חשבונית ירוקה:
1. היכנס ל-[invoiceguru.co.il](https://invoiceguru.co.il)
2. צור 3 מוצרים: בסיס (₪990), Silver (₪1,480), VIP (₪2,380)
3. הפק לינק תשלום לכל אחד
4. הדבק ב-`PAY_LINKS` ב-admin.html

### ניסוח הודעת WhatsApp לתשלום:
```
שלום! 😊

הכנתי עבורך שובר הקלטה מיוחד באולפן יקיר כהן הפקות.

🎤 חבילת Silver — ₪1,480
📍 עמק איילון 34, מודיעין

לתשלום מאובטח ונוח:
💳 ויזה | ישראכרט | מסטרקארד
📱 Bit | PayBox
🔵 PayPal
🏦 העברה בנקאית | צ'ק
🍎 Apple Pay | 🤖 Google Pay

👇 לחץ על הקישור ומלא פרטים —
תדע בדיוק על מה אתה משלם:
[לינק חשבונית ירוקה]
```

---

## 🌐 הטמעה ב-Google Sites

```
Insert → Embed → URL:
https://voucher.yakircohen.com/voucher.html?data=DATA&embedded=true
```

**חשוב:** `?embedded=true` מסיר padding מיותר ומתאים לגובה iframe.

### Iframe Height Auto-resize:
הוסף סקריפט קטן בדף Google Sites (דרך Embed HTML):
```html
<script>
window.addEventListener('message', function(e) {
  if (e.data && e.data.frameHeight) {
    document.querySelector('iframe').style.height = e.data.frameHeight + 'px';
  }
});
</script>
```

---

## 🔐 אבטחה

| פיצ'ר | מצב |
|--------|------|
| admin.html — סיסמה | ✅ שנה את `ADMIN_PASS` |
| voucher.html — סיסמה חכמה | ✅ NOY-2026-K4X |
| נתונים ב-URL בלבד | ✅ אין localStorage |
| HTTPS | ✅ Cloudflare SSL אוטומטי |
| iframe מותר ב-Google Sites | ✅ מוגדר ב-_headers |
| admin לא ניתן להטמעה | ✅ אין X-Frame-Options ב-admin |

---

## 📱 תמיכה בדפדפנים

| | Chrome | Firefox | Safari | Edge |
|--|--|--|--|--|
| voucher.html | ✅ | ✅ | ✅ | ✅ |
| admin.html | ✅ | ✅ | ✅ | ✅ |
| Speech-to-Text | ✅ | ❌ | ❌ | ✅ |
| Haptic Feedback | ✅ נייד | — | ✅ | — |

---

## 🔧 פתרון בעיות

**Q: Google Drive לא מנגן?**
A: ודא שהקובץ שיתוף הוא "כל מי שיש לו קישור". המרה ל-`/uc?export=download` אוטומטית.

**Q: הסיסמה לא עובדת?**
A: הסיסמה case-insensitive. ודא שהלינק הנכון נשלח עם הסיסמה הנכונה מאותו שובר.

**Q: ה-iframe ב-Google Sites חתוך?**
A: ב-Sites, לחץ על ה-embed → Resize → הגדל גובה ידנית, או השתמש בסקריפט ה-postMessage למעלה.

**Q: Speech-to-Text לא עובד?**
A: עובד רק ב-Chrome/Edge. ודא שהאתר בהttps (Cloudflare מטפל בזה).

---

Built with ❤️ for Yakir Cohen Productions
