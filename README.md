# Magnetic Field Inference from Spectropolarimetric Data

## Overview
This project analyzes photospheric magnetic fields in a solar active region using spectropolarimetric data from Hinode/SOT-SP, focusing on the Fe I lines at 630.15 nm and 630.25 nm. The magnetic field strength and orientation are inferred using the Weak Field Approximation (WFA) under conditions of unresolved Zeeman splitting. The workflow includes wavelength calibration, robust polarization mapping, Monte Carlo noise analysis, and systematic error propagation.

## Data
- **Input files:**
	- `datos_loop.fits`: Main spectropolarimetric data cube (Stokes I, Q, U, V)
	- `datos_sint.fits`: Synthetic data for Monte Carlo noise analysis
	- `atlas_6301_6302.fits`: Reference solar spectrum for calibration
- **Spectral lines:** Fe I 6301.5 Å and 6302.5 Å
- **Instrument:** Hinode Solar Optical Telescope Spectropolarimeter (SOT/SP)

## Methodology
1. **Wavelength Calibration:** Gaussian fitting of absorption lines for sub-pixel precision using `scipy.optimize.curve_fit`.
2. **Polarization Mapping:** Median-based statistics and adaptive peak finding for robust Stokes parameter extraction.
3. **Noise Characterization:** Median Absolute Deviation (MAD) from continuum windows.
4. **Monte Carlo Simulation:** Synthetic data to validate WFA inference and quantify systematic bias.
5. **Magnetic Field Inference:** Matrix-form WFA to derive line-of-sight ($B_\parallel$), transverse ($B_\perp$), and azimuth ($\chi_B$) field maps with propagated uncertainties.

## Requirements
- Python 3.8+
- Required libraries:
	- numpy
	- matplotlib
	- scipy
	- astropy
	- tqdm

Install dependencies with:
```bash
pip install numpy matplotlib scipy astropy tqdm
```

## Usage
1. Place the required FITS files (`datos_loop.fits`, `datos_sint.fits`, `atlas_6301_6302.fits`) in the project directory.
2. Open `magnetic_field_inference.ipynb` in Jupyter or VS Code.
3. Run all cells sequentially to reproduce the analysis, plots, and field maps.
4. Outputs include:
	 - Wavelength calibration plots
	 - Maps of $B_\parallel$, $B_\perp$, and $\chi_B$ with uncertainty estimates
	 - Monte Carlo noise/bias analysis

## Interpretation & Limitations
- **$B_\parallel$ (line-of-sight):** Robust to noise, reliable across the field of view.
- **$B_\perp$ (transverse):** More sensitive to noise; values below ~50 G may be noise-dominated.
- **Azimuth ($\chi_B$):** Only reliable where $B_\perp \gg 50$ G and uncertainty $<30^\circ$; otherwise, interpret with caution.
- **Noise levels:** Estimated from continuum as $\sigma \approx 1.7 \times 10^{-3}$.
- **Systematic bias:** Quantified and discussed in the notebook; see Monte Carlo results for details.
