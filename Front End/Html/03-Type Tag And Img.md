## 1) نوعين من الـ Tags

- ال **Paired / Normal tags (ليها فتح وقفل):**

```html
<div>...content...</div>
```

- ال **Void / Self-closing tags (ملهاش قفل — عناصر فارغة):**

```html
<br> 

<hr> 

<img>
```

- في **HTML5** السلاش الأخير اختياري: تقدر تكتب :

```html
<img src="..." alt="">
```

أو

```html
<img src="..." alt="" />
```

> (في XHTML السلاش مطلوب).

---

## 2) الـ `img` والعناصر المرتبطة بيها (Attributes)

- الصيغة الأساسية :

```html
<img src="images/photo.jpg" alt="وصف موجز للصورة" />
```

- ال**`src`**: مسار الصورة (relative أو absolute).  
    
- ال**`alt`**: نص بديل للـ SEO ولـ screen readers؛ يظهر لو الصورة ما اتحملتـش.  
    
- ال**`title`**: بقايا نص تظهر كـ tooltip عند المرور بالفأرة (مش بديل للـ alt).  
    
- ال**`loading="lazy"`**: تحميل كسول (يدعم تقليل وقت تحميل الصفحة).  
    
- ## ال**`width` و `height`**: من الأفضل تضمينهم (أو استخدام CSS `aspect-ratio`) لتقليل **Cumulative Layout Shift**.
    

## 3) لو حطيت **أكثر من `src`** في نفس الوسم

```html
<img src="a.jpg" src="b.jpg" alt="...">
```

- هذا **غير صحيح/غير صالح** طبقًا للـ HTML (duplicate attributes). سلوك المتصفح غير مضمون — لا تعتمد على ده.  
    
- الحل الصحيح لو عايز صور مختلفة لأحجام أو دقات مختلفة هو استخدام **`srcset`/`sizes`** أو عنصر `<picture>`.

---

## 4) ال `srcset` و `<picture>` (لـ responsive / art direction)

**مثال `srcset`**

```html
<img 
  src="images/photo-800.jpg"
  srcset="images/photo-400.jpg 400w, images/photo-800.jpg 800w, images/photo-1600.jpg 1600w"
  sizes="(max-width:600px) 100vw, 600px"
  alt="شاب يبتسم أمام لابتوب"
  loading="lazy"
  width="800" height="533"
/>
```

**مثال `<picture>`** (لو عايز صيغة مختلفة أو صورة موجهة لعرض معين):

```html
<picture>
  <source media="(max-width:600px)" srcset="images/photo-small.jpg">
  <source type="image/webp" srcset="images/photo.webp">
  <img src="images/photo.jpg" alt="شرح الصورة" loading="lazy">
</picture>
```

---

## 5) الترتيب والـ `alt` والـ SEO

- **الترتيب بين attributes** (مثل `alt` قبل `src`) **مش مهم تقنيًا** — المتصفحات تقرأها كلها. لكن للوضوح والقراءة البشرية يفضّل وضع `src` ثم `alt`.  
    
- **كتابة الـ `alt`:**
    - هدفه: وصف محتوى الصورة للمستخدم الذي لا يرى الصورة + لمحركات البحث.  
        
    - كن **موجزًا ووصفياً** (مثال جيد: `"شخص يكتب كود على لابتوب في مكتب منزلي"`).  
        
    - لو الصورة دي للزينة فقط: استخدم `alt=""` (فارغ) أو `role="presentation"` عشان لا يزعجها القارئ الصوتي.  
        
    - لا تضع كلمات مفتاحية بشكل مبالغ فيه — اكتب وصف طبيعي.  
        
    - **طول مناسب:** لا قاعدة صارمة، لكن حاول تظل موجز (عدة كلمات — 5–15 كلمة عموماً)؛ بعض الأدلة تشير إلى أن أقل من ~125 حرف أفضل للشاشات المساعدة.

---

## 6) مسارات الصور (Paths)

- **Relative (نسبية):**
    - `images/photo.png` → من نفس مكان ملف الـ HTML (أو حسب بنية المشروع).  
        
    - `./images/photo.png` → نفس الدليل.  
        
    - `../images/photo.png` → ادخل مجلد واحد لفوق ثم images.  
        
- **Root-relative:** `/assets/images/photo.png` → من جذر السيرفر.  
    
- **Absolute URL:** `https://example.com/images/photo.png`  
    
- **مهم:** استخدم `/` (forward slashes) في الـ URLs، لا تستخدم backslashes `\`.

---

### 7) بنية المجلد المقترحة

```pgsql
MyProject/
  index.html
  css/
    style.css
  js/
    app.js
  images/    <-- حط كل الصور هنا
    logo.png
    hero.jpg
```

- يسهّل التنظيم والصيانة. تقدر تستخدم `assets/images/` لو بتحب تفصل assets.

---

### 8) قواعد اسم الملف للصور (Best practices)

- استخدم أحرف صغيرة، و`-` للفصل: `profile-picture.jpg`  
    
- تجنّب الفراغات و الحروف الخاصة.  
    
- اسم معبّر يساعد SEO: `red-running-shoes.jpg` أحسن من `IMG_1234.jpg`.

---

### 9) أمثلة على `alt` جيدة وسيئة

- سيء: `alt="image1"` أو `alt=" "`  
    
- جيد: `alt="طفل يقرأ كتابًا في مكتبة المدرسة"`  
    
- للزينة: `alt=""` (وهذا يخبر القارئ الصوتي أنه لا يحتاج لذكرها)

---

### تلميحات سريعة (VSCode)

- اضغط **Ctrl + Space** أثناء كتابة `src="` عشان يظهر لك اقتراحات المسارات (IntelliSense).  
    
- اختصار Emmet: اكتب `img` ثم اضغط `Tab` لتوليد `<img src="" alt="">` تلقائيًا. مفيد جدًا.