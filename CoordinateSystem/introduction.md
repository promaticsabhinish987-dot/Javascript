
# 3 types of coordinate systems in JavaScript (screenX,clientX,pageX)

1. Screen coordinates (screenX, screenY)
- from top left corber of `Computer Screen`
2. Window coordinates (clientX,clientY)
- from top left corner of the `browser window`
3. Document coordinates (pageX,pageY)
- from top left corner of `HTML document`
4. getBoundingClientRect() and elementFromPoint(x,y) to obtain coordinates.
- its a element coordinate 


we can get the position of an element on the screen relative to the screen or window or document


**1. A️⃣ Element position relative to VIEWPORT**

```ts

const rect = box.getBoundingClientRect();

rect.left   // clientX space
rect.top
rect.right
rect.bottom

```

Note :- ViewPort is the visible part of the screen.

**2. B️⃣ Element position relative to DOCUMENT**


```ts

const rect = box.getBoundingClientRect();

const docX = rect.left + window.scrollX;
const docY = rect.top  + window.scrollY;

```
Now we have page coordinate.

Note :- document is the full html page that we can scroll,and its the child of the viewport

**3. C️⃣ Element position relative to SCREEN**

```ts

const rect = box.getBoundingClientRect();

const screenX = rect.left + window.screenX;
const screenY = rect.top  + window.screenY;

```

Note: rarely needed , but possible , it includes the tab of os screen.



```
SCREEN (physical monitor)
┌─────────────────────────────┐
│  Browser Window             │
│  ┌─────────────────────┐   │
│  │  VIEWPORT            │   │
│  │  (clientX/Y)         │   │
│  │   ┌─────────────┐   │   │
│  │   │  DOCUMENT    │   │   │
│  │   │  (pageX/Y)   │   │   │
│  │   └─────────────┘   │   │
│  └─────────────────────┘   │
└─────────────────────────────┘

```


![Coordinate Systems Diagram](https://i.sstatic.net/qP6La.png)


## Example of each start from ViewPort.

Viewport = the visible window into the document

Controlling the viewport means:

Changing **what part of the document is visibl**e

Changing **how big that visible area is**

Changing **how content is scaled inside it**

You are **not moving elements —**
you are **moving or reshaping the camera** that looks at them 🎥


#### Why do we want to control the viewport

A) Scrolling the viewport (most common)
B) Resizing the viewport

```ts

window.addEventListener('resize', () => {
  console.log(window.innerWidth, window.innerHeight);
});

```
- for responsive layout
- for recalculate positions
- canvas resizing

C) Zooming (scaling the viewport)

```ts

<meta name="viewport" content="width=device-width, initial-scale=1">

```

element --> document (bigger then viewPort) --> viewPort (camera on document)


**Viewport is the camera
Document is the world
Elements are objects in the world**




















