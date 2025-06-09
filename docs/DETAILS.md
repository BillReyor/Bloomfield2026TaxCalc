# Calculation Details

This calculator models Bloomfield's four-year phase-in of the 2024 property revaluation.
Equalized mill rates show the revenue-neutral baseline for each phase-in level.
The council's adopted mill rates already include any budget changes and are the
figures actually used to compute taxes.

```javascript
const defaultRates = {
  councilY0: 37.49, // FY 2025
  councilY1: 35.64, // FY 2026
  councilY2: 34.15, // FY 2027
  councilY3: 32.88, // FY 2028
  councilY4: 31.79, // FY 2029
  equalizedY1: 34.27, // informational
  equalizedY2: 31.88, // informational
  equalizedY3: 29.80, // informational
  equalizedY4: 27.97  // informational
};
```

These defaults are defined in the embedded script near the bottom of `index.html`.

## Inputs

- **Current Assessed Value** – post-revaluation assessment.
- **Old Assessed Value** – previous assessment before October 2024 (optional).
- **Revaluation Increase (%)** – percent increase used to infer your old value (optional).
- **Council Mill Rates** – FY 2025–2029 rates; overridable in Advanced Configuration.
- **Equalized Rates** – revenue-neutral rates for FY 2026–2029 (four phases of the revaluation).

## Calculation Steps

1. **Read Inputs** – start with `defaultRates` and override any values entered in the Advanced Configuration panel.
2. **Compute Phase-In Assessments** – if an old value or percentage is provided, the difference between new and old is applied over four years:

```javascript
const diff     = postVal - oldVal;
const assessY1 = oldVal + 0.25 * diff;
const assessY2 = oldVal + 0.50 * diff;
const assessY3 = oldVal + 0.75 * diff;
const assessY4 = postVal;
```

3. **Determine Mill Rates** – the equalized rates show what the mill rate would be if revenue stayed flat at each phase-in level. The calculator uses the council's adopted rates to compute your taxes.
4. **Compute Annual Taxes** – each phased assessment is divided by 1000 and multiplied by the appropriate mill rate.
5. **Render Output** – the page displays estimated taxes for GL 2023–GL 2027 along with year-over-year changes.

These calculations provide estimates only and may not match your exact bill.

## Helper Functions

Several small helper functions keep the user interface responsive. They are defined in the script portion of `index.html`:

- `validateInput()` – enables or disables the **Calculate** button when the post‑revaluation value is invalid.
- `formatCurrency(num)` – formats numbers as US dollars with comma separators and two decimal places.
- `renderWarning()` – displays a warning if neither an old value nor a revaluation percentage is provided.
- `renderWithDiff(taxY0, taxY1, taxY2, taxY3, taxY4)` – renders the results table and calculates year‑over‑year changes.

## Event Handlers

- **Advanced Configuration Toggle** – clicking the element with ID `toggleAdvanced` shows or hides the advanced section and updates ARIA attributes.
- **Calculate Button** – the main calculation logic runs when `calculateBtn` is clicked, reading inputs, computing taxes and rendering results.
