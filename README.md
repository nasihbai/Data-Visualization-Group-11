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

## Challenges & Solutions

### Technical Hurdles

#### 1. TopoJSON reference error in Opera GX (and Chromium-based browsers)

The original `index.html` loaded TopoJSON from cdnjs:

```
https://cdnjs.cloudflare.com/ajax/libs/topojson/3.0.2/topojson-client.min.js
```

On Opera GX (and some Chromium builds with strict CSP or content-blocking), the `topojson` global was not exposed correctly, causing the choropleth map to throw:

```
ReferenceError: topojson is not defined
```

The map panel rendered blank and the country-click interaction was broken across the whole dashboard because `byIso` lookups depended on features resolved through TopoJSON.

#### 2. D3 double-click conflict with brush zoom

D3's built-in zoom handler registers its own `dblclick.zoom` listener. When the brushable line chart (Chart 1) and the choropleth map both had zoom + custom double-click reset, the native zoom handler fired first and prevented the custom reset from running, leaving the view stuck after a zoom.

#### 3. Data cleaning — missing ISO-3 codes

Several countries in the UNDP dataset used non-standard ISO-3 codes (e.g. Kosovo `XKX`, Channel Islands) that had no matching feature in the world TopoJSON. These rows still appeared in dropdowns and rankings but produced silent no-ops on the map, with no visual indication to the user.

---

### Solutions

#### Fix 1 — Switch CDN to jsDelivr

Replaced the cdnjs URL with the jsDelivr package URL, which correctly sets `window.topojson` as a UMD global across all Chromium-based browsers:

```js
// Before (broken in Opera GX)
<script src="https://cdnjs.cloudflare.com/ajax/libs/topojson/3.0.2/topojson-client.min.js"></script>

// After (works everywhere)
<script src="https://cdn.jsdelivr.net/npm/topojson-client@3.1.0/dist/topojson-client.min.js"></script>
```

Also bumped the patch version from `3.0.2` → `3.1.0` which includes a fix for feature-collection edge cases.

#### Fix 2 — Suppress native zoom dblclick, wire custom reset

D3's zoom attaches as `dblclick.zoom`. Calling `.on("dblclick.zoom", null)` on the SVG removes it, then a separate listener on the outer `div` triggers `zoom.transform` back to `d3.zoomIdentity`:

```js
// Disable D3's built-in double-click zoom handler
svg.on("dblclick.zoom", null);

// Wire a clean reset on the container div instead
d3.select("#chartMap").on("dblclick", () => {
  svg.transition()
     .duration(400)
     .call(zoom.transform, d3.zoomIdentity);
});
```

The same pattern is applied to the bubble scatter chart (`#chartBubble`) so both zoomable panels reset consistently.

#### Fix 3 — Graceful null handling for unmatched ISO-3 codes

The `valueFor()` helper already returns `null` for missing records. The map fill logic was extended to fall back to a neutral grey, and the tooltip falls back to `d.properties.name` when `byIso` has no match:

```js
function valueFor(iso3, year) {
  const recs = byIso.get(iso3);
  if (!recs) return null;           // no match → grey on map, skip in rankings
  const rec = recs.find(r => r.year === year);
  return rec ? rec.pr_f : null;
}

// In the mousemove handler — graceful name fallback
const name = (byIso.get(iso3) && byIso.get(iso3)[0].country)
             || d.properties.name;  // TopoJSON built-in name as last resort
```

Data cleaning in Excel/Python removed rows where both `iso3` and `country` were blank, and standardised `XKX` entries so Kosovo appears correctly in charts even when absent from the map.

---

## Data Sources

- UNDP Human Development Reports — Gender Inequality Index (GII)
- UNDP — Gender Development Index (GDI)
- World Bank — Labour force participation, maternal mortality
- UN Women — Parliamentary representation

---

## License

This project was created for academic purposes. Data belongs to respective source organisations.
