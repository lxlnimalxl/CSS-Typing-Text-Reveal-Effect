# ✨ CSS Typing / Text-Reveal Effect

A minimal **HTML + CSS** demo that creates a typewriter-like text reveal using a `::before` pseudo-element, `attr(data-text)`, and a width animation (with a blinking caret). Clean, dependency‑free, and easy to customize.

---

## 📸 Preview

The heading reveals the text `lxlnimalxl` from left to right on a dark background with a soft glow.

---

## 🗂 Project Structure

```
index.html   # Markup (h2 with data-text)
style.css    # Styles + keyframes for the reveal effect
```

---

## 🚀 Getting Started

1. Open `index.html` in any modern browser.
2. Edit the heading text in **two places** (for accessibility and fallback):

   ```html
   <h2 data-text="YourText">YourText</h2>
   ```

---

## 🧠 How It Works

* The `<h2>` renders normal text.
* The `::before` pseudo-element duplicates that content via `content: attr(data-text);`.
* The pseudo-element is positioned absolutely over the original text and gets a fixed width that grows from `0` → `100%` to simulate typing.
* A right border acts as the caret, while `drop-shadow` gives a glow.

Key CSS ideas:

```css
h2 {
  position: relative;
  font-size: 6em;
  color: #222;             /* base, hidden under the reveal layer */
}

h2::before {
  content: attr(data-text);
  position: absolute;
  color: #fff;
  overflow: hidden;        /* hide unrevealed characters */
  white-space: nowrap;     /* keep on one line */
  border-right: 4px solid #fff; /* caret */
  animation: reveal 8s linear infinite; /* looping reveal */
  filter: drop-shadow(0 0 20px #fff) drop-shadow(0 0 50px #fff);
}

@keyframes reveal {
  from { width: 0; }
  to   { width: 100%; }    /* grow to full width */
}
```

---

## 🛠 Customization

* **Text**: Change the `data-text` and inner text.
* **Speed**: Adjust `animation-duration` (e.g., `8s`).
* **Caret**: Change `border-right` width/color or add a blink by layering another animation on `opacity`.
* **Glow**: Tweak `drop-shadow` radii and color.
* **Font**: Swap to your preferred family or import from Google Fonts.
* **Background**: Replace the black background with a gradient/image.

Example carets & speeds:

```css
h2::before { border-right: 2px solid #00e5ff; animation: reveal 4s steps(30, end) infinite; }
```

---

## ✅ Accessibility Tips

* Keep inner text in the `<h2>` identical to `data-text` so screen readers read the same content.
* Maintain sufficient contrast between foreground and background.
* Avoid overly long infinite animations that may distract; consider `prefers-reduced-motion`.

```css
@media (prefers-reduced-motion: reduce) {
  h2::before { animation: none; width: 100%; border-right: 0; }
}
```

---

## 🧩 Known Issues & Fixes

If you’re using the supplied starter files, consider these tweaks:

* **Typo:** `white-space: nowarp;` → should be `nowrap;`.
* **Units:** In the keyframes, `width: 100;` needs units → use `100%`.
* **Fixed width:** `width: 190px;` caps the reveal and may cut text. Prefer `width: 100%` inside the animation and let the pseudo-element size itself to content (or set `max-width`).

Suggested corrected block:

```css
h2::before {
  content: attr(data-text);
  position: absolute;
  color: #fff;
  overflow: hidden;
  white-space: nowrap;
  border-right: 4px solid #fff;
  animation: reveal 8s linear infinite;
  filter: drop-shadow(0 0 20px #fff) drop-shadow(0 0 50px #fff);
}
@keyframes reveal { from { width: 0; } to { width: 100%; } }
```

---

## 🧪 Variations to Try

* **Step typing:** `animation-timing-function: steps( N , end);` for choppy, typewriter jumps.
* **Blinking caret:** add `animation: blink 1s step-end infinite alternate;` on a separate caret element or via `box-shadow`.
* **Reverse wipe:** animate `clip-path` or `mask-image` instead of width.

---

## 📄 License

MIT — free to use and modify. If you find this helpful, a ⭐ on your repo is appreciated!
