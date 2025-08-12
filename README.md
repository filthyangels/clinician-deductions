# Clinician Deductions — Single-file HTML App

A lightweight, single-page tool for Australian **junior doctors and nurses** to estimate **work-related deductions** (PAYG, resident taxpayers). Built to be **fast**, **offline-friendly**, and **ATO-aware**. No build step, no dependencies.

> **Important disclaimer:** This is a personal side project/hobby tool. It is **not affiliated with or endorsed by the Australian Taxation Office (ATO)**, does **not** constitute financial, tax, or legal advice, and may be incomplete or out of date. **Use at your own risk.** Always refer to the **official ATO documentation** and consider seeking advice from a qualified professional. The author(s) **accept no liability** for any loss or consequences arising from use of this tool.

---

## Features

* **Single HTML file** (`index.html`), no external libraries
* **Live calculations** (no “Calculate” button)
* **Left sidebar**: section status (green = included, orange = pending), live **Summary** + **Total**
* **Evidence checklist** auto-builds as you go
* **Collapse/expand** per category (ticked = expanded)
* **Reset** restores defaults and reseeds starter rows where applicable
* **Self-tests** to verify logic (see below)
* Number input **spinners removed** so they don’t cover values on macOS/iOS

---

## Quick start (GitHub Pages)

1. Rename your file to **`index.html`**.
2. In your GitHub repo: **Add file → Upload files** → drop `index.html` → **Commit**.
3. **Settings → Pages** → **Source: *Deploy from a branch*** → **Branch: `main` / (root)** → **Save**.
4. Wait \~30–60s; your site appears at:
   `https://<your-username>.github.io/<repo-name>/`

> If you see 404/old content, refresh after a minute or do a hard reload (Shift+Reload).

---

## What’s included (categories)

* **Registration (AHPRA/NMBA)** — `card-ahpra`
* **Professional indemnity (MDO)** — `card-mdo`
* **Union / Association fees** — `card-union`
* **Phone & Internet** (combined) — `card-pi`
* **Work from home (Home office)** — `card-home`

  * **Fixed-rate 70c/hr** (`home-choice-fixed`)
  * **Actual costs** (`home-choice-actuals`) incl. power and (optionally) phone/internet
* **Textbooks / Journals / Subscriptions** — `card-books`
* **CPD / Conferences / Exams** — `card-cpd`
* **Uniform / Laundry / PPE** — `card-laundry`
* **Tools & Equipment** (incl. laptop, stethoscope) — `card-assets`
* **Parking / Tolls** — `card-parking`
* **Travel — Car** (CPK + Logbook) — `card-car`
* **Travel — Transport (non-car)** — `card-travel-noncar`
* **Travel — Overnight** — `card-travel-overnight`
* **Overtime meal (allowance received)** — `card-overtime`
* **Vaccinations / Medical checks** — `card-vax`
* **Licences / Certifications** — `card-licence`
* **Software / Apps** — `card-software`
* **Stationery** — `card-stationery`
* **Self-tests** — `card-tests`

> **Green/orange sidebar logic:** a section’s bubble is **green** only if the section’s **included amount > 0**. **Orange** means the section is ticked but has **no includable amount** yet. Off when unticked or excluded by rules.

---

## Key rules & interactions (ATO-aware)

* **Work from home (WFH) — Fixed rate 70c/hr**

  * Excludes **Phone & Internet** entirely; the PI card is **greyed/disabled** and **not** added separately.

* **WFH — Actual costs**

  * If **Phone & Internet is ticked**, its total is **included inside Actuals** and **not added separately**; the manual `home-actuals-intph` is disabled.
  * If **Phone & Internet is not ticked**, you can use the manual `home-actuals-intph`.

* **Car — cents per km**: **cap 5,000 km**, default rate **\$0.85** (editable).

* **Laundry**: work-only × **\$1.00** + mixed × **\$0.50**.

* **Overtime meal**: deductible **only** if an **allowance was received and declared**; claim the amount **actually spent** (user-entered).

* **Tools & equipment**:

  * ≤ \$300 → immediate deduction × work%
  * > \$300 → depreciation (prime cost or diminishing), **pro-rated** for days held within the FY (2024-07-01 to 2025-06-30).

---

## Self-tests (what “Run self-tests” checks)

1. **Phone/Internet monthly → annual** math
2. **WFH fixed excludes PI** (and greys the card)
3. **WFH actuals includes PI** correctly (no double count)
4. **Software multi-item** sum
5. **Assets pro-rata depreciation** and row remove → recalculates
6. **Car CPK** (1,000 km @ 0.85 = \$850)
7. **Car logbook** (\$4,000 × 25% = \$1,000)
8. **Transport (non-car)** multi-sum
9. **Overnight travel** multi-sum
10. **Overtime meals**: zero unless allowance declared
11. **Reset** returns total to 0 and re-enables PI

> Tests print to `<pre id="test-output">`. If you change logic, update tests accordingly.

---

## ATO references

Use official ATO pages (not blogs). Helpful starting points:

* Working from home
* Phone & Internet
* Car expenses & Logbook
* Travel & accommodation
* Tools & equipment
* Union fees / Registrations
* Overtime meal allowances
* Self-education expenses

*(Keep links current when updating the app.)*

---

## Accessibility & privacy

* Semantic markup, labelled inputs, keyboard-friendly.
* All logic is client-side; no analytics, no data sent to a server.
* If you add persistence later, prefer **localStorage** and clearly explain what’s stored.

---

## Contributing / Maintenance

* Keep **all existing IDs** (inputs, outputs, tables, buttons) so tests and user muscle memory keep working.
* Preserve function names used by tests (`recalc`, `updateSectionTicks`, `updateEvidence`, `runTests`, etc.).
* After changes, click **Run self-tests** and confirm all pass.

---

## License

Add a license (e.g., MIT) if you intend others to reuse; otherwise, omit.

---

## Legal & Disclaimer (expanded)

* This project is a **personal side project/hobby** and **not an official ATO tool**.
* It provides **general information only** and is **not financial, tax, or legal advice**.
* Information may be **incomplete, incorrect, or out of date**; tax rules change.
* **Always consult the official ATO guidance** and/or a qualified professional for your circumstances.
* The author(s) and contributors **accept no responsibility or liability** for any loss, damage, or consequences arising from use of this software.

---

## Support

Open a GitHub Issue with:

* Steps you took
* What you expected vs what happened
* Screenshots (if helpful)
* Browser + OS

*Built to help clinicians spend more time on patients, not paperwork.*
