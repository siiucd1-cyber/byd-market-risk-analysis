# Market Risk — BYD (1211.HK) · Revised

> Market risk workstream of a group enterprise-risk-management project on BYD, Financial Risk Management module, MSc Accounting and Financial Management, UCD Smurfit (2026). **This file contains only the section I authored.**
>
> This is the post-submission revised version; corrections are listed at the end. The original submission is [`market-risk-analysis.pdf`](market-risk-analysis.pdf). · [中文版](market-risk-analysis-zh.md)

## Scope

Market risk is measured through three channels (price competition, raw material prices and foreign exchange) because these are the primary external routes into BYD's financial metrics. All figures are in RMB; the base year is 2025.

| Risk channel | Why it matters for BYD | Transmission | What is analysed |
|---|---|---|---|
| Price competition | Highly competitive Chinese EV market where price cuts pressure vehicle pricing | Lower selling price → lower revenue per vehicle → margin compression | Volume and revenue growth, unit revenue, gross margin, volume–price bridge |
| Raw material price | Battery-related input prices drive production cost | Higher input cost → higher cost of sales → lower gross margin | Lithium price, staged transmission, sensitivity |
| Foreign exchange | Overseas expansion increases currency exposure | FX moves → translated foreign revenue / cost mismatch → profit volatility | Overseas revenue share, net exposure, natural-hedge ratio |

## Price competition risk

Between 2023 and 2025, vehicle sales growth slowed from 62.4% to 7.7% and RMB revenue growth from 42.0% to 3.5%. Auto revenue per vehicle fell in each year (RMB 160,100 → 144,600 → 141,000) and gross margin declined from 20.21% to 17.74%.

A volume–price bridge of auto segment revenue shows that in 2025 revenue rose RMB 31.3bn: volume contributed +RMB 47.7bn and price (including mix) −RMB 16.5bn. The price effect keeps offsetting part of the volume gain, which points to weakening pricing power.

At the same time, domestic revenue fell 11.2% in 2025 while overseas revenue grew 40.1%. The domestic market faces pressure on both volume and price, and group growth depends on overseas sales. Price competition is a material risk, but it does not on its own explain 2025 domestic performance.

Data: `data/byd-key-metrics-2023-2025.csv` · `analysis/auto-revenue-volume-price-bridge.csv`

## Raw material price risk

Lithium carbonate is used as the principal input-cost proxy. The quarterly comparison of lithium price and gross margin over 2023–2025 is descriptive: margin rose while lithium fell in 2023, but after 2024 lithium traded flat at low levels and margin swings came mainly from other factors.

To avoid assuming 1:1 transmission, a staged chain is used: lithium at 15.4% of battery cost (CITIC Securities estimate), battery pack at 35% of the vehicle (IEA benchmark), and auto cost at 77.99% of cost of sales (2025 segment data). This gives lithium-related cost of about RMB 27.8bn, or 4.2% of cost of sales.

```
CoS₁ = CoS₀ + lithium-related cost × Δlithium price × (1 − pass-through)
```

With no pass-through, a ±10% lithium move shifts gross margin by ∓0.35 pp (17.40%–18.09%), about RMB 2.8bn pre-tax or 8.5% of net profit; ±30% corresponds to ∓1.04 pp.

Both coefficients are external estimates. A rough bottom-up calculation puts lithium cost at about one third of the top-down figure, so these results are closer to an upper bound and should be calibrated with installed-capacity and battery-mix data.

Data: `data/lithium-carbonate-and-gross-margin-quarterly.csv` · `analysis/lithium-cost-sensitivity.csv`

## FX risk

Overseas revenue share rose from 21.6% in 2022 to 38.7% in 2025 (RMB 310.7bn) while domestic revenue turned negative, so BYD increasingly depends on foreign markets. The currency split of overseas revenue is not disclosed, so USD/CNY is used as the benchmark for aggregate non-RMB exposure. Since 2020, USD/CNY and EUR/CNY have broadly tracked the 10-year yield differential against China, which serves as a reference for exchange-rate expectations.

Sensitivity uses a net-exposure formula:

```
ΔGross profit = overseas revenue × w × ΔUSD/CNY × (1 − h)
```

where w is the USD (and USD-linked) share and h is foreign-currency cost as a share of foreign-currency revenue (natural hedge). With w = 50%:

- h = 0 (exported vehicles produced entirely at RMB cost): an 8% RMB appreciation reduces gross profit by about RMB 12.4bn, −1.55 pp of gross margin, equivalent to 38% of net profit.
- h = 50%: −0.77 pp.
- h = 80.5% (implicit in the submitted formula): −0.30 pp.

Unless the foreign-currency cost share is high, the FX impact on gross margin exceeds that of a ±10% lithium move. h is the key unknown that decides the conclusion.

Data: `data/overseas-revenue-mix.csv` · `data/fx-rates-quarterly.csv` · `analysis/fx-overseas-gross-profit-sensitivity.csv`

## Conclusions and monitoring

1. **FX**: highest priority. Require disclosure or internal tracking of the foreign-currency cost share (h) and the hedge ratio; set trigger levels from the margin impact of a given RMB appreciation.
2. **Price competition**: track revenue per vehicle and the price effect in the volume–price bridge, separating price cuts from mix shifts.
3. **Lithium**: manageable but not negligible. Track the carbonate price and pass-through capacity, and calibrate the transmission coefficients with physical-volume data.

Mitigation: product differentiation and cost control for price competition; long-term contracts, diversified sourcing and selective hedging for lithium; more local overseas production (raising h) and forward contracts for FX.

## Corrections to the submitted version

1. Auto cost share: the submission used 2023 auto cost, giving 55.85%; the correct 2025 value is 77.99%.
2. Lithium transmission: the submitted spreadsheet scaled lithium cost back up to total cost of sales, producing 1:1 transmission; now an additive cost change.
3. Gross margin: the submission used (revenue − cost) / cost; now (revenue − cost) / revenue.
4. FX: the submission applied the shock to overseas gross profit, implying an 80.5% natural hedge; h is now an explicit parameter.
5. Currency basis: the submission computed growth and unit revenue in USD at year-end rates; everything is now restated in RMB.
