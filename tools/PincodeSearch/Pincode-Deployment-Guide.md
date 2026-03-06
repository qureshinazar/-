# India Pincode Search — Deployment Guide

## ✅ What Was Generated

| Output | Location | Details |
|---|---|---|
| **index.json** | `pincode-data/index.json` (10 KB) | State → district mapping for fast dropdowns |
| **37 state files** | `pincode-data/states/*.json` (29.3 MB) | Per-state pincode data loaded dynamically |
| **4 sitemap files** | `pincode-data/sitemaps/` | 165,635 URLs across 4 XML files + index |
| **Blogger HTML** | `pincode-search.html` | High-performance dynamic SEO page |

## 🚀 Step-by-Step Deployment

### Step 1: Push latest changes to GitHub
The files are already pushed to your repository `qureshinazar/-` on the `main` branch.

### Step 2: Verify jsDelivr CDN access

Verify that jsDelivr is correctly serving your JSON files by opening:
- `https://cdn.jsdelivr.net/gh/qureshinazar/-/pincode-data/index.json`
- `https://cdn.jsdelivr.net/gh/qureshinazar/-/pincode-data/states/delhi.json`

### Step 3: Add Blogger page

1. Log into your **Blogger Dashboard**.
2. Go to **Pages** → click **New Page**.
3. In the editor toolbar, switch from "Compose View" to **"HTML View"**.
4. Paste the entire code from `pincode-search.html`.
5. Name the page title **"India Pincode Search"**.
6. Set the Custom Permalink to exactly `india-pincode-search` (so the URL becomes `/p/india-pincode-search.html`).
7. Click **Publish**.

### Step 4: Submit Sitemaps to Google Search Console

1. Go to [Google Search Console](https://search.google.com/search-console).
2. Open your property (`aiocrafters.com`).
3. Click on **Sitemaps** in the left sidebar.
4. Under "Add a new sitemap", paste exactly this URL:
   `https://cdn.jsdelivr.net/gh/qureshinazar/-/pincode-data/sitemaps/sitemap-index.xml`
5. Click **Submit**.

---

## 📐 How It Works

### Architecture
```text
User visits: /p/india-pincode-search.html?chhattisgarh/balod/arkar-bo/491222
                                          ↓
                          JS parses URL → loads chhattisgarh.json from jsDelivr
                                          ↓
                          Populates dropdowns → shows Arkar BO results
                                          ↓
                          Updates: <title>, meta description, JSON-LD, canonical URL
```

### Two Search Modes
1. **Search Pincode Tab** — Uses `api.postalpincode.in` to fetch instant results. Clicking a result auto-routes the user to the detailed rich-results view.
2. **Browse by Location Tab** — Uses the JS-based dropdowns powered by the `pincode-data` hosted on GitHub/jsDelivr.

### Dynamic SEO for each pincode
When a pincode is selected (e.g., 491222), JavaScript automatically injects:
- **Title tag:** "Pincode 491222 - Arkar BO | BALOD, CHHATTISGARH"
- **Meta description:** Unique per pincode
- **Canonical URL:** Cleans up the URL to prevent duplicate content issues
- **JSON-LD Schema:** PostalAddress schema for Google rich snippets
- **Internal Crosslinks:** The "Nearby Post Offices" table generates SEO-friendly anchor links

## ⚠️ Important Notes

> **jsDelivr Caching:** jsDelivr caches files aggressively. If you ever update the JSON data in the future, you may need to purge the cache or use versioned URLs (like `qureshinazar/-@v1.0`).

> **Google Indexing Time:** Google will gradually discover and index the 165K URLs via the sitemaps. Because this is relying on JavaScript rendering (Dynamic URL routing on a single HTML file), Googlebot will render the queries, but indexing all 165K paths will take time.
