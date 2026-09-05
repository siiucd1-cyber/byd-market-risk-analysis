# BYD Market Risk Analysis

**English** · [中文](README-zh.md)

Market risk workstream of a group project on **enterprise risk management for BYD (1211.HK)**, completed for the Financial Risk Management module, MSc Accounting and Financial Management, UCD Smurfit Business School (2026).

This repository contains **only the market risk section, which I authored**. The wider group report (governance framework, operational risk, country risk) is not included.

📄 **[Read the full report (PDF)](https://github.com/siiucd1-cyber/byd-market-risk-analysis/blob/main/report/market-risk-analysis.pdf)** — the submitted coursework document, with the original charts and tables. A condensed write-up is in [`report/market-risk-analysis.md`](report/market-risk-analysis.md).

## Question

BYD is growing quickly in scale and in overseas exposure, but into a more crowded and more volatile environment. Which external channels actually transmit into earnings, and by how much?

Three channels are examined: **price competition**, **raw material prices**, and **foreign exchange**.

## Findings

### 1. Price competition is already visible in the numbers

| | 2023 | 2024 | 2025 |
|---|---|---|---|
| Vehicle sales (m units) | 3.02 | 4.27 | 4.60 |
| Vehicle sales growth | 62.4% | 41.4% | 7.7% |
| Revenue growth | 39.7% | 27.1% | 5.8% |
| Avg. revenue per vehicle (RMB '0000) | 22.60 | 20.11 | 20.06 |
| Gross margin | 20.21% | 19.44% | 17.74% |

Volumes still rise, but growth decelerates sharply while average revenue per vehicle and gross margin fall together — the signature of price-led competition rather than demand weakness.

### 2. Lithium transmits to cost of sales through a three-stage chain

Rather than assuming a 1:1 pass-through from lithium price to cost, the analysis uses a staged mechanism with sourced coefficients:

```
ΔCoS = CoS₀ × 35% × 15.4% × ΔLC
```

| Stage | Coefficient | Source |
|---|---|---|
| Lithium carbonate → battery cost | 15.4% | CITIC Securities estimate |
| Battery pack → vehicle value | 35% | IEA benchmark |
| Vehicle cost → BYD cost of sales | 55.85% | BYD 2025 annual report |

A ±10% lithium price shock is then run through to cost of sales and gross margin (`analysis/lithium-cost-sensitivity.csv`).

### 3. FX exposure is rising structurally

Overseas revenue share moved from 21.6% (2022) to 38.7% (2025), while domestic revenue growth turned negative (−9.2%) in 2025. Because BYD discloses overseas revenue without a regional breakdown, USD/CNY is used as a proxy for aggregate non-RMB exposure rather than assigning exposure to any single currency.

USD/CNY and EUR/CNY are shown to track the 10-year sovereign yield differential against China over 2020–2025, which is used as the reference for exchange-rate expectations.

### 4. Two sensitivity grids quantify the downside

| Grid | Shock range | Output |
|---|---|---|
| Lithium cost | −10% to +10%, 2% steps | Cost of lithium, cost of sales, gross margin — `analysis/lithium-cost-sensitivity.csv` |
| FX translation | ΔUSD/CNY −8% to +8%, 1% steps × USD share of overseas revenue 30%–70% | Overseas gross profit, $bn — `analysis/fx-overseas-gross-profit-sensitivity.csv` |

The FX grid uses `Overseas Gross Profit₁ = Overseas Gross Profit₀ × (1 + w × ΔUSD/CNY)`, base $8.60bn. An 8% USD/CNY move shifts overseas gross profit by $0.21bn at w=30% and $0.48bn at w=70% — FX risk lands on translated overseas profit, not on company-wide margins.

## Repository contents

```
report/     full report (PDF, as submitted) + condensed write-up in English and Chinese
data/       key metrics, quarterly lithium prices and gross margin, FX rates, overseas revenue mix
analysis/   sensitivity grids: lithium cost, FX translation
figures/    charts: price competition, lithium vs gross margin, lithium sensitivity, USD/CNY and EUR/CNY vs yield differentials
```

## Data note

All figures published here are either compiled by me or derived from BYD's publicly filed annual reports and public commodity/FX series. Raw exports from licensed market-data terminals are deliberately **not** included in this repository.

## Method and tools

Excel for data assembly and sensitivity modelling; staged transmission modelling for the cost channel; descriptive and comparative analysis for the FX channel. Coefficients are sourced rather than assumed, and each conclusion is traceable to the underlying series in `data/`.

---

Wang Danyang · woshiwdy@163.com
