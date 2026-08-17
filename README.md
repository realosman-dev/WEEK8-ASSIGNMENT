# Week 8 — Supply Chain Optimization

Author: Finley Maranga

## Overview
This repository contains the Week 8 deliverables covering demand forecasting, inventory
optimization, and distribution planning for a simulated retail supply chain, plus the
accompanying management briefing and hackathon reflection.

## Contents
| Path | Description |
|---|---|
| `notebooks/week8_supply_chain_optimization.ipynb` | Main technical notebook: data prep, Prophet forecasting, safety stock / reorder point calculation, stockout simulation, and PuLP distribution optimization |
| `data/historical_demand.csv` | Historical daily demand dataset used for forecasting |
| `slides/Week8_Ops_Review_Slides.pdf` | Slide deck for the Quarterly Operations Review management briefing |
| `video/Week8_Ops_Review_[YourName].mp4` | 15-minute recorded presentation (or see link below if hosted externally) |
| `hackathon2_reflection.md` | Team reflection on Hackathon #2 |

## How to run the notebook
```bash
pip install prophet pulp pandas numpy matplotlib scikit-learn
jupyter notebook notebooks/week8_supply_chain_optimization.ipynb
```
Run all cells top to bottom. The notebook auto-detects whether `prophet`/`pulp` are installed
and uses them as the primary methods; install both before running for the required output.

## Key results
- 45-day demand forecast evaluated via MAPE/RMSE on a holdout window
- Safety stock and reorder point calculated at a 95% service level
- Stockout simulation comparing inventory policy with vs. without safety stock
- Optimal warehouse-to-region distribution plan minimizing shipping cost (PuLP)

## Video
If the video file exceeds GitHub's upload limits, it is hosted here instead: `<add link if applicable>`
