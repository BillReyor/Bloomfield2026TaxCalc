# Bloomfield Tax Calculator

This repository contains a single-page calculator for estimating residential property taxes in the Town of Bloomfield for fiscal years 2026&ndash;2029. It is written entirely in HTML and JavaScript.

Default mill rates for each fiscal year are defined near the bottom of `Index.html` and used when calculating taxes. Open the **Advanced Configuration** panel (collapsed on load) if you need to override them or enter your old assessment or revaluation percentage.

## Getting Started

1. Clone or download this repository.
2. Open `Index.html` in a modern web browser.
3. Adjust the form fields to match your property information.
4. Click **Calculate My Taxes** to see yearly and monthly projections.

No build tools or server are required.

See [docs/DETAILS.md](docs/DETAILS.md) for details about the calculation process and how to modify the default assumptions.

## Repository Structure

- `Index.html` &ndash; main calculator page with embedded JavaScript
- `docs/` &ndash; documentation describing the calculations

## Contributing

Contributions are welcome. Please open an issue or submit a pull request if you have improvements.
