# Credit Valuation Adjustment for FX Forward and EUR IRS

This project implements a simplified Credit Valuation Adjustment framework for a portfolio consisting of an EUR/PLN FX Forward and a EUR receiver Interest Rate Swap.

The workflow includes CDS bootstrapping, Monte Carlo exposure simulation, portfolio netting and the impact of monthly Variation Margin.

## Project overview

The objective of the project is to estimate counterparty credit risk for derivative contracts using a simplified CVA framework.

The project covers:

- CDS spread bootstrapping
- default probability estimation
- FX Forward valuation
- Interest Rate Swap valuation
- Monte Carlo simulation of exposure profiles
- portfolio-level exposure aggregation
- CVA calculation for standalone instruments
- portfolio CVA with netting
- portfolio CVA with monthly Variation Margin

## Instruments

### FX Forward

- Buy EUR / sell PLN
- Notional: 1,000,000 EUR
- Maturity: 3 years
- Strike: 4.4439

### Interest Rate Swap

- Receiver EUR IRS
- Notional: 10,000,000 EUR
- Maturity: 3 years
- Fixed rate: 2.02%
- Floating leg: EURIBOR 3M

## Methodology

The project follows a simplified CVA calculation framework:

1. Bootstrap survival probabilities from CDS spreads.
2. Simulate FX and interest rate risk factors using Monte Carlo.
3. Calculate exposure profiles for the FX Forward and the IRS.
4. Aggregate exposures at portfolio level.
5. Include correlation between FX and interest rate risk factors.
6. Calculate CVA using expected exposure, discount factors and default probabilities.
7. Compare standalone CVA, uncollateralized portfolio CVA and collateralized portfolio CVA with monthly Variation Margin.

## Data

The repository includes public market data used in the project:

- EUR/PLN historical FX rates
- EURIBOR 3M / EUR interest rate proxy

Data sources:

- Stooq
- ECB Data Portal

## Key assumptions

- Calculation date: 31.12.2025
- Number of Monte Carlo simulations: 10,000
- Time step: monthly
- Recovery rate: 40%
- No wrong-way risk
- Counterparty default is assumed to be independent from market risk factors
- Simplified discounting assumptions are used

## Key results

| Case | CVA PLN |
|---|---:|
| FX Forward standalone | 3,695.58 |
| Receiver IRS standalone | 9,438.77 |
| Sum of standalone CVAs | 13,134.35 |
| Portfolio without Variation Margin | 10,590.01 |
| Portfolio with monthly Variation Margin | 2,087.49 |

Portfolio netting reduces CVA compared with the sum of standalone CVAs.  
Monthly Variation Margin significantly reduces the portfolio-level CVA.

## Repository structure

```text
cva-derivatives-python/
├── data/
│   ├── README.md
│   ├── euribor_3m_daily.csv
│   └── eurpln_d.csv
├── notebooks/
│   └── cva_fx_forward_irs.ipynb
├── .gitignore
├── LICENSE
├── README.md
└── requirements.txt
