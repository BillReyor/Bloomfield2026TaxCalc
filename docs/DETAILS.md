# Calculation Details

This calculator models Bloomfield's four-year phase-in of the 2024 property revaluation. Equalized mill rates come from the town's spreadsheet and represent the revenue-neutral baseline for each phase-in level. After adding the council's budget increase, they become the actual mill rates used to compute taxes.

```javascript
const defaultRates = {
  councilY0: 37.49,
  councilY1: 35.64,
  councilY2: 34.03,
  councilY3: 32.11,
  councilY4: 30.45,
  equalizedY0: 27.97,
  equalizedY1: 34.27,
  equalizedY2: 31.88,
  equalizedY3: 29.80,
  equalizedY4: 27.97,
  futureIncrease: 0.03
};
```
*(see `index.html` lines 370&ndash;383).* 

## Inputs

- **Current Assessed Value** – post-revaluation assessment.
- **Old Assessed Value** – previous assessment before October 2024 (optional).
- **Revaluation Increase (%)** – percent increase used to infer your old value (optional).
- **Council Mill Rates** – FY 2025–2029 rates; overridable in Advanced Configuration.
- **Equalized Rates** – revenue-neutral rates for each phase of the revaluation.
- **Annual Budget Increase** – projected increase applied beyond FY 2026.

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
3. **Determine Mill Rates** – for each year the town sets an equalized rate that would keep revenue flat at that phase-in level. The council's adopted budget increase is then layered on top to get the actual mill rate.
4. **Compute Annual Taxes** – each phased assessment is divided by 1000 and multiplied by the appropriate mill rate.
5. **Render Output** – the page displays estimated taxes for FY 2025–FY 2029 along with year-over-year changes.

These calculations provide estimates only and may not match your exact bill.
