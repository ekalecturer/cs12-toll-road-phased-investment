# Serang–Panimbang Toll Road: IRR 13.96% Against a 13.55% Hurdle, 4.68% of Trials Make Money

**Case Study #12 in *The Feasibility Stress Test*. Primary lens: Capital Budgeting.**

An open-source Python reconstruction and browser simulator of a published reassessment of an Indonesian toll road. The base case clears the hurdle by 41 basis points of IRR. This repo shows which inputs that margin depends on.

## The case

The Serang–Panimbang Toll Road is a National Strategic Project (PSN) linking Banten's Serang area to the Tanjung Lesung Special Economic Zone, in three sections. Design changes, slow approvals and land-acquisition delays pushed the schedule back, so the authors reassess the investment under phased operation. Concession of 50 years (2019–2069), WACC 13.55% (30% equity, 70% debt), total investment cost IDR 8,288,497 million including interest during construction. Section 3 construction is government-funded (VGF) and excluded from the investor's capex.

## Citation

Utomo, W. & Utomo, C. (2026). *Investment Decision on the Serang–Panimbang Toll Road Project, Taking into Account the Phased Operation of the Toll Road.* Journal Research of Social Science, Economics, and Management, 5(12), 13061–13073. https://doi.org/10.59141/jrssem.v5i12.1605 (CC BY-SA 4.0)

## Confirmed findings (paper's own tables)

| Metric | Value |
|---|---|
| Base NPV (WACC 13.55%) | IDR 399,084 million |
| Base IRR / PI / discounted payback | 13.96% / 1.05 / 45 years |
| PPJT 2017 NPV (for comparison) | IDR 531,699 million |
| Deterministic turning points (NPV = 0) | tariff IDR 1,068/km; construction capex 109.4% of base; S1 ADT growth 84% of base; Section 2 open by 2024 |
| Monte Carlo (Crystal Ball, 10,000 trials, 12 inputs) | mean NPV -IDR 1,203,368 million; SD 687,674; 468 trials (4.68%) with NPV >= 0 |
| Tornado (stochastic) | tariff 33.93%; tariff + initial ADT S1 51.66% of explained variation |

Recommendations in the paper: set a tariff floor near IDR 1,068/km with biennial adjustment, re-validate traffic forecasts regularly, prioritise Section 2 scheduling and land acquisition, and manage the top five stochastic variables together. The paper reports no post-decision outcome.

## Reconstruction results (ILLUSTRATIVE, not the authors' numbers)

| Statistic | Paper | Reconstruction (10,000 trials) |
|---|---|---|
| Mean NPV (IDR million) | -1,203,368 | -952,297 |
| SD | 687,674 | 686,994 |
| P(NPV >= 0) | 4.68% | 8.95% |

Validation: tariff +/-15% lands within 7% of the paper's Table 17 values. Own arithmetic: base NPV is 4.8% of total investment cost; IRR margin over WACC is 0.41 points. Part of the paper's gap between a positive base case and a negative simulated mean comes from its own distributions: ADT growth is triangular 70% / 85% / 100% of plan, so its most likely value is already a 15% haircut. With every input at its mode, the reconstructed NPV is about -IDR 318 billion.

## Honesty disclosure

- **Full text was read through automated extraction** of the open-access PDF, not a manual page-by-page review. Check numbers against the paper before reuse.
- The paper does **not** publish its annual cash-flow workbook. This is a reconstruction from its published inputs with **two calibration scalars**: K (revenue scale, so base NPV matches) and PHI (an effective present-value factor on capex, back-solved from the paper's capex sensitivity). Only the tariff sensitivity rows are out-of-sample.
- **My assumptions:** the split of 50.677 km between Sections 1 and 2 (26.4 / 24.277 km; Section 3 is 33 km per the paper), traffic growth limited to 20 years after opening, no tax, class-mix multiplier from the Section 1 mix.
- **My extensions:** the optional traffic-correlation copula and the tariff-uplift / capex-support levers are not in the paper. The paper simulates all inputs as independent.
- The paper has internal inconsistencies (table cross-references, the Section 2 opening range 2023–2027 versus 2023–2026 among feasible trials, a PII cost note that does not multiply out). The reconstruction does not try to resolve them.
- The reconstruction's P(NPV >= 0) is about double the paper's. Do not read it as a replication.

## Run it

```bash
pip install -r requirements.txt
jupyter nbconvert --to notebook --execute notebook.ipynb
```

Or open `docs/index.html` in a browser for the interactive simulator (no build step). Enable GitHub Pages on the `docs/` folder to host it.

## License

MIT, copyright 2026 Eka Krisna Santoso. See `LICENSE`. The source paper remains the authors' work (CC BY-SA 4.0).

---
Part of **The Feasibility Stress Test**: real Monte Carlo and financial-engineering case studies for capex decisions.
