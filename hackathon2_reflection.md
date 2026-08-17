# Hackathon #2 Reflection

**Team member:** Finley Maranga

## How did your team divide the work?

_[Fill in with your actual team setup — suggested structure below]_

We split the project along the three pillars of the challenge: **Forecasting**, **Optimization**, and **Presentation**. One or two members focused on data preparation and the Prophet forecasting model — cleaning the historical demand data, engineering the external regressors (promotions/holidays), and tuning the model until MAPE was at an acceptable level. Another member(s) took ownership of the inventory optimization layer — calculating safety stock and reorder points from the forecast's error distribution, and building the stockout simulation to compare policies. The remaining member(s) led the linear programming formulation (the distribution problem in PuLP) and consolidated everyone's results into the final slide deck and management-style narrative, making sure the technical output was translated into a business story a non-technical audience could follow.

## What was the biggest analytical hurdle?

_[Fill in specifics — example below]_

The biggest hurdle was translating forecast *uncertainty* into a defensible safety stock number rather than picking an arbitrary buffer. It required going back to the holdout evaluation, pulling the actual residual standard deviation, and connecting that statistically to the target service level (Z-score) and lead time — rather than just eyeballing a "safe-looking" number. Getting the team aligned on why this approach was more rigorous than a flat percentage buffer took some discussion.

## How did you ensure your final recommendation was actionable?

_[Fill in specifics — example below]_

We anchored every recommendation to a number a manager could act on immediately: a specific reorder point (in units), a specific safety stock level, and a specific shipping allocation with its total cost. We also stress-tested the "why" behind each number — e.g., being ready to explain *why* the safety stock level was necessary (tied to service level and stockout cost) rather than presenting it as a black-box output — so the recommendation could survive pushback in a live Q&A, not just look good on a slide.

---
*Word count target: ~200 words. Edit the bracketed sections above with your team's actual details before submitting.*
