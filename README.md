# BYD Market Risk Analysis

**English** · [中文](README-zh.md)

Market risk workstream of a group project on **enterprise risk management for BYD (1211.HK)**, completed for the Financial Risk Management module, MSc Accounting and Financial Management, UCD Smurfit Business School (2026).

This repository contains **only the market risk section, which I authored**. The wider group report (governance framework, operational risk, country risk) is not included.

> **Revised version.** After submission I re-audited the working spreadsheet cell by cell against the Wind source files and corrected five errors (see [Corrections to the submitted version](#corrections-to-the-submitted-version)). All figures on this page and in `data/` and `analysis/` are the corrected results. [`report/market-risk-analysis.pdf`](report/market-risk-analysis.pdf) is kept unchanged as the original submission.

## Question

BYD is growing quickly in scale and in overseas exposure, but into a more crowded and more volatile environment. Which external channels actually transmit into earnings, by how much, and which one deserves the most attention?

Three channels are examined: **price competition**, **raw material prices**, and **foreign exchange**. All figures are in RMB; the base year is 2025.

## Findings

### 1. Price competition: unit revenue has fallen three years running, and growth now comes from abroad

| | 2023 | 2024 | 2025 |
|---|---|---|---|
| Vehicle sales (m units) | 3.02 | 4.27 | 4.60 |
| Vehicle sales growth | 62.4% | 41.4% | 7.7% |
| Revenue growth | 42.0% | 29.0% | 3.5% |
| Auto revenue per vehicle (RMB '0000) | 16.01 | 14.46 | 14.10 |
| Change in revenue per vehicle | −8.3% | −9.7% | −2.5% |
| Gross margin | 20.21% | 19.44% | 17.74% |
| Domestic revenue growth | 32.9% | 25.6% | **−11.2%** |
| Overseas revenue growth | 75.2% | 38.5% | 40.1% |

Volume–price bridge of auto segment revenue (RMB bn):

| | Revenue change | Volume effect | Price effect (incl. mix) |
|---|---|---|---|
| 2024 | +133.9 | +200.1 | −66.2 |
| 2025 | +31.3 | +47.7 | −16.5 |

- Revenue per vehicle has declined every year, and the price effect keeps offsetting part of the volume gain. Pricing power is weakening.
- In 2025 domestic revenue fell 11.2% and all growth came from overseas (+40.1%). The domestic picture is **pressure on both volume and price**, so it cannot be attributed to price competition alone.
- Without model-level data, the price effect includes mix changes (e.g. a higher share of cheaper models) and cannot be split further.

![Unit revenue and gross margin, 2023–2025](figures/fig-price-competition.svg)

Data: [`data/byd-key-metrics-2023-2025.csv`](data/byd-key-metrics-2023-2025.csv) · [`analysis/auto-revenue-volume-price-bridge.csv`](analysis/auto-revenue-volume-price-bridge.csv)

### 2. Lithium: a ±10% shock moves gross margin by about 0.35 pp

A staged transmission is used rather than a 1:1 link between lithium and cost of sales:

```
Lithium-related cost = CoS × auto share of CoS × battery pack share × lithium share of battery
                     = RMB 661.3bn × 77.99% × 35% × 15.4% ≈ RMB 27.8bn (4.2% of CoS)
CoS₁ = CoS₀ + lithium-related cost × Δlithium price × (1 − pass-through)
```

| Stage | Coefficient | Source |
|---|---|---|
| Lithium carbonate → battery cost | 15.4% | CITIC Securities estimate (external) |
| Battery pack → vehicle | 35% | IEA benchmark (value basis, external) |
| Auto cost → BYD cost of sales | 77.99% | BYD 2025 segment data |

| Lithium shock | −30% | −10% | 0 | +10% | +30% |
|---|---|---|---|---|---|
| Gross margin | 18.78% | 18.09% | 17.74% | 17.40% | 16.71% |
| Change (pp) | +1.04 | +0.35 | — | −0.35 | −1.04 |

Each 10% move in lithium is worth about RMB 2.8bn pre-tax, or 8.5% of 2025 net profit, assuming no pass-through.

**Limitation:** a rough bottom-up check (4.6m vehicles × ~40 kWh × ~0.6 kg LCE/kWh × 2025 average price) gives only about RMB 8.2bn of lithium cost, roughly one third of the top-down figure. The 15.4% coefficient may date from a higher-price period, so the table above is closer to an **upper bound**.

![Lithium shock vs gross margin](figures/fig-lithium-sensitivity.svg)

![Quarterly lithium carbonate price vs BYD gross margin](figures/fig-lithium-vs-gross-margin.png)

Data: [`analysis/lithium-cost-sensitivity.csv`](analysis/lithium-cost-sensitivity.csv)

### 3. FX exposure is rising structurally

Overseas revenue share rose from 21.6% (2022) to 38.7% (2025, RMB 310.7bn). BYD does not split overseas revenue by currency, so USD/CNY is used as the benchmark for aggregate non-RMB exposure.

Since 2020, USD/CNY and EUR/CNY have broadly tracked the 10-year sovereign yield differential of the US and the euro area against China, which serves as a reference for exchange-rate expectations.

![USD/CNY vs US–China 10-year yield differential](figures/fig-usdcny-vs-yield-differential.png)

![EUR/CNY vs euro area–China 10-year yield differential](figures/fig-eurcny-vs-yield-differential.png)

### 4. FX sensitivity depends on the natural-hedge ratio, and is probably larger than lithium

```
ΔGross profit = overseas revenue × w × ΔUSD/CNY × (1 − h)
```

- *w*: USD (and USD-linked) share of overseas revenue; scenario value 50%
- *h*: foreign-currency cost as a share of foreign-currency revenue, i.e. the degree of natural hedging. h = 0 means exported vehicles are produced entirely at RMB cost; h = 80.5% (overseas cost / overseas revenue) reproduces the formula in the submitted version

**Impact on group gross margin (pp, w = 50%)**

| ΔUSD/CNY | h = 0% | h = 25% | h = 50% | h = 80.5% (submitted assumption) |
|---|---|---|---|---|
| −8% | −1.55 | −1.16 | −0.77 | −0.30 |
| −4% | −0.77 | −0.58 | −0.39 | −0.15 |
| +4% | +0.77 | +0.58 | +0.39 | +0.15 |
| +8% | +1.55 | +1.16 | +0.77 | +0.30 |

At h = 0, an 8% RMB appreciation cuts gross profit by about RMB 12.4bn, equivalent to 38% of net profit. Even at h = 50%, the impact (−0.77 pp) exceeds that of a ±10% lithium move (0.35 pp).

**Conclusion:** the submitted version found that FX mainly affects the translation of overseas profit rather than group-wide margin. That result came from the formula's implicit 80.5% natural hedge. Once the assumption is relaxed, **FX is likely a larger market risk than lithium at 2025 levels**. The key unknown is h, so the board should require disclosure or tracking of the foreign-currency cost share and the hedge ratio as a first-order monitoring metric.

![FX shock vs gross margin](figures/fig-fx-sensitivity.svg)

Data: [`analysis/fx-overseas-gross-profit-sensitivity.csv`](analysis/fx-overseas-gross-profit-sensitivity.csv)

## Corrections to the submitted version

| # | Submitted version | Problem | Correction |
|---|---|---|---|
| 1 | Auto cost = 55.85% of cost of sales | The spreadsheet divided **2023** auto cost by 2025 cost of sales | Correct 2025 value: 77.99% |
| 2 | ±10% lithium → ±10% cost of sales | The formula scaled lithium cost back up to total cost of sales, producing 1:1 transmission and contradicting the stated method | CoS₁ = CoS₀ + Δlithium cost |
| 3 | Base "gross margin" 52.4% | Computed as (revenue − cost) / cost, i.e. a mark-up | (revenue − cost) / revenue = 17.74% |
| 4 | FX shock applied to overseas gross profit | Implicitly assumes overseas cost and revenue share a currency (h = 80.5%), understating exposure | Net exposure on foreign-currency revenue, with h as a parameter |
| 5 | Growth rates and unit revenue in USD | Wind GSD converts at each year-end rate, so growth rates mix in FX moves; unit revenue was actually in USD '000 | All figures restated in RMB, matching the annual reports |

After correction, 2025 revenue per vehicle still fell 2.5% (it looked flat in USD), which gives the price-pressure finding firmer support.

## Repository structure

```
report/     Submitted report PDF (original) + revised condensed write-ups (EN/ZH)
data/       Key metrics (RMB), quarterly lithium price and margin, FX rates, overseas revenue mix
analysis/   Volume–price bridge, lithium sensitivity, FX sensitivity (ΔUSD/CNY × natural-hedge ratio)
figures/    Charts
```

## Data note

Financial data are from Wind (GSD income statement and segment breakdown), converted back to RMB at the same year-end rates Wind used, which reproduces the reported RMB figures (e.g. 2024 revenue RMB 777.1bn). **Raw exports from paid terminals are not included in this repository.**

## Methods and tools

Excel for data preparation and sensitivity modelling (all intermediate values are formulas and traceable); Python for CSV outputs and charts.

---

Wang Danyang · woshiwdy@163.com
