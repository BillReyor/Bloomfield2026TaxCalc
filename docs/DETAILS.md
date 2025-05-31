# Calculation Details

The calculator estimates taxes for fiscal years 2026\u20132029. By default it uses the council mill rates stored in the `defaultRates` object at the bottom of `index.html`:

```javascript
const defaultRates = {
  councilY1: 35.64,
  councilY2: 34.03,
  councilY3: 32.11,
  councilY4: 30.45,
  equalizedY1: 34.27,
  equalizedY2: 31.88,
  equalizedY3: 29.80,
  equalizedY4: 27.97,
  futureIncrease: 0.03
};
```

*(see `index.html` lines 321\u2013332).* 

## Inputs

- **Current Assessed Value** \u2013 your post-revaluation assessment.
- **Old Assessed Value** \u2013 optional previous assessment before October 2024.
- **Revaluation Increase (%)** \u2013 optional percentage used to infer your old value.
- **Council Mill Rates** \u2013 FY 2026\u20132029 values, overridable in Advanced Configuration.
- **Equalized Rates** \u2013 provided for reference; not used in calculations.
- **Annual Budget Increase** \u2013 projected increase applied to FY 2028 and FY 2029.

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
*(see `index.html` lines 483\u2013487).* 

3. **Compute Annual Taxes**

   For each fiscal year the assessed value is divided by 1000 and multiplied by the council mill rate. FY 2028 and FY 2029 include the optional `futureIncrease`:

```javascript
const taxY1 = millY1 * councilY1;
const taxY2 = millY2 * councilY2;
const taxY3 = (millY3 * councilY3) * (1 + futureIncrease);
const taxY4 = (millY4 * councilY4) * (1 + futureIncrease);
```
*(see `index.html` lines 495\u2013499 and 505\u2013509).* 

4. **Render Output**

   Results are inserted into the `#results` element either with or without year-over-year differences, depending on whether an old value was provided.

```javascript
resultsEl.innerHTML = html;
```
*(see `index.html` lines 364\u2013441).* 

These calculations provide an estimate only and may not match your actual tax bill.
