# SDG 5 — Visualizing the Global Reality of Gender Equality

**CDS6324 Data Visualization Project · Group TT4L_G11**

An interactive, single-page data visualization dashboard that explores how sex shapes survival, education, work, and power across 193 countries from 1990 to 2023. Built on composite indices from the [UNDP Human Development Report](https://hdr.undp.org/).

---

## Live Demo

Deployed on Netlify → **[your-site-name.netlify.app](https://your-site-name.netlify.app)**  
*(update this link after deploying)*

---

## Features

The dashboard contains six linked chart panels, all controlled by a shared region/country/year filter bar:

| # | Theme | Chart type |
|---|-------|-----------|
| 1 | Health & Survival Gap | Line chart + ranked bar |
| 2 | Maternal Health Risk Landscape | Choropleth map |
| 3 | Education Parity | Diverging bar / small multiples |
| 4 | Labour Force Participation Gap | Area chart |
| 5 | Political Empowerment | Dot / lollipop chart |
| 6 | Gender Inequality Index (GII) | Choropleth map + trend |

**Key interactions**
- Click any country on a map or ranking bar to highlight it across every panel
- Drag the year slider (or press **Play**) to animate 1990–2023
- Filter by world region to narrow comparisons

---

## Project Structure

```
.
├── index.html      # Self-contained dashboard (HTML + embedded CSS + JS + D3)
├── netlify.toml    # Netlify deployment configuration
└── README.md
```

All data, styles, and JavaScript (including D3 v7) are bundled inline inside `index.html` — no build step or server required.

---

## Deploying to Netlify

### Option A — Netlify Drop (fastest)
1. Go to [app.netlify.com/drop](https://app.netlify.com/drop)
2. Drag the project folder onto the page
3. Your site is live instantly

### Option B — Connect GitHub repo
1. Push this repo to GitHub
2. Log in to [netlify.com](https://netlify.com) → **Add new site → Import from Git**
3. Select the repo; Netlify auto-detects `netlify.toml`
4. Click **Deploy** — done

No build command or environment variables are needed.

---

## Team

| Name | Contribution |
|------|-------------|
| Abdullah Nasih Ulwan | Health & Survival (Panel 1 & 2) |
| Imran Syahmi | Education Parity (Panel 3) |
| Danish Adam | Labour, Politics & GII (Panel 4–6) |

Submitted to **Dr. Aziah Binti Ali**

---

## Data Sources

- UNDP Human Development Reports — Gender Inequality Index (GII)
- UNDP — Gender Development Index (GDI)
- World Bank — Labour force participation, maternal mortality
- UN Women — Parliamentary representation

---

## License

This project was created for academic purposes. Data belongs to respective source organisations.
