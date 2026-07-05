# SDG 5 — Visualizing the Global Reality of Gender Equality

**CDS6324 Data Visualization Project · Group TT4L_G11**

An interactive data visualization site that explores how sex shapes survival, education, work, and power across 193 countries from 1990 to 2023. Built on composite indices from the [UNDP Human Development Report](https://hdr.undp.org/).

The site has two pages — a main six-panel dashboard and a side-by-side country comparison tool.

---

## Live Demo

Deployed on Netlify → **[your-site-name.netlify.app](https://your-site-name.netlify.app)**  
*(update this link after deploying)*

---

## Features

The dashboard contains six linked chart panels, all controlled by a shared region/country/year filter bar:

| # | Theme | Chart type |
|---|-------|-----------|
**Main dashboard (`index.html`) — six linked panels:**

| # | Theme | Chart type |
|---|-------|-----------|
| 1 | Health & Survival Gap | Line chart + ranked bar |
| 2 | Maternal Health Risk Landscape | Bubble scatter (log scale) |
| 3 | Secondary Education Gap | Diverging bar chart |
| 4 | Labour Force Participation Gap | Area chart over time |
| 5 | Female Seats in Parliament | World choropleth map |
| 6 | Gender Inequality Index (GII) | Best/worst ranking bars |

**Comparison page (`comparison.html`):**  
Pick any two countries and a year to see a side-by-side breakdown of all indicators with winner highlighting and a full indicator table.

**Key interactions**
- Click any country on a map or ranking to highlight it across every panel
- Drag the year slider (or press **Play**) to animate 1990–2023
- Filter by world region to narrow comparisons

---

## Project Structure

```
.
├── index.html        # Main dashboard — six linked chart panels
├── comparison.html   # Country comparison page
├── styles.css        # Shared stylesheet
├── data.js           # Shared dataset (UNDP HDR columnar data + world TopoJSON)
├── netlify.toml      # Netlify deployment configuration
└── README.md
```

No build step or server required. D3 v7 and TopoJSON are loaded from jsDelivr CDN.

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
| Abdullah Nasih Ulwan | Health & Survival (Panels 1 & 2) |
| Imran Syahmi | Education & Labour Participation (Panels 3 & 4) |
| Danish Adam | Political Power & GII (Panels 5 & 6) |

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
