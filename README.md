# CAPTURED ⚡

**AI-powered funny image caption generator. Upload a photo, pick a vibe, get a caption that actually describes what's in it — not a generic template.**

🔗 **Try it live → [https://revati-n.github.io/CAPtured/](https://revati-n.github.io/CAPtured/)**

---

## Before you start — get your free API key

CAPSHUNNED runs entirely in your browser. It uses Google's Gemini AI to read your image, which means you need a (free) API key to use it. This sounds scarier than it is.

**Here's how:**

1. Go to **[aistudio.google.com/apikey](https://aistudio.google.com/apikey)**
2. Sign in with any Google account
3. Click **"Create API Key"**
4. Copy it

That's genuinely it. No credit card. No subscription. Google gives you **500 free requests per day** on this key.

> Your key is saved in your own browser only — it never goes to any server, including mine. The app has no backend at all.

---

## Using the app

### step 1 — paste your key
At the top of the page, paste your Gemini API key into the input box and hit **SAVE KEY**. You'll only need to do this once — it stays saved in your browser.

### step 2 — upload your image
Drag and drop any image onto the upload zone, or click it to browse. JPG, PNG, WEBP, GIF all work. If you want to swap the image later, hit the **⟳ REPLACE IMAGE** button in the corner of the preview.

### step 3 — configure your caption

You have three things to set:

**Humor style** — this controls what kind of funny:
| Style | What you get |
|---|---|
| Brain rot | Gen-Z chaos. "bro really said this is fine and meant it" |
| Deadpan | Dry, unbothered, slightly judgemental |
| Roast | Genuinely savage. Don't say we didn't warn you |
| Wholesome | Silly but kind. Good for group chats |
| Dad jokes | Pun-based, tied to what's actually in the image |

**Tone** — this controls the *energy* of the caption:
- **Chaotic** — internet brain, no filter
- **Corporate** — written like a LinkedIn post gone wrong
- **Dramatic** — cinematic, everything is a moment
- **Chill** — unbothered, one eyebrow raised
- **Unhinged** — conspiracy mode, connecting dots that don't exist

**Length** — slider from Micro to Epic:
- **Micro** → 3 words max
- **Short** → half a tweet
- **Medium** → one solid one-liner
- **Long** → two sentences, the second undercuts the first
- **Epic** → 3–4 sentences that escalate in absurdity

### step 4 — hit the button
Click **▶ CAPSHUN THIS IMAGE** and wait a second or two. You'll get:
- One main caption (typed out dramatically)
- Three alternate captions below it

Click any alternate to swap it in as the main. Hit **COPY ↗** to copy to clipboard.

---

## Tips for better captions

- **Weirder images = funnier captions.** The AI has more to work with when something unusual is happening in the frame.
- **Mix styles and tones.** Dad jokes + Corporate tone is a surprisingly good combo.
- **Micro length + Roast** is lethal for single-subject photos.
- **Epic length + Unhinged** for group photos. Trust.
- If the first result is mid, just hit the button again — temperature is set high so you'll get something different each time.

---

## Something went wrong?

| Error | Fix |
|---|---|
| *Invalid API key* | Double-check you copied the full key from aistudio.google.com |
| *Rate limit hit* | You've hit 10 requests/minute. Wait 60 seconds and try again |
| *Empty response* | Try a different image, or regenerate — occasional API hiccup |
| *Model not found* | Rare — reload the page and try again |

If your daily limit of 500 runs out, it resets at midnight Pacific Time.

---

## Privacy

- Your image goes from your browser → directly to Google's Gemini API. It doesn't pass through any server I own.
- Your API key is stored in your browser's `localStorage`. It's not transmitted anywhere except to Google when you generate a caption.
- There are no cookies, no analytics, no tracking on this site.

On the free API tier, Google may use inputs to improve their models. If that's a concern, you can upgrade to a paid Gemini tier directly with Google — but for captioning memes, it's genuinely not something to worry about.

---
