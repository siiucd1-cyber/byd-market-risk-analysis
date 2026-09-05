# Market Risk — BYD (1211.HK)

> Market risk workstream of a group enterprise-risk-management project on BYD, Financial Risk Management module, MSc Accounting and Financial Management, UCD Smurfit (2026). **This file contains only the section I authored.**
>
> [中文版](market-risk-analysis-zh.md)

## Scope

Market risk is measured through three channels — price competition, raw material prices and foreign exchange — because these are the primary external routes into BYD's financial metrics. Price competition compresses selling prices and margin; raw material volatility moves the cost base; exchange-rate movements matter increasingly as overseas exposure grows.

| Risk channel | Why it matters for BYD | Transmission | What is analysed |
|---|---|---|---|
| Price competition | Highly competitive Chinese EV market where price cuts pressure vehicle pricing | Lower selling price → lower revenue per vehicle → margin compression → weaker profitability | Vehicle sales growth, revenue growth, gross margin, net margin, average revenue per vehicle |
| Raw material price | Production costs sensitive to battery-related raw materials and input-price movements | Higher input cost → higher cost of sales → lower gross margin → earnings pressure | Cost of sales, gross margin trend, lithium price trend, cost sensitivity |
| Foreign exchange | Overseas expansion increases exposure to rate movements and translation effects | FX moves → translated revenue volatility / cost mismatch / exchange gains and losses → profit volatility | Overseas revenue ratio, foreign currency exposure, exchange-rate sensitivity |

## Price competition risk

Price competition is a material market risk for BYD. In an intensely competitive Chinese EV market, price cuts and mix changes can support volume while eroding pricing power and profitability. Key indicators for 2023–2025 are used to assess the exposure.

Vehicle sales continued to rise between 2023 and 2025, but growth decelerated sharply — from 62.4% to 41.4% to 7.7%. Revenue growth decelerated in parallel, from 39.7% to 5.8%. Average revenue per vehicle fell from RMB 226,000 in 2023 to RMB 201,000 in 2024 and RMB 201,000 in 2025, and gross margin declined from 20.21% to 17.74%.

The combination matters more than any single line: volume still growing while unit revenue and margin fall together is the signature of price-led competition rather than weak demand.

Data: `data/byd-key-metrics-2023-2025.csv`

## Raw material price risk

Lithium carbonate is used as the principal input-cost proxy. It is chosen because it is closely tied to battery cost and offers the most transparent basis for sensitivity analysis within the scope of this report.

Quarterly lithium carbonate prices are plotted against BYD's quarterly gross margin for 2023–2025. The comparison is descriptive rather than causal, but it establishes that lithium price variation moves with profitability variation, which supports a cost-side sensitivity analysis.

To avoid assuming a 1:1 pass-through from lithium price to cost of sales, the analysis uses a **staged transmission mechanism** with sourced coefficients:

1. Lithium carbonate → battery cost: lithium accounts for **15.4%** of battery cost (CITIC Securities estimate)
2. Battery pack → vehicle value: battery packs account for **35%** of EV value (IEA benchmark)
3. Vehicle cost → cost of sales: vehicle cost accounts for **55.85%** of BYD's cost of sales (2025 annual report)

Giving:

```
ΔCoS = CoS₀ × 35% × 15.4% × ΔLC
```

A ±10% shock to the lithium price is then run through to cost of sales and gross margin. Higher lithium prices raise cost of sales and compress gross margin; negative shocks work in the opposite direction. Lithium-linked input cost therefore remains a material exposure for BYD.

Data: `data/lithium-carbonate-and-gross-margin-quarterly.csv` · `analysis/lithium-cost-sensitivity.csv`
Charts: `figures/fig-price-competition.png` · `figures/fig-lithium-vs-gross-margin.png` · `figures/fig-lithium-sensitivity.png`

## Foreign exchange risk

FX risk grows in importance as BYD expands abroad. With rising foreign revenue, exchange-rate movements affect the RMB value of sales and raise earnings volatility. The question examined here is whether increasing international exposure has made currency movement a more significant source of market risk.

Domestic revenue growth peaked in 2022 and turned negative (−9.2%) in 2025. Over the same period the overseas revenue share rose from 21.6% (2022) to 38.7% (2025), with overseas growth consistently exceeding domestic growth. BYD is therefore increasingly reliant on foreign markets, and exchange-rate movements are becoming more material to reported revenue and earnings stability.

BYD discloses overseas revenue without a regional breakdown. This analysis therefore does not attribute exposure to any single non-RMB currency; USD/CNY is used as a benchmark for aggregate external currency exposure.

Since 2020, USD/CNY and EUR/CNY have broadly tracked the 10-year sovereign yield differentials of the US and euro area against China. The relationship is not one-for-one over short periods, but the long-run co-movement supports using rate differentials as a reference for exchange-rate expectations.

Data: `data/overseas-revenue-mix.csv` · `data/fx-rates-quarterly.csv`
Charts: `figures/fig-usdcny-vs-yield-differential.png` · `figures/fig-eurcny-vs-yield-differential.png`

## Data note

All figures published here are compiled by me or derived from BYD's publicly filed annual reports and public commodity and FX series. Raw exports from licensed market-data terminals are not included in this repository.
