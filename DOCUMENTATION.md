# Ummay Salma — Portfolio Website (Soft Beige & Editorial theme)

Single-page portfolio: `ummay_salma_portfolio_editorial.html` (HTML + CSS + JavaScript in one file, no build step, no libraries).
Same content and features as the dark version; only the design changed.
Last updated: 1 November 2026.

**Concept:** Elegant, warm and sophisticated — it should feel like a modern design magazine.

---

## 1. Files in this folder

| File | What it is |
|---|---|
| `ummay_salma_portfolio_editorial.html` | The website. Open in any browser to preview (internet needed for the fonts, see §4). |
| `google-apps-script.gs` | Optional script that saves form questions to Google Sheets / Google Docs (see §9, Option B). Not part of the website itself. |
| `DOCUMENTATION.md` | This guide. |

---

## 2. Design system

### 2.1 Colour palette

| Role | Hex | Where it is used |
|---|---|---|
| Background | `#F7F3ED` | Page background, input fields, small chips |
| Primary | `#292824` | Headings, main buttons, logo outline, strong lines, "In progress" badge |
| Secondary | `#E8DFD2` | About section panel, Contact panel, image placeholders, tags on hover |
| Accent | `#B96E50` | Italic highlight words in headlines, dots, circles, link underline on hover |
| Text | `#66615B` | Body text |

**Derived shades** (made from the palette, so nothing off-brand was added):

| Name | Hex | Why it exists |
|---|---|---|
| Accent ink | `#9A5439` | A darker accent for **small** text (labels, kickers, button hover). `#B96E50` on cream has a contrast of about 3.5:1, which is fine for large headlines but too low for small text; `#9A5439` reaches about 5:1. |
| Surface | `#FBF8F3` | Slightly lighter cream for the contact form card, email card and the project pop-up, so they lift off the beige. |
| Lines | primary at 13% / 28% opacity | Hairline rules and outlines. |
| Error / Success | `#A33A2B` / `#4C6B3C` | Form messages only. |

All colours are CSS variables at the top of the `<style>` block (`:root`). Change them there and the whole site follows.

### 2.2 Typography

| Use | Font | Notes |
|---|---|---|
| Headlines, logo, project titles, big numbers | **Instrument Serif** (regular + italic) | Elegant editorial serif. It has **no bold** weight, so do not make headlines bold. Italic + accent colour is the highlight style (e.g. *matter.*). |
| Body text, buttons, labels, navigation | **Inter** (400 / 500 / 600 / 700) | Clean sans-serif. Small uppercase labels use wide letter-spacing. |

Fonts load from Google Fonts (`<link>` in `<head>`). If a visitor is offline or the request is blocked, the page falls back to **Georgia** (serif) and the system sans-serif — it still works, just looks slightly different. To change a font, replace the names in the `<link>` and in the `--serif` / `--sans` variables.

### 2.3 Layout and shape

- **Editorial grid:** Work uses a 12-column grid. Cards alternate wide (7 columns) and narrow (5 columns) — wide / narrow on the first row, narrow / wide on the second — and the right-hand cards sit 110 px lower. This staggered rhythm is what gives the magazine feel. On phones it becomes one column.
- **Big thumbnails:** every project cover is 4:3, with a rounded 28 px container.
- **Rounded image containers:** hero and About images use a 36 px radius; panels (About, Contact) 48–56 px; buttons and tags are pills.
- **Cream and beige rhythm:** the page is cream; About and Contact sit on beige panels so the page changes "paper" as you scroll.
- **Details:** a very light paper-grain texture over the background; hairline rules instead of boxes; numbered projects (01 / 04).

### 2.4 Sections, top to bottom

Header (logo + navigation) → Hero → "Areas I love working on" strip → **Work** (4 projects) → **About** → **Process** (5 steps) → **Skills** → **Contact** (email + form) → Footer.

---

## 3. What is included (same as the dark version)

- Logo: typographic "US" monogram (circle, upright **U** + italic accent **S**) with an option to use a logo image
- Designation: **Product Designer · UI & UX Designer · Graphic Designer**
- Areas I love working on: **Mobile Apps · Product Design · Web Experiences · UX Research**
- StockFlow marked **In progress** (badge on the cover + status in the pop-up)
- Project pop-up with a highlighted Behance button for each project (StockFlow: "Check out my other projects")
- Email `salmamonowara@gmail.com` with a Copy button
- **Have any question?** form (Name, Email, Message) → your email, and optionally Google Sheets / Docs
- Working **Back to top** (footer, Contact section and logo)
- Image slots for the hero, About and every project cover
- Responsive design (desktop, tablet, phone), keyboard-friendly, respects "reduce motion"

New in this version: clicking a **project thumbnail** also opens the pop-up (the "Explore concept" button remains the keyboard-friendly way in).

---

## 4. Logo

**Default:** the typographic "US" monogram — nothing to do.

**To use your own logo image:**

1. Export your logo as PNG (transparent background), SVG or WebP. About 92–140 px tall; it is shown at 46 px.
2. Put it in an `assets` folder next to the HTML file (e.g. `assets/logo.png`).
3. In `SITE_CONFIG` (end of the HTML file) set:

```js
logoImage: 'assets/logo.png',
logoImageAlt: 'Ummay Salma logo',
hideNameWithLogo: false,   // true = show only the image, hide the "ummaysalma." text
```

If the path is wrong, the "US" monogram is shown automatically. To go back, set `logoImage: ''`.

---

## 5. Replacing the placeholders with your own images

Hero, About and the four project covers show drawn placeholders (shapes in the palette colours) until you add pictures. Fill the `images` block in `SITE_CONFIG`:

```js
images: {
  hero:  { src: 'assets/hero.jpg',  alt: 'Ummay Salma — portfolio hero image' },
  about: { src: 'assets/about.jpg', alt: 'Portrait of Ummay Salma' },
  projects: {
    bookloop:  { src: 'assets/bookloop.jpg',  alt: 'BookLoop app screens' },
    delivera:  { src: 'assets/delivera.jpg',  alt: 'Delivera app screens' },
    nestora:   { src: 'assets/nestora.jpg',   alt: 'Nestora website screens' },
    stockflow: { src: 'assets/stockflow.jpg', alt: 'StockFlow dashboard screens' }
  }
}
```

### Steps
1. Create a folder named `assets` next to the HTML file.
2. Export the images at the sizes below and put them in it.
3. Write each path in `src`. Leave `src: ''` to keep that placeholder.
4. Hard refresh the page (Ctrl/Cmd + Shift + R).
5. When you publish, upload the `assets` folder too.

### Sizes (export at 2× so they stay sharp on retina screens)

| Slot | Shape | Export size | What happens |
|---|---|---|---|
| Hero | Portrait 4:5 | **1000 × 1250 px** | Fills the rounded container. The two floating labels ("Human-centered", "Product thinking") stay on top. |
| About | Square 1:1 | **1000 × 1000 px** | Fills the frame. A soft dark shade is added at the bottom so the caption stays readable; the "Curiosity → Clarity → Craft" sticker stays. |
| Each project | Landscape 4:3 | **1600 × 1200 px** | Fills the big thumbnail; slight zoom on hover. The "In progress" badge on StockFlow stays. |

### Good to know
- **Cropping:** images fill their frame and are cropped from the centre, so keep important content in the middle. All four project covers have the same 4:3 shape, so one export size works for all.
- **Show the whole image instead of cropping:** change `object-fit: cover` to `object-fit: contain` in `.hero-image`, `.project-img` or `.about-img`.
- **Weight:** JPG/WebP for photos and screens, PNG/SVG for transparency. Aim for under 300 KB each (squoosh.app can compress).
- **File names:** lowercase, numbers and hyphens, no spaces.
- **Do not link to Behance/Instagram image addresses directly** — they can block or change. Download the image and keep it in `assets`.
- **Wrong path?** The placeholder stays and nothing breaks. Chrome → DevTools → Console shows which file was not found.
- **Alt text:** write a short description of the image (screen readers, SEO).

---

## 6. Everyday edits

| What | Where |
|---|---|
| Designation | Search for `Product Designer ·` (hero `<p class="eyebrow">`). |
| Areas I love working on | `<div class="focus-items">` — one `<span><i></i> Name</span>` per item. |
| Project text / tags | The matching `<article class="project-card">`; its pop-up text is in `projectInfo` (script). |
| Behance link and button text of a project | `projectInfo` → the project → `link`, `linkKicker`, `linkLabel`. Remove `link` to hide the button. |
| Remove "In progress" from StockFlow | Delete the `<span class="status-badge art-status">` line in its card and the `status:` line in `projectInfo.stockflow`. |
| Email address | `SITE_CONFIG.email` (all email links update). Also change it inside `formEmailEndpoint` and in `google-apps-script.gs` if you use them. |
| Behance profile link | Search for `ummaysalma82` (3 places). |
| Colours / fonts | `:root` at the top of the `<style>` block. |
| Spacing of the staggered grid | `.project-card:nth-child(2)` and `(4)` → `margin-top: 110px` (set to `0` for a flat grid). |

---

## 7. Back to top

Fixed in the earlier version and kept here. The links point to `#top`, which is an invisible anchor at the very start of the page (the header itself is fixed to the screen, and a browser cannot scroll to a fixed element). A small script adds a smooth scroll and respects "reduce motion".

---

## 8. Project pop-up links

| Project | Button text | Opens |
|---|---|---|
| BookLoop | View BookLoop on Behance | Bookloop case study |
| Delivera | View Delivera on Behance | Delivera case study |
| Nestora | View Nestora on Behance | Nestora (spelled "Nastora" in its Behance address) case study |
| StockFlow | **Check out my other projects** | "Styled Comfort" clothing brand landing page on Behance |

All open in a new tab.

---

## 9. Question form — how messages reach you

The website is plain HTML, so it cannot send email by itself. The form posts to a free service. Use Option A, B or both.

### Option A — send each question to your email (already switched on)

Uses **FormSubmit** (formsubmit.co), free, no account.

1. Upload / host the website (§11). *(Opening the file straight from your computer may be blocked by the browser; test on the hosted link.)*
2. Send **one test question** from the live site.
3. FormSubmit emails `salmamonowara@gmail.com` an **activation link**. Click it once (check Spam/Promotions).
4. Done. New questions arrive as a table (name, email, message, page). Use *Reply* to answer the visitor.

Until step 3 is done, questions are **not** delivered. Your email address is already public on the page, so putting it in the form address exposes nothing new. A hidden "honeypot" field catches most spam bots.

### Option B — also save each question to Google Sheets / Google Docs

Uses **Google Apps Script** (free, inside your Google account). Each question becomes a row in a Google Sheet; optionally also an entry in a Google Doc and an email copy.

1. Go to **sheets.google.com**, create a blank spreadsheet (e.g. *Portfolio questions*).
2. **Extensions → Apps Script**.
3. Delete the sample code, paste everything from `google-apps-script.gs`, click **Save**.
4. *(Optional)* For a Google Doc too: create a Doc, copy the long ID from its address (`docs.google.com/document/d/`**`THIS-PART`**`/edit`) into `DOC_ID`.
5. **Deploy → New deployment → ⚙ Select type → Web app** → *Execute as:* **Me**, *Who has access:* **Anyone** → **Deploy**. Approve the permission screen (Google shows "unverified app" for your own script: *Advanced → Go to project*).
6. Copy the **Web app URL** (ends with `/exec`).
7. Paste it in `SITE_CONFIG`:

```js
googleScriptUrl: 'https://script.google.com/macros/s/XXXXXXXX/exec'
```

8. Send a test question; a row should appear in the **Questions** tab.

After changing the Apps Script code later: **Deploy → Manage deployments → ✏ → New version** (the URL stays the same).

A Sheet keeps Name / Email / Message in separate columns (easy to sort and search); the Doc option is there because you asked for it.

### What the visitor sees
Empty or invalid fields → red outline and a short message. While sending → button disabled. Success → "Thank you!…" and the form clears. Failure → a message with your email as a clickable fallback.

---

## 10. Accessibility notes

- Body text `#66615B` on `#F7F3ED` ≈ 5.6:1; headings `#292824` ≈ 14:1; small accent text uses `#9A5439` ≈ 5:1 (all pass WCAG AA).
- The bright accent `#B96E50` is used only for large italic headlines, shapes and dots, never for small text.
- Visible keyboard focus ring, labelled form fields, `aria-live` form messages, motion turned off for visitors who prefer reduced motion.

---

## 11. Publishing

Any static host works (Netlify Drop, GitHub Pages, Cloudflare Pages, Vercel). Upload the HTML file (rename it to `index.html` so the plain address opens it) plus the `assets` folder if you use images or a logo.

### Checklist before you publish
- [ ] Option A activated (§9) and a test question received.
- [ ] If using Option B: a test row appears in the Sheet.
- [ ] Click *Explore concept* (and each thumbnail) on all four projects; each Behance button opens the right page. When StockFlow's case study is published, update its `link` / `linkLabel` and remove the "In progress" badge.
- [ ] Add your own images (§5) — the placeholders are decorative, but real work thumbnails sell the portfolio.
- [ ] Check on a phone: menu, form, Back to top.
- [ ] The `assets` folder is uploaded (images / logo).
- [ ] Fonts load (open the live site while online).

---

## 12. What was tested (1 Nov 2026, Chrome; desktop 1366 px, tablet 820 px, phone 390 px)

34 automated checks passed: theme colours and fonts applied; designation; areas; US logo; StockFlow badge; email link; form title and labels; empty-form and bad-email blocking; valid submission (request contained name, email, message); success and failure messages; Back to top from footer, Contact and logo; all four pop-up links (correct address, new tab, status only on StockFlow); thumbnail click opens the pop-up; no JavaScript errors; no sideways scrolling on tablet and phone.
Image slots were tested separately with sample pictures (hero, About, three project covers) and with a deliberately wrong path (placeholder stayed, nothing broke), also for the logo.

**Not tested here:** real delivery to your inbox / Google Sheet (needs your activation and Google account — §9) and the live Google Fonts download (the preview used local copies of the same two fonts).

---

## 13. Troubleshooting

| Problem | Likely reason | Fix |
|---|---|---|
| Headlines look like Times/Georgia | Fonts did not download (offline / blocked) | Check the internet connection; the layout still works. |
| Form says "Sorry, something went wrong" | File opened directly from the computer, or no internet | Test on the hosted link. |
| Form says success but no email arrives | Activation link not clicked | Click the FormSubmit activation email (check Spam). |
| Nothing in the Google Sheet | Web app access not "Anyone", or old deployment | Redeploy (§9 B step 5) and re-paste the `/exec` URL. |
| An image does not appear | Wrong path or file name (capitals matter on most hosts), or `assets` not uploaded | Fix `src`; the placeholder stays meanwhile. |
| Changes not visible | Browser cache | Hard refresh (Ctrl/Cmd + Shift + R). |
