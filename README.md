# Household Poverty Prediction – Project Website

Single-page website for the CSE 276 capstone **Household Poverty Prediction for Programme Targeting** (Lovely Professional University). It presents the problem, method, results for countries A, B and C, the BFS route-planning part, and a **Try it** section where visitors upload their own data and get predictions.

Live: https://sphinx-light.github.io/poverty_prediction_site/

## Contents

| File | Purpose |
|---|---|
| `index.html` | The whole site (HTML, CSS and JavaScript in one file, no build step) |

## Try it section

The upload form sends two CSV files (household and individual) to a separate model API and shows the scores, metrics (if a `poor` column is included) and a downloadable results file.

The API lives in the `Poverty-prediction-CSE-276-Project` repository and is hosted on Render. Nothing is stored by the website.

### Setting the API address

Either type the address into the "Model API address" box on the page, or set the default near the top of the Try it script in `index.html`:

```js
const DEFAULT_API_URL = window.POVERTY_API_URL || 'https://poverty-prediction-cse-276-project.onrender.com';
```

Use the base address only: https, no `/health` or other path.

### Requirements for it to work

- The API must allow this site: on Render, set `ALLOWED_ORIGINS` to `https://sphinx-light.github.io` (no path, no trailing slash).
- Both must use https. A https page cannot call an http API.
- The free Render server sleeps when idle. The first "Check connection" can take up to a minute.

If the status says "not reachable", press F12, open the Console, and look for a CORS message. It means `ALLOWED_ORIGINS` does not match the site's address.

## Run locally

Open `index.html` in a browser. To test Try it against a local API, run the API (`uvicorn app:app --port 8000`), keep the address `http://localhost:8000`, and set `ALLOWED_ORIGINS=*` on the API (a local file has the origin `null`).

## Deploy on GitHub Pages

1. Put `index.html` at the root of this repository.
2. Go to Settings > Pages, choose the `main` branch and the `/ (root)` folder, then save.
3. The site appears at `https://<username>.github.io/<repository-name>/` after a minute or two.

## Notes

- Fonts and any external assets load from public CDNs, so the page needs internet access to look right.
- Results on the site come from the DrivenData Pover-T data. Check the competition terms before reusing it.
