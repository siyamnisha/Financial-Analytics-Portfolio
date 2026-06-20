# Md. Siyam Hossain Nisha — Financial Analytics Portfolio

A single-file, responsive portfolio site built to showcase Financial Analytics coursework and quantitative research projects — analytics-ready data pipelines, ARIMA/GARCH/LSTM forecasting, and responsible AI use in academic work.

**Live structure:** everything lives in one file, `index.html` — no build step, no dependencies, ready for GitHub Pages.

---

## 🚀 Deploy to GitHub Pages

1. Create a new repository (e.g. `username.github.io` for a root-domain site, or any name for a project site).
2. Add `index.html` to the repository root.
3. Push to GitHub:
   ```bash
   git init
   git add index.html
   git commit -m "Add portfolio site"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<repo-name>.git
   git push -u origin main
   ```
4. In the repo, go to **Settings → Pages**.
5. Under **Build and deployment**, set **Source** to `Deploy from a branch`, branch `main`, folder `/ (root)`.
6. Save. Your site will be live at:
   - `https://<your-username>.github.io/` (if the repo is named `<your-username>.github.io`), or
   - `https://<your-username>.github.io/<repo-name>/` (for any other repo name).

GitHub Pages can take a minute or two to publish after the first push.

---

## 📁 Project Structure

```
.
├── index.html      # the entire site — HTML, CSS, and JS in one file
└── README.md       # this file
```

No `node_modules`, no build pipeline, no package manager — just open `index.html` in a browser to preview locally, or use a simple local server:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

---

## 🛠️ Tech Stack

- **HTML5 / CSS3 / Vanilla JavaScript** — no frameworks, no external CSS libraries
- **Google Fonts** — Poppins (display), Inter (body), JetBrains Mono (data/labels)
- **Inline SVG + Canvas** — all charts (price trend, volatility forecast, return forecast) are hand-drawn with the Canvas API, no charting library
- **CSS custom properties** — power the light/dark theme toggle

---

## ✏️ Customizing

All editable content lives directly in `index.html`. Useful anchors to search for:

| What to change | Where to look |
|---|---|
| Name, role text, hero stats | `<section class="hero" id="home">` |
| Bio & timeline | `<section ... id="about">` |
| Skill bars & percentages | `<section ... id="skills">`, edit `data-pct` values |
| Project content & real metrics | `<section ... id="projects">` |
| Chart data | `<script>` block at the bottom, look for `drawLineChart` / `drawBarChart` calls |
| Resume / GitHub / Drive links | search for `href="#"` and `showToast(...)` — replace with real URLs once available |
| Colors | `:root { --primary; --secondary; --accent; --bg; }` near the top of the `<style>` block |
| Profile photo | the `<img src="data:image/jpeg;base64,...">` in the hero section — it's embedded directly so the file stays single-file and portable |

---

## 🤖 Responsible AI Disclosure

This site documents an explicit AI-use practice: AI tools were used for code generation, debugging, and content drafting throughout these projects, with every output independently reviewed and validated against the underlying notebooks, data-quality logs, and project memos before being presented. See the **AI Practice** and **Prompt Log** sections on the site itself for the full disclosure and a step-by-step audit trail.

---

## 📬 Contact

- **Email:** [siyamzahlen@gmail.com](mailto:siyamzahlen@gmail.com)
- **LinkedIn:** [linkedin.com/in/md-siyam-hossain-nisha-26b913363](http://www.linkedin.com/in/md-siyam-hossain-nisha-26b913363)

---

© 2026 Md. Siyam Hossain Nisha. Built with HTML, CSS, JavaScript, Python, and Responsible AI.
