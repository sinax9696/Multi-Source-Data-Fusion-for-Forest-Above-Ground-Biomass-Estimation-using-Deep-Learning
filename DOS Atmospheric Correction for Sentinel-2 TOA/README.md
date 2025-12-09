# DOS Atmospheric Correction for Sentinel-2

**A Lightweight, Transparent, Research-Ready Python Implementation**

## 🛰 Introduction

This repository contains a clean and fully transparent implementation of Dark Object Subtraction (DOS) for Sentinel-2 Level-1C TOA imagery (scaled to 0–10000). The module supports multiple DOS models, NDWI-based water masking, and visualization tools useful for GIS analysis and machine learning preprocessing.

## ⭐ Features

| Feature | Description |
|---------|-------------|
| **DOS1–DOS4** | From basic subtraction to Rayleigh + aerosol models |
| **Water-Masked DOS** | More accurate Dark Object estimation using NDWI |
| **Rayleigh optical thickness** | Band-specific coefficients included |
| **Sentinel-2 Ready** | Fully compatible with multi-band TOA GeoTIFFs |
| **Visualization Tools** | Histograms, comparison figures, diff maps |
| **Lightweight & Fast** | Uses NumPy + Rasterio, no heavy dependencies |

## 📦 Installation

```bash
pip install rasterio numpy matplotlib
```

## 🚀 Quick Usage Example

```python
from dos_corrector import DOSCorrector

corrector = DOSCorrector(percentile=1, dos_method='DOS2')

corrected, dark_values = corrector.simple_dos(
    image_path="sentinel_toa.tif",
    output_path="sentinel_dos2.tif",
    sun_elevation=55.0
)
```

## 🌊 Water-Masked DOS

Water bodies offer extremely stable low-reflectance values. This makes them ideal for estimating atmospheric path radiance.

### ✔ NDWI Formula

$
\text{NDWI} = \frac{\rho_{\text{Green}} - \rho_{\text{NIR}}}{\rho_{\text{Green}} + \rho_{\text{NIR}}}
$

### ✔ Usage Example

```python
corrector = DOSCorrector(percentile=1, dos_method='DOS2')

corrected, dark, water_mask = corrector.dos_with_water_mask(
    "sentinel_toa.tif",
    "sentinel_dos_water.tif",
    sun_elevation=55,
    green_band_idx=2,
    nir_band_idx=7
)
```


## 🎨 Visualization Tools

`plot_comparison()` generates:

* Original TOA map
* DOS-corrected map
* Difference heatmap
* Histograms & statistics

### Example Usage

```python
corrector.plot_comparison(
    original_path="sentinel_toa.tif",
    corrected_path="sentinel_dos2.tif",
    band_idx=3
)
```


## ⚙ Algorithm Summary

### 1️⃣ Dark Object Extraction

$
\rho_{\text{dark}} = \text{percentile}(\text{valid\_pixels}, 1\%)
$

### 2️⃣ Atmospheric Transmittance (Rayleigh)

$
T_v = \exp\left(-\frac{\tau_r}{\cos(\theta_z)}\right)
$

Where:
- $\tau_r$ = Rayleigh optical thickness
- $\theta_z$ = solar zenith angle

### 3️⃣ Final Surface Reflectance

$
\rho_{\text{surface}} = \frac{\rho_{\text{TOA}} - \rho_{\text{dark}}}{T_v}
$

Values are clipped to: $[0, 10000]$

## 📊 DOS Method Comparison

| Method | Includes | Recommended For |
|--------|----------|-----------------|
| **DOS1** | Path radiance only | Quick preprocessing |
| **DOS2** | Rayleigh scattering | Best general option |
| **DOS3** | Rayleigh + Aerosol | Hazy scenes |
| **DOS4** | More complete model | Difficult atmospheres |
| **Water-Masked** | NDWI DO estimation | Scenes containing water |

## 📌 Notes & Limitations

* DOS is a simplified correction model
* Not a replacement for Sen2Cor, 6S, or MAJA
* Requires correct sun elevation metadata
* Adjacency effects are not modeled


## 🤝 Contributing

Pull requests and issues are welcome. Feel free to suggest features such as:

* GPU acceleration
* Numba optimization
* GEE JavaScript port

## 📬 Contact

For questions or collaborations: **GitHub Issues** 

