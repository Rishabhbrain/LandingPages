# NexOps Consulting — Demo Landing (Light/Dark + Assistant)

![Made with](https://img.shields.io/badge/Made%20with-HTML%20%2B%20Tailwind%20%2B%20JS%20%2B%20Three.js-7C4DFF?style=for-the-badge)
![No build step](https://img.shields.io/badge/Build-None%20\(Play%20CDN\)-10B981?style=for-the-badge)
![License](https://img.shields.io/badge/license-MIT-222?style=for-the-badge)

A modern, single‑file demo site for an **operations/supply‑chain consulting** brand. It focuses on *useful* interactions (not just visuals): ROI calculator with CSV export, cycle‑time reduction visual with recommendations, a **Supply Chain Risk Monitor** (Three.js), a **floating chat assistant**, testimonials, “Why Us” proof‑point accordions, and a persistent **Light/Dark** mode toggle.

Live preview friendly — open `index.html` in any browser.

---

## ✨ Why this exists (Thought Process)

> Consultants often ship brochure sites full of static “capabilities.” Operators want *signals*: **time saved**, **money saved**, and **risk surfaced**. This demo swaps pretty noise for interactive proof.

**Design bets**

* **Value in < 10s**: ROI & cycle‑time tools are above the fold.
* **From glossy to *useful***: The hero WebGL is repurposed into a *Risk Monitor* with geographic alerts (pins) to start a real conversation.
* **No symmetric card grid**: Asymmetric **bento** layout creates motion and hierarchy without carousels.
* **Proof > claims**: “What makes us stand out” is an accordion with verifiable details/actions.
* **Conversion ready**: Floating assistant pre‑fills the contact form; micro‑analytics track intent locally until GA4 is wired.
* **Low friction**: No bundler; everything runs from a static file. Perfect for GH Pages.

---

## 🧭 Table of Contents

* [Features](#-features)
* [UI/UX Decisions](#-uiux-decisions)
* [Tech Stack](#-tech-stack)
* [Getting Started](#-getting-started)
* [Customization](#-customization)
* [Implementation Notes](#-implementation-notes)
* [Screenshots](#-screenshots)
* [Roadmap](#-roadmap)
* [Deployment](#-deployment)
* [License](#-license)

---

## 🔥 Features

* **Hero → Supply Chain Risk Monitor**

  * Lightweight Three.js globe (wireframe + glow) with geolocated **risk pins** and a **7‑day alert list**.
* **ROI / Payback Calculator**

  * Instant monthly savings, annualized ROI, payback months.
  * **CSV export** of the last run.
* **Cycle‑Time Reduction Visual**

  * Dual bars + delta **and** a dynamic **recommendation** message.
* **Engagement Analytics (local)**

  * Tracks CTA clicks, calculator runs, session seconds and draws a live **sparkline**.
* **“Why Us” Proof Accordions**

  * Click to reveal real process details and actionable links.
* **Testimonials**

  * Speech‑bubble styling (no repetitive card grids).
* **Contact Form (demo)**

  * Client‑side success message; ready to wire to Formspree/backend.
* **Floating Chat Assistant**

  * Rule‑based responses for ROI/cycle‑time; auto‑captures email and pre‑fills the contact form.
* **Light/Dark Mode**

  * Navbar toggle; **persisted in `localStorage`**.
* **Micro‑interactions**

  * Magnetic buttons, morphing blobs, subtle noise texture.

---

## 🧩 UI/UX Decisions

* **Asymmetric Bento Layout**: Services are arranged in different spans/rotations for energy and scannability — no uniform “cards.”
* **Color System**: Electric violet brand, cyan/amber/emerald accents, tuned for both dark and light surfaces.
* **Typography**: Plus Jakarta Sans + Inter for clarity at large and small sizes.
* **Clarity over gimmicks**: Animations are slow and purposeful, with emphasis on legibility and content hierarchy.
* **Accessibility**: High‑contrast text tokens for light/dark, keyboard focus on inputs, semantic headings; client‑side only, so no flashing or heavy motion.

---

## 🛠 Tech Stack

* **HTML**: single file, semantic sections.
* **Tailwind (Play CDN)**: utility classes + in‑page `tailwind.config` for colors, fonts, animations.
* **Vanilla JavaScript**: calculators, analytics, chat, mode persistence.
* **Three.js**: `0.160.x` for the globe and risk pins.
* **No build step**: Works on any static host (GitHub Pages/Netlify/Vercel static export).

---

## 🚀 Getting Started

```bash
# 1) Clone
git clone https://github.com/<you>/nexops-consulting-demo.git
cd nexops-consulting-demo

# 2) (Optional) serve locally
# macOS/Linux
python3 -m http.server 5500
# Windows
py -m http.server 5500

# 3) Open in your browser
open http://localhost:5500/index.html   # macOS
# or just double‑click index.html
```

> **Tip:** It’s a single `index.html`. Drop it into any static host and you’re live.

---

## 🎨 Customization

### Branding (name + copy)

Search and replace **“NexOps Consulting”** and update hero/section copy.

### Colors / Theme

Inside the inline Tailwind config:

```js
colors: {
  ink: { /* light & dark scales */ },
  brand: { DEFAULT:'#7C4DFF', 2:'#22D3EE', 3:'#F59E0B', 4:'#10B981' }
}
```

### Light/Dark default

```js
// set default
const savedMode = localStorage.getItem('nexops-mode') || 'dark';
setMode(savedMode);
// change 'dark' → 'light' if you want to start in light mode
```

### Add/Edit Risk Pins

```js
const risks = [
  { lat: 19.07, lon: 72.87, label: 'Mumbai Port Congestion', level: 'High' },
  { lat: 51.51, lon: -0.13, label: 'UK Customs Delay', level: 'Med' },
  // add yours here
];
```

* `level: 'High' | 'Med'` controls pin color.
* Pins auto‑render on the globe **and** in the alert list.

### ROI Calculator: Currency / Locale

```js
const fmt = (n) => new Intl.NumberFormat('en-IN').format(Math.round(n));
// swap en-IN for your locale
```

### Hook up Forms & Analytics

* **Formspree**: replace the `submit` handler with a `fetch` POST.
* **GA4**: uncomment the snippet at the bottom and add your measurement ID.
* **Chat → LLM**: replace the rule engine with a `fetch('/api/chat', { ... })` call.

---

## 🧪 Implementation Notes

### Three.js Globe

* Wireframe sphere + soft glow, animated Y‑rotation.
* Geo pins are converted via `latLonToVec3` to sphere coordinates.
* Chosen for **low GPU overhead** and clarity (no textures/tiles).

### Calculators

* ROI uses baseline cost × improvement to compute monthly savings, then annualized ROI/payback.
* Cycle‑time shows relative bars and emits a *recommendation* tiered on improvement %.
* Latest ROI run can be exported to CSV for email follow‑ups.

### Assistant (Demo)

* Rule‑based (regex) for *fast response* and zero backend.
* Email regex auto‑fills the contact form to reduce friction.

### Local Micro‑Analytics

* CTA clicks, calc runs, session seconds, and a canvas sparkline (no external deps). Replace with GA4 when deploying.

---

## 🖼 Screenshots

> Add screenshots/GIFs into `/screenshots` and reference them here.

* Hero with **Risk Monitor**
* ROI Calculator with **CSV Export**
* Cycle‑time **Recommendations**
* **Light/Dark** comparison
* Floating **Chat Assistant**

---

## 🗺 Roadmap

* [ ] Real data feed for Risk Monitor (ports, weather, supplier events).
* [ ] GA4 events + dashboard template.
* [ ] Chat assistant → serverless LLM endpoint.
* [ ] Accessibility pass for `prefers-reduced-motion`.
* [ ] Unit tests for calculators.

---

## ⬆️ Deployment

### GitHub Pages (no build)

1. Rename file to `index.html` at repo root.
2. Settings → Pages → Deploy from Branch → `main` / root.
3. You’re live at `https://<you>.github.io/<repo>/`.

### Netlify / Vercel

* New Project → Import repo → Framework preset **None** → Deploy.

---

## 📄 License

MIT © \[Your Name]

---

### Credits / Inspiration

* **UI patterns**: Bento blocks, morphing blobs, micro‑interactions inspired by community components (e.g., uiverse.io)
* **Type**: Plus Jakarta Sans, Inter
* **Stack**: Tailwind, vanilla JS, Three.js

> If this saved you time or gave you ideas, ⭐ the repo. It helps others find it and tells me to keep shipping more utilities like this.
