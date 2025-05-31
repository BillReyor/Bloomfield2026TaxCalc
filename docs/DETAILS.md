# Calculation Details

The calculator estimates taxes for fiscal years 2025–2029. By default it uses the council mill rates stored in the `defaultRates` object at the bottom of `index.html`:

```javascript
const defaultRates = {
  councilY0: 36.90,
  councilY1: 35.64,
  councilY2: 34.03,
  councilY3: 32.11,
  councilY4: 30.45,
  equalizedY0: 35.90,
  equalizedY1: 34.27,
  equalizedY2: 31.88,
  equalizedY3: 29.80,
  equalizedY4: 27.97,
  futureIncrease: 0.03
};
```

*(see `index.html` lines 370–383).* 

## Inputs

- **Current Assessed Value** – your post-revaluation assessment.
- **Old Assessed Value** – optional previous assessment before October 2024.
- **Revaluation Increase (%)** – optional percentage used to infer your old value.
- **Council Mill Rates** – FY 2025–2029 values, overridable in Advanced Configuration.
- **Equalized Rates** – comparison mill rates adjusted to full market value
  (70% to 100%) for cross-town or year-to-year analysis; not used in
  calculations.
- **Annual Budget Increase** – projected increase applied to FY 2028 and FY 2029.
The Advanced Configuration panel is hidden when the page loads. Expand it if you need to supply your old value or override any of the default rates.


## Calculation Steps

1. **Read Inputs**

   The script starts with the defaults from `defaultRates` and overrides them with any values entered in the Advanced Configuration panel.

2. **Determine Phase-In**

   If an old assessment (or revaluation percentage) is provided, the difference between the new and old values is phased in over four years:

```javascript
const diff     = postVal - oldVal;
const assessY1 = oldVal + 0.25 * diff;
const assessY2 = oldVal + 0.50 * diff;
const assessY3 = oldVal + 0.75 * diff;
const assessY4 = postVal;
```
*(see `index.html` lines 474–490).* 

3. **Compute Annual Taxes**

   For each fiscal year the assessed value is divided by 1000 and multiplied by the council mill rate. FY 2028 and FY 2029 include the optional `futureIncrease`:

```javascript
const taxY1 = millY1 * councilY1;
const taxY2 = millY2 * councilY2;
const taxY3 = (millY3 * councilY3) * (1 + futureIncrease);
const taxY4 = (millY4 * councilY4) * (1 + futureIncrease);
```
*(see `index.html` lines 480–489).* 

4. **Render Output**

   If an old assessment or percentage increase is supplied, the script renders the full phase-in table with year-over-year changes. Otherwise it shows a warning message asking for one of those values.

```javascript
resultsEl.innerHTML = html;
```
*(see `index.html` lines 373–436).* 

These calculations provide an estimate only and may not match your actual tax bill.
