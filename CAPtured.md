# CAPBOT 💀
**Funny image captions. No mercy. No server. No keys.**

Live at → `https://revati-n.github.io/CAPtured`

---

## What it does

User uploads a photo, picks a humor style, clicks Generate — gets a funny caption. That's it.

No backend. No API calls. No user accounts. No data sent anywhere. Everything runs in the browser.

---

## Deploy in 2 minutes

1. Fork or create a new GitHub repo named `capbot`
2. Drop `index.html` into the root of the repo
3. Go to **Settings → Pages → Source → Deploy from branch → `main` / `/ (root)`**
4. Done. Live at `https://revati-n.github.io/capbot`

---

## How it works

### The model — MobileNet V4 (via Transformers.js)

On page load, the site downloads **MobileNet V4 Conv Small** (~22MB) from Hugging Face's CDN using the [Transformers.js](https://huggingface.co/docs/transformers.js) library. This is an image classification model trained on ImageNet-1k (1000 object/scene classes).

It runs entirely inside the browser using **ONNX Runtime Web** — no GPU needed, works on any modern device. After the first visit, the model is **cached by the browser** so subsequent loads are instant.

When the user clicks Generate:
1. The uploaded image is passed to MobileNet
2. MobileNet returns the **top 10 predicted labels** with confidence scores (e.g. `golden retriever: 0.91`)
3. The top labels + confidence go into the **Humor Engine**

### The Humor Engine (pure JavaScript)

The humor engine is a set of JS functions — one per humor style. It takes the label data and produces a caption using:

- **Template pools** — each style has 12–15 hand-written caption templates with `${noun}` slots filled from detected labels
- **Confidence branching** — if the model is very confident (>75%) or very uncertain (<30%), special templates trigger that play with that uncertainty
- **Randomness** — `pick()` randomly selects from the pool so the same image gives different captions on retry
- **Label cleaning** — ImageNet labels like `"golden_retriever, dog, canine"` get cleaned to just `"golden retriever"`

### The 4 styles

| Style | Voice | Example |
|-------|-------|---------|
| 🥶 **Dry** | Deadpan. Matter-of-fact. Zero enthusiasm. | `"a dog. just sitting there. being a dog. breathtaking."` |
| 🔥 **Unhinged** | Capslock energy. Chaotic. Existentially distressed. | `"WAIT. IS THAT A DOG?? NO. NO NO NO. I AM NOT OKAY."` |
| 😈 **Sarcastic** | Condescending. Roast mode. Fake impressed. | `"oh wow. a dog. i've never seen one of those before. truly revolutionary content."` |
| 🧠 **Brainrot** | Chronically online Gen Z. Sigma. Rizz. No cap. | `"this dog is lowkey giving main character energy no cap fr fr"` |

---

## File structure

```
capbot/
├── index.html    ← The entire app. One file.
└── README.md     ← This file.
```

That's it. One file does everything.

---

## Customising the humor engine

All caption logic is inside `index.html` in the `<script type="module">` block.

### Adding or editing templates

Find the function for the style you want:

```js
function dryCaption(n, n2, n3, conf, hi, lo) {
  const templates = [
    `a ${n}. just sitting there. being a ${n}. breathtaking.`,
    // ← add your own templates here
  ];
  return pick(templates);
}
```

Variables available in every template:
- `n` → top detected label (e.g. `"dog"`)
- `n2` → second label
- `n3` → third label
- `conf` → confidence score (0 to 1)
- `hi` → true if confidence > 75% (model is sure)
- `lo` → true if confidence < 30% (model is guessing)

### Adding a new humor style

**1. Add the button in the style grid:**
```html
<button class="style-btn" data-s="villain">
  <span class="s-emoji">🦹</span>
  <span class="s-name">Villain Era</span>
  <span class="s-desc">No remorse.</span>
</button>
```

**2. Add CSS for the active state:**
```css
.style-btn.active[data-s="villain"] {
  border-color: #9b00ff;
  color: #9b00ff;
  background: #0d0014;
}
```

**3. Add the caption function:**
```js
function villainCaption(n, n2, n3, conf, hi, lo) {
  const templates = [
    `the ${n} has been located. phase one is complete.`,
    `i did not choose the ${n} life. the ${n} life chose me.`,
  ];
  return pick(templates);
}
```

**4. Wire it up in `buildCaption()`:**
```js
case 'villain': return villainCaption(n, n2, n3, conf, veryConfident, uncertain);
```

---

## Known limitations

- **MobileNet is a classifier, not a scene understander.** It identifies dominant objects well but doesn't understand relationships, emotions, or context. The humor engine is designed to work with whatever labels come out — including weird or unexpected ones.
- **Abstract images** (memes, screenshots, artwork) may return low-confidence labels. The engine has fallback templates specifically for uncertain detections.
- **First load** requires ~22MB download. Cached by the browser after that — instant on return visits.
- **Best on Chrome / Edge** (WebGPU support speeds up inference). Works on Firefox too via WASM fallback, just slightly slower.

---

## Tech stack

| Thing | What |
|-------|------|
| Model | MobileNet V4 Conv Small (ImageNet-1k, ~22MB) |
| Inference | ONNX Runtime Web via Transformers.js |
| Model source | Hugging Face CDN |
| Frontend | Vanilla HTML + CSS + ES Module JS |
| Hosting | GitHub Pages (free) |
| Backend | None |
| Data sent anywhere | Nothing |

---

