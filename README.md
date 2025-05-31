# Bloomfield Tax Calculator

This repository contains a single-page calculator for estimating residential property taxes in the Town of Bloomfield for fiscal years 2026&ndash;2029. It is written entirely in HTML and JavaScript.

Default mill rates for each fiscal year are defined near the bottom of `index.html` and are used when calculating taxes. You can override them via the "Advanced Configuration" section of the form.

## Getting Started

1. Clone or download this repository.
2. Open `index.html` (or navigate to the repository's root on GitHub Pages) in a modern web browser.

When hosted on GitHub Pages, visiting the repository's root URL will load the calculator automatically.
3. Adjust the form fields to match your property information.
4. Click **Calculate My Taxes** to see yearly and monthly projections.

No build tools or server are required.

See [docs/DETAILS.md](docs/DETAILS.md) for details about the calculation process and how to modify the default assumptions.

## Repository Structure

- `index.html` &ndash; main calculator page with embedded JavaScript
- `docs/` &ndash; documentation describing the calculations

## Contributing

Contributions are welcome. Please open an issue or submit a pull request if you have improvements.
