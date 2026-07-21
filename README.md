# Excel Staffing Gantt

A single-page web app that turns an Excel workbook of shift data into a **15-minute increment gantt chart** with lunch and break overlays, employee filtering, hourly staffing totals, and PNG/PDF export.

Everything runs in the browser — there is **no backend, no build step, and no install**.

## Live demo (GitHub Pages)

Once you push this repo to GitHub and enable Pages, the app will be live at:

```
https://<your-username>.github.io/<your-repo-name>/
```

## Features

- `.xlsx` / `.xls` upload with drag-and-drop
- worksheet selector for multi-tab workbooks
- password-locked collapsible column mapping (default password: `opslock`)
- validation rules
  - **Error:** no scheduled agents during operating hours
  - **Warning:** fewer than 2 scheduled agents during operating hours
- downloadable warnings + errors (CSV or Excel)
- 15-minute grid snapping
- business hours logic
  - Mon–Fri: 6:00 AM – 8:00 PM
  - Sat–Sun: 8:00 AM – 4:00 PM
- gantt layout: **Agent Name → Shift → Bar Chart**
- lunch and break block overlays
- **Sum of employees by hour** row above each day
- day view and week view
- sticky headers (top and left) while scrolling
- resizable gantt container
- employee filter
- exports
  - Day PNG / Day PDF
  - Week PNG / Week PDF
- darkened headers for exports so nothing renders as white-on-white

## Repository structure

```
.
├── index.html   # the entire app
├── README.md    # this file
└── LICENSE      # MIT license
```

## How to host it live on GitHub Pages

1. Create a new GitHub repository (public).
2. Upload `index.html`, `README.md`, and `LICENSE` to the root.
3. Commit and push.
4. In the repository, go to **Settings → Pages**.
5. Under **Build and deployment**, set:
   - **Source:** Deploy from a branch
   - **Branch:** `main` (or whichever branch you pushed to)
   - **Folder:** `/ (root)`
6. Save. GitHub will publish the site in about a minute.
7. Your live URL will be:
   `https://<your-username>.github.io/<your-repo-name>/`

## How to change the mapping password

Open `index.html` and search for:

```js
const CONFIG = { mappingPassword: 'opslock', ... }
```

Change `'opslock'` to whatever you want.

This password is intended to prevent **accidental** changes to the column mapping. Because the app is fully client-side, this is not a strong security control — treat it as a soft lock, not a firewall.

## Expected Excel structure

One row per agent per day.

| Agent Name | Day     | Shift Start | Shift End | Lunch Start | Lunch End | Break 1 Start | Break 1 End | Break 2 Start | Break 2 End |
|------------|---------|-------------|-----------|-------------|-----------|---------------|-------------|---------------|-------------|
| Ava        | Monday  | 6:00 AM     | 2:30 PM   | 10:00 AM    | 10:30 AM  | 8:15 AM       | 8:30 AM     | 12:15 PM      | 12:30 PM    |
| Ben        | Monday  | 9:00 AM     | 5:00 PM   | 12:30 PM    | 1:00 PM   | 10:45 AM      | 11:00 AM    | 3:00 PM       | 3:15 PM     |

You can download an editable template directly from the app’s **Download template** button.

If your export uses different headers (e.g. `Employee` instead of `Agent Name`), unlock the mapping section and adjust the column mapping.

## Libraries used

Loaded from CDN — no install needed:

- [SheetJS (`xlsx`)](https://sheetjs.com) — reads and writes Excel files
- [html2canvas](https://html2canvas.hertzen.com) — captures the gantt view for export
- [jsPDF](https://github.com/parallax/jsPDF) — generates the PDF file

## License

MIT — see `LICENSE`.
