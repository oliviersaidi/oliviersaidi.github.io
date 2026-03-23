# oliviersaidi.github.io — Maintenance Guide

## Repo & Local Setup

- **Live site:** https://oliviersaidi.github.io
- **GitHub repo:** https://github.com/oliviersaidi/oliviersaidi.github.io
- **Local clone (iCloud):** `~/Library/Mobile Documents/com~apple~CloudDocs/Github_webpage/`
- **Single file:** all content is in `index.html` — no build step, no dependencies

---

## Workflow: Edit Locally and Push

```bash
# 1. Navigate to local repo
cd ~/Library/Mobile\ Documents/com~apple~CloudDocs/Github_webpage

# 2. Pull latest before editing (always do this first)
git pull

# 3. Edit index.html with any text editor or VS Code
open -a "Visual Studio Code" index.html

# 4. Stage, commit, and push
git add index.html
git commit -m "describe what you changed"
git push origin main
```

GitHub Pages redeploys automatically within ~1 minute of push.

---

## Key Sections in index.html

| Section | What it contains |
|---|---|
| CSS variables (`:root`) | Colors, fonts — edit theme here |
| `.header-links` | Top-right nav links (ORCID, GitHub, arXiv, Cambridge, Zenodo, Contact) |
| `.metrics` | Impact stats — views/downloads are dynamic via Zenodo API |
| `.paper` blocks | One block per paper — title, meta, abstract, badges |
| `.repos` | Open source repo cards |
| `footer` | Bottom nav links — mirrors header links |
| `<script>` (end of body) | Zenodo API fetch for dynamic stats |

---

## Adding a New Paper Badge

Find the correct `.paper` block and add a badge inside `.paper-badges`:

```html
<a class="badge" href="URL" target="_blank">Label</a>
<a class="badge primary" href="URL" target="_blank">Label</a>  <!-- primary = gold color -->
```

**Badge order convention:** DOI (primary) → Cambridge Open Engage → SSRN → Code

---

## Adding a New Paper Section

Copy an existing `.paper` block and update:
- `paper-title` — title + link to primary source
- `paper-meta` — author · year · venue(s) · stats
- `paper-abstract` — 2–3 sentence summary
- `paper-badges` — DOI, Cambridge, SSRN, Code buttons

---

## Dynamic Impact Stats (Zenodo API)

The script at the bottom of `index.html` fetches stats from 3 Zenodo records at page load:

| Record ID | Paper |
|---|---|
| 15006676 | PACF: Pattern-Aware Complexity Framework (NP-hard) |
| 15873947 | PACF: LLM Inference Efficiency |
| 18894726 | PACF_F: Volatility Model Selection |

To add a new Zenodo record, add its ID to the `records` array in the script:

```javascript
const records = [15006676, 15873947, 18894726, NEW_ID];
```

---

## Pending Items

- [x] SSRN badge added to PACF_F (Abstract ID 6366718)
- [x] Cambridge Open Engage badge added to PACF_LLM
  - URL: `https://www.cambridge.org/engage/coe/article-details/69afcaead1922e37d565fe6d`

---

## Instructions for Claude (AI Assistant)

When asking Claude to update the site:

1. **Always specify the local path:**
   `"/Users/olivier/Library/Mobile Documents/com~apple~CloudDocs/Github_webpage/index.html"`

2. **Workflow Claude should follow:**
   - Read the current file first before editing
   - Make targeted edits (never rewrite the whole file)
   - Commit and push via Desktop Commander
   - Confirm the push was successful with `git log --oneline -3`

3. **Never delete or rewrite** the Zenodo API script block at the bottom of the file

4. **Commit message conventions:**
   - `feat:` — new content or link added
   - `fix:` — broken link, typo, layout issue
   - `update:` — refreshing existing content

5. **Key URLs to know:**
   - Cambridge author search: `https://www.cambridge.org/engage/coe/search-dashboard?text=olivier+saidi`
   - Zenodo author search: `https://zenodo.org/search?q=Olivier+Saidi&f=resource_type%3Apublication`
   - arXiv paper: `https://arxiv.org/abs/2506.13810`
   - ORCID: `https://orcid.org/0009-0004-3221-6911`
