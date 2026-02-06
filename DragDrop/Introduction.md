## 1️⃣drag and drop

drag & drop is just mouse (or pointer) movement + state.


==> User pressed mouse → moved mouse → released mouse

## 2️⃣ Two ways to implement Drag & Drop in JS

### A) Native HTML5 Drag & Drop API

Uses browser-provided drag events

Good for file drag, simple UIs

❌ Hard to customize visuals

❌ Weird edge cases

### B) Manual Drag (Mouse / Pointer Events)

You move elements yourself

Used in real apps (Trello, Figma, whiteboards)

✅ Full control

✅ Predictable


## PART A — Native HTML5 Drag & Drop API

3️⃣ Mental model of Native Drag & Drop

Browser gives you:

1. A draggable element

2. A data carrier

3. A drop target


Browser handles:

Mouse tracking

Ghost image

Drag lifecycle

You handle:

What data moves

Where it can be dropped

What happens on drop

Core drag & drop lifecycle

dragstart → drag → dragenter → dragover → dragleave → drop → dragend


| Event     | Meaning                 |
| --------- | ----------------------- |
| dragstart | User started dragging   |
| drag      | Mouse is moving         |
| dragenter | Entered a drop zone     |
| dragover  | Hovering over drop zone |
| dragleave | Left drop zone          |
| drop      | Released mouse          |
| dragend   | Cleanup                 |



<div id="box" draggable="true">Drag me</div>
<div id="zone">Drop here</div>
















