# Calculation Details

The calculator estimates taxes for fiscal years 2026&ndash;2029 using a four-year phase-in of your new assessed value. The yearly rate inputs are generated at runtime from arrays in the script, making it simple to adjust the assumptions. The defaults are:

```javascript
const years = [2026, 2027, 2028, 2029];
const defaultCouncil = [35.64, 34.03, 32.11, 30.45];
const defaultEqualized = [34.27, 31.88, 29.80, 27.97];
```

*(see `Index.html` lines 155&ndash;177)*.

## Inputs

- **Previous Assessed Value** – your assessment before the 2024 revaluation.
- **Current Assessed Value** – your new assessment after revaluation.
- **Pre-Reval Council Mill Rate** and **Equalized Rate** – mill rates prior to revaluation.
- **Base Mill Rate (Pre-Reval)** – used to calculate your current tax.
- **FY Rates** – council and equalized mill rates for each year of the phase-in.
- **Future Budget Increase** – an optional percentage increase applied after FY 2027.

## Calculation Steps

1. **Baseline Values**
   - Convert assessed values to property value by dividing by 0.7.
   - Compute the annual tax before revaluation:

     ```javascript
     const assessedMillPre = assessedPre / 1000;
     const annualTaxPre = assessedMillPre * millRatePre;
     ```
     *(see `Index.html` lines 192&ndash;197)*.
2. **Assessment Phase-In**
   - The change in assessment is phased in over four years:

     ```javascript
     const changeInAssessment = assessedPost - assessedPre;
     const quarterPhase = changeInAssessment / 4;
     const assessed = years.map((_, i) => assessedPre + quarterPhase * i);
     ```
     *(see `Index.html` lines 198&ndash;207)*.
3. **Yearly Taxes**
   - For each year, the script computes council tax and the increase relative to your pre-reval tax. Results are displayed in a table:

     ```javascript
     const council = assessedMill.map((mill, i) => mill * councilMill[i]);
     const inc = council.map(val => val - annualTaxPre);
     const mon = inc.map(val => val / 12);
     ```
     *(see `Index.html` lines 209&ndash;233)*.

4. **Rendering Results**
   - The calculator builds an HTML summary and inserts it into the `#results` element.

     ```javascript
     const resultsEl = document.getElementById('results');
     resultsEl.innerHTML = html;
     ```
     *(see `Index.html` lines 234&ndash;291)*.

These calculations provide an estimate only and may not match your actual tax bill.
