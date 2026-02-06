

# 🌍 Viewport — First Principles Notes

> **Viewport = the visible area of the web page inside the browser window**

Think of the viewport as a **camera** looking at a **large world (web page)**.

---

## 🧠 First Principles Mental Model

### Fundamental Fact

* **Screen** = physical device
  (mobile, laptop, monitor)

* **Web Page** = virtual document
  (can be wider & taller than the screen)

👉 Since the page is often **bigger than the screen**, the browser needs a **window** to show part of it.

🎯 **That window is the viewport**

---

### 🔑 Key Insight

> **The page does NOT move.
> The viewport moves over the page.**

Scrolling = moving the viewport
Not moving the document itself

---

## 🤔 Why Viewport Exists

If viewport didn’t exist:

* Websites would look **tiny on mobile**
* Layouts would **overflow badly**
* Browsers would **zoom randomly**

👉 Viewport **normalizes layout logic** across devices

---

## 📱 Viewport in HTML (Baseline Control)

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

### First-Principles Explanation

#### `width=device-width`

* **Cause**: Mobile browsers used to pretend screens were wide
* **Effect**: Layouts broke
* **Solution**: Set viewport width = real device width

#### `initial-scale=1.0`

* Prevents automatic zooming
* Shows page at **natural scale**

---

## ⚙️ Viewport in JavaScript (Real Power)

JavaScript can **ask questions** about the viewport **at runtime**

---

## 1️⃣ Viewport Size APIs

```js
window.innerWidth   // viewport width
window.innerHeight  // viewport height
```

📌 These are **NOT screen size**
📌 These represent the **visible area only**

---

## 2️⃣ Viewport Position (Scroll APIs)

```js
window.scrollY  // vertical scroll position
window.scrollX  // horizontal scroll position
```

🧠 Meaning:

> “How much has the viewport moved over the page?”

---

## 3️⃣ Viewport Change Detection

```js
window.addEventListener('resize', () => {
  console.log('Viewport changed');
});
```

### Cause → Effect

* User resizes screen / rotates device
* Viewport size changes
* Browser fires `resize` event
* JS reacts (recalculate layout, animations, etc.)

---

## 📦 Element vs Viewport — The Core Question

Most real-world problems reduce to:

> **“Is this element inside the viewport right now?”**

---

## 📐 `getBoundingClientRect()` (Critical API)

### Why it exists

* JS needs element position **relative to the viewport**
* Browser provides coordinates in **viewport space**

```js
element.getBoundingClientRect();
```

### Returned Values

* `rect.top` → distance from **top of viewport**
* `rect.bottom` → bottom edge position
* `rect.left`, `rect.right`

📌 Values change as the viewport scrolls

---

## 🧪 Example — Change Color When Element Enters Viewport

### HTML

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Viewport Example</title>

  <style>
    body {
      height: 200vh;
      margin: 0;
      font-family: Arial;
    }

    .box {
      margin-top: 120vh;
      height: 150px;
      width: 150px;
      background: gray;
      transition: background 0.5s;
    }

    .visible {
      background: green;
    }
  </style>
</head>
<body>

  <h2>Scroll down</h2>
  <div class="box" id="box"></div>

  <script src="script.js"></script>
</body>
</html>
```

---

### JavaScript

```js
const box = document.getElementById('box');

function checkViewport() {
  const rect = box.getBoundingClientRect();
  const viewportHeight = window.innerHeight;

  // Cause → Effect logic
  if (rect.top < viewportHeight && rect.bottom > 0) {
    box.classList.add('visible');
  } else {
    box.classList.remove('visible');
  }
}

window.addEventListener('scroll', checkViewport);
```

---

### 🧠 Logic Breakdown (First Principles)

* `rect.top < viewportHeight`
  → element’s top is above viewport bottom

* `rect.bottom > 0`
  → element’s bottom is below viewport top

👉 **Some part of element overlaps viewport**

✅ Element is visible

---

## 🚀 Real-World Use Cases (All Same Core Idea)

All these features boil down to **viewport visibility**:

* Lazy loading images
* Infinite scrolling
* Sticky headers
* Scroll animations
* Virtual lists
* Ad impression tracking
* Performance optimization

---

## 🧩 Final Mental Model (Remember This)

```
Web Page = Large World
Viewport = Camera
Scroll = Camera Movement
Visibility = Overlap between camera & object
```

Once this clicks, **scroll-related bugs disappear** 😄




## Q1) find the height and width of viewport and document


_**Width and Height of viewport**_

```ts

window.innerWidth  //viewport width
window.innerHeight //viewport height

```

Note :- it will show the visible viewport ares width and height , it includes the scrollbars mostly.

```ts

document.documentElement.clientWidth //viewport width (without scrollbar)
document.documentElement.clientHeight

```
use when scrollbar width matter.


```ts

window.visualViewport.width //viewport width on mobile/zoom
window.visualViewport.height 

```

actual visible are after zoom, changes when keyboard opens on phone. 

Note :- its advance and mobile specific.


_**Width and Height of Document** _


```ts

const doc = document.documentElement;

const documentHeight = doc.scrollHeight;  //height of document 
const documentWidth  = doc.scrollWidth;   //width of document

```

Note :- it measures the total document size, incuding the overflow content.

=> Use this for infinite scroll end detection.


**How much we have scrolled the screen**


```ts

window.scrollY   // vertical scroll
window.scrollX   // horizontal scroll

```

Summary 


```

Viewport size      → innerWidth / innerHeight
Document size      → scrollWidth / scrollHeight
Scroll position    → scrollX / scrollY

```


```ts

function getSizes() {
  const doc = document.documentElement;

  return {
    viewport: {
      width: window.innerWidth,
      height: window.innerHeight
    },
    document: {
      width: doc.scrollWidth,
      height: doc.scrollHeight
    },
    scroll: {
      x: window.scrollX,
      y: window.scrollY
    }
  };
}


```


---

