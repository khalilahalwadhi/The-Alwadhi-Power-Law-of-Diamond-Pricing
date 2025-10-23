# The Alwadhi Power-Law of Diamond Pricing

*A mathematical framework for gemstone valuation with empirical validation*

---

## Quick Interpretation

The **Alwadhi Power-Law** defines a universal relationship between a diamond's *price* and its *carat weight* using a single exponent (α ≈ 1.725).

**In short:** Price increases faster than size, following a predictable, fractal-based scaling law that remains stable across markets and time.

---

## Overview

This repository hosts the research paper, reference implementation, and example assets for the **Alwadhi Power-Law of Diamond Pricing** — a closed-form analytic model linking diamond price to carat weight with shape and quality modifiers.

Empirical testing across ~1.2 million trades (2019–2024) yields **R² ≈ 0.9874**, with stable parameters across markets.

---

## Core Result

### Price Function

```
P(W, s, qᵢ) = B(t) × W^α × Cₛ × Π Mqᵢ
```

**Where:**
- `W` = Carat weight
- `α` = 1.725 ± 0.012 (universal exponent)
- `B(t)` = Time-varying base price
- `Cₛ` = Shape coefficient
- `Mqᵢ` = Quality modifiers (color, clarity, etc.)
- **Valid range:** 0.20 ct ≤ W ≤ 10.00 ct

### Elasticity

```
εP,W = α
```

Constant price elasticity across all carat weights.

---

## Why It Matters

- ✅ **Transparent, analytic pricing** — Predictable scaling without opaque machine learning
- ✅ **Computationally lean** — Millisecond-level latency on standard CPUs
- ✅ **Empirically stable** — Robust across time, geography, and grading laboratories
- ✅ **Applicable beyond diamonds** — Framework generalizes to other gemstones with modified coefficients

---

## Repository Structure

```
📦 alwadhi-power-law
├── 📁 paper/          # LaTeX source and compiled PDF of the preprint
├── 📁 models/         # Python reference implementation
├── 📁 data/           # Synthetic datasets & summary statistics
├── 📁 examples/       # Notebooks: pricing, CIs, shape effects, portfolios
├── 📁 api/            # Lightweight pricing API (Flask/FastAPI)
└── 📄 README.md
```

---

## Quickstart

### Installation

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
```

### Using the Model

```python
from models.alwadhi import AlwadhiPowerLaw

model = AlwadhiPowerLaw(alpha=1.725, base_price=3127.43)

# Price a 1.5ct princess diamond
price = model.price(
    weight=1.50,
    shape="princess",
    quality_modifiers={"color": 0.98, "clarity": 1.03}
)
print(f"Price: ${price:,.2f}")

# 95% confidence interval
lo, hi = model.confidence_interval(price)
print(f"95% CI: ${lo:,.2f} - ${hi:,.2f}")
```

---

## Key Parameters

| Parameter | Meaning | Value |
|-----------|---------|-------|
| **α** (Alpha) | Universal exponent | 1.7245 [1.7123–1.7367] |
| **B(t)** | Base price | $3,127.43 (drift µ ≈ 0.0234) |
| **R²** | Model fit | 0.9874 |

### Shape Coefficients (Cₛ)

| Shape | Coefficient |
|-------|-------------|
| Round | 1.000 |
| Princess | 0.853 |
| Cushion | 0.897 |
| Oval | 0.801 |
| Emerald | 0.748 |
| Pear | 0.651 |
| Marquise | 0.598 |
| Radiant | 0.796 |
| Asscher | 0.719 |
| Heart | 0.682 |

---

## Applications

- 💎 **Retail & wholesale pricing** — Real-time quotation and confidence intervals
- 🏦 **Insurance & appraisal** — Replacement valuation and underwriting
- 📊 **Financial derivatives** — Risk modeling for diamond-linked instruments
- 🔍 **Market policy** — Transparency and deviation monitoring

---

## Assumptions & Scope

- ✓ Natural, colorless diamonds within **0.20–10 ct** range
- ✓ No extreme market shocks or atypical grades
- ⚠️ Fancy colors, synthetics, and ultra-large stones (>10 ct) may deviate due to non-scalable factors

---

## Reproducibility

- Synthetic datasets and example scripts included
- Commercial transaction data not shared, but summary statistics provided
- All code is open-source and documented

---

## Citation

```bibtex
@misc{alwadhi_powerlaw_2025,
  title   = {The Alwadhi Power-Law of Diamond Pricing: A Universal 
             Mathematical Framework for Gemstone Valuation},
  author  = {Al-Wadhi, Khalilah Aisha},
  year    = {2025},
  note    = {Preprint. CC BY 4.0},
}
```

---

## License

- **Paper & Documentation:** CC BY 4.0 International
- **Code:** MIT License (see individual subdirectories)

---

## Contact

**Khalilah Aisha Al-Wadhi**  
*Maison Alwadhi®*, Sydney (Australia)

📧 [k@maisonalwadhi.com.au](mailto:k@maisonalwadhi.com.au)  
🔗 [ORCID: 0009-0001-0934-7161](https://orcid.org/0009-0001-0934-7161)

---

## Supplement

📄 **[Download Preprint PDF](https://github.com/user-attachments/files/23103389/The_Alwadhi_Power_Law_of_Diamond_Pricing.pdf)**

---

<details>
<summary><b>📚 Expand: Theoretical Derivation</b></summary>

### Fractal Scaling Foundation

The power-law emerges from self-similar value accumulation across scales:

```
dP/dW = α × P/W
```

Integration yields:

```
P(W) = B × W^α
```

Where α encodes the rate at which marginal value compounds with mass.

### Dimensional Analysis

```
[Price] = [Base] × [Weight]^α
[USD] = [USD/ct^α] × [ct]^α
```

Dimensionally consistent for any positive α.

</details>

<details>
<summary><b>🔬 Expand: Dataset Methodology</b></summary>

### Data Sources
- **Primary:** Rapaport Diamond Report (2019–2024)
- **Secondary:** GIA, AGS, and HRD certified transaction records
- **Volume:** ~1.2M validated trades

### Preprocessing
1. Outlier removal (±3σ residuals)
2. Grading harmonization across labs
3. Currency normalization (USD 2024)

### Validation
- **Training:** 70% (840K records)
- **Testing:** 30% (360K records)
- **Cross-validation:** 5-fold stratified by shape

</details>

---

### Contributing

We welcome contributions! Please see `CONTRIBUTING.md` for guidelines.

**Areas of interest:**
- Extensions to colored diamonds
- Laboratory-grown diamond coefficients
- Alternative gemstones (sapphire, ruby, emerald)
- Integration with blockchain provenance systems

---

### Acknowledgments

Special thanks to the gemological research community and participating trade organizations for data partnerships.

---
