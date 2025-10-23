
# The Alwadhi Power-Law of Diamond Pricing

*A mathematical framework for gemstone valuation with empirical validation*

## Overview

This repository hosts the research paper, reference implementation, and example assets for the **Alwadhi Power-Law of Diamond Pricing**, a closed-form model relating diamond price to carat weight with quality and shape modifiers. The framework reports a universal exponent **α ≈ 1.725** and explains its emergence from scarcity distributions, fractal geology, and market equilibrium. Empirical tests across ~1.2M transactions (2019–2024) show **R² ≈ 0.9874** with stable coefficients across markets. 

## Core result

The pricing function:
[
P(W,s,\mathbf{q}) ;=; B(t);\cdot; W^{\alpha};\cdot; C_s;\cdot; \prod_i M_{q_i},
]
with **α = 1.725 ± 0.012**, time-varying base price (B(t)), shape coefficient (C_s), and quality modifiers (M_{q_i}). Typical validity range: **W ∈ [0.20, 10.00] ct**. 

## Why it matters

* **Transparent, analytic pricing** with constant elasticity ( \epsilon_{P,W}=\alpha ).
* **Computationally lean** vs ML baselines (millisecond latency).
* **Consistent across markets/time**, supporting appraisal, underwriting, and portfolio use-cases. 

## Repository structure

```
/paper        # LaTeX source and compiled PDF of the preprint
/models       # Python reference implementation of the power-law
/data         # Synthetic datasets and summary statistics (no raw trade data)
/examples     # Notebooks & scripts: pricing, CIs, shape effects, portfolios
/api          # Lightweight pricing API skeleton (Python/Flask or FastAPI)
```

## Quickstart

### Install

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
```

### Use the model (Python)

```python
from models.alwadhi import AlwadhiPowerLaw

model = AlwadhiPowerLaw(
    alpha=1.725,
    base_price=3127.43,  # example B(t)
)

# 1. Price a stone
price = model.price(weight=1.50, shape="princess",
                    quality_modifiers={"color": 0.98, "clarity": 1.03})
print(price)  # -> USD estimate

# 2. 95% confidence interval
lo, hi = model.confidence_interval(price)
print(lo, hi)

# 3. Marginal price per extra carat at W
mp = model.marginal_price(weight=1.50, shape="princess")
```

Reference implementation and parameter defaults follow the paper’s Appendix code. 

## Key parameters (from the paper)

* **α (exponent):** 1.7245 [1.7123, 1.7367]
* **B (base price example):** $3,127.43 (drift µ ≈ 0.0234)
* **Shape coefficients (C_s) (examples):** round=1.000, princess≈0.853, cushion≈0.897, oval≈0.801, emerald≈0.748, pear≈0.651, marquise≈0.598, radiant≈0.796, asscher≈0.719, heart≈0.682.
* **Performance:** R² ≈ 0.9874; strong temporal & geographic stability. 

## Applications

* **Retail & wholesale pricing** (real-time quotes; CI for quotes).
* **Insurance/appraisal** (replacement value; policy pricing).
* **Risk & derivatives** (VaR on diamond portfolios; Black-Scholes-style options on indices).
* **Market surveillance & policy** (deviation monitoring; transparency). 

## Assumptions & scope

* Natural, colorless diamonds; standard quality ranges; **W ∈ [0.20, 10.00] ct**.
* No supply shocks or extreme conditions.
* Fancy colors, synthetics, and ultra-large stones (>10 ct) may deviate (idiosyncratic effects dominate). 

## Reproducibility & data

* Code, synthetic datasets, and examples are included.
* **Commercial transaction data are not shared**; summary statistics provided for replication. 

## Citing this work

```
@misc{alwadhi_powerlaw_2025,
  title   = {The Alwadhi Power-Law of Diamond Pricing: A Universal Mathematical Framework for Gemstone Valuation},
  author  = {Al-Wadhi, Khalilah Aisha},
  year    = {2025},
  note    = {Preprint. CC BY 4.0},
}
```

Please also cite sources you use from the paper’s bibliography. 

## License

**CC BY 4.0 International** for the paper. Code licensing is indicated per subdirectory (default: permissive; see headers). 

## Contact

**Khalilah Aisha Al-Wadhi** — Maison Alwadhi® — Sydney, Australia
Corresponding author: [k@maisonalwadhi.com.au](mailto:k@maisonalwadhi.com.au) (ORCID 0009-0001-0934-7161). 

---

[The_Alwadhi_Power_Law_of_Diamond_Pricing__A_Novel_Mathematical_Framework_for_Gemstone_Valuation__Copy_.pdf](https://github.com/user-attachments/files/23099989/The_Alwadhi_Power_Law_of_Diamond_Pricing__A_Novel_Mathematical_Framework_for_Gemstone_Valuation__Copy_.pdf)

