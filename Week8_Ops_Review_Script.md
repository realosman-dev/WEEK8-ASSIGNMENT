# Week 8 Ops Review — Speaker Script
### For recording `Week8_Ops_Review_[YourName].mp4` — target runtime ~15 minutes

Pace note: read at a natural, unhurried pace (~130 wpm). Each slide's timing is a guide, not a stopwatch requirement — if you're comfortable with the material, let it breathe. Total script below runs ~14–15 minutes read straight through.

---

## Slide 1 — Title / BLUF (~60 sec)

> Good morning / afternoon, everyone. Thank you for the time. I'm going to keep this tight and lead with the headline, then back it up.
>
> Bottom line up front: operations are in a healthy, improving position. We had zero lost-time safety incidents this quarter and equipment uptime is trending in the right direction — I'll show those numbers in a moment. On the supply chain side, we now have a demand forecasting model accurate to within 4.4% of actual demand, and using that model's error distribution, we've redesigned our inventory buffer so that our expected stock-out rate drops from roughly 1-in-2 replenishment cycles to about 1-in-20 — right at our 95% service-level target.
>
> What I'm asking for today is approval to move this from a pilot analysis into standard operating policy, plus sign-off on a lowest-cost distribution routing model we've validated. Let me walk through the details.

## Slide 2 — Quarter at a Glance (~60 sec)

> Here's the scorecard for the quarter. [If you've swapped in real Week 6/7 numbers, this note doesn't apply — otherwise:] A quick flag: the Safety and Equipment Uptime figures on this slide are illustrative placeholders — swap those in for your real Week 6 and Week 7 results before you present live; everything on the forecasting and inventory side is real output from this week's analysis.
>
> Walking across: zero lost-time incidents, uptime improving to 94.2%. On forecasting, our model is accurate to 4.4% MAPE on a 45-day holdout — that's tight enough to trust for inventory decisions. And the headline number: modeled stock-out rate goes from about 49% of replenishment cycles down to about 5% once we apply a properly-sized safety stock buffer.
>
> The "why it matters" side is really the pitch for the rest of this deck: fewer stock-outs protect revenue, a right-sized buffer protects working capital — we're not just piling on inventory — and the distribution optimization directly reduces freight spend.

## Slide 3 — Safety Recap (~45 sec)

> Quick recap of safety, since it's the foundation everything else sits on. Recordable incidents trended down across the quarter to zero last month. Our Total Recordable Incident Rate is at 0.8, below the 1.2 industry benchmark we track against. Every incident from earlier in the quarter has a closed-out root-cause corrective action.
>
> One open item I want to flag proactively: we still need to finish pedestrian-forklift zone striping at DC2 — that's on the punch list and I'll cover it as a resourcing ask if needed.

## Slide 4 — Equipment Health Recap (~45 sec)

> On equipment, the trend line speaks for itself — fleet uptime has climbed steadily to 94.2%, driven by preventive maintenance compliance now at 96% and unplanned downtime down about 30% versus last quarter. We have two aging conveyor units flagged for FY capital planning rather than continued reactive repair.
>
> I'm including this because it's directly relevant to what's next: the safety-stock and reorder-point math I'm about to show assumes a reasonably reliable lead time. If equipment or fulfillment reliability were degrading, we'd need a bigger buffer — the fact that it's improving is part of why we can be disciplined about not over-stocking.

## Slide 5 — Demand Forecast (~90 sec)

> Now into the Week 8 work itself. We built a Prophet forecasting model — that's a time-series model that decomposes demand into trend, weekly and yearly seasonality, holiday effects, and here, a promotion regressor we added ourselves.
>
> We didn't just fit it and trust it — we held out the most recent 45 days, trained only on data before that, and checked how well the model predicted demand it had never seen. The result: 4.4% mean absolute percentage error, and an RMSE of about 40 units against average daily demand of roughly 660 units. That's a tight enough error band to base inventory decisions on.
>
> The external factor point is worth dwelling on for a second: holiday weeks alone shift demand by up to 130 units a day, and planned promotions lift demand 25 to 45%. Feeding the promotion calendar into the model as a regressor means we're not caught flat-footed by demand we actually knew was coming.

## Slide 6 — Inventory Policy (~90 sec)

> This is the core inventory-optimization result. We ran 2,000 simulated replenishment cycles using the lead-time demand distribution calibrated from our actual forecast error. Without a safety stock buffer, we'd stock out in about 49% of cycles — essentially a coin flip, because the reorder point only covers average demand, and real demand is sometimes above average. Add a safety stock of 163 units on top of that reorder point, and the stock-out rate drops to about 4.5%, which lines up almost exactly with our 95% target service level.
>
> Here are the assumptions behind that number, stated explicitly: 95% service level, a 7-day lead time we're treating as fixed, and a demand variability figure we deliberately pulled from the forecast's actual error — not a generic historical standard deviation — because that's the number that reflects the real uncertainty we have to plan around.

## Slide 7 — Distribution Optimization (~75 sec)

> Last piece of the analytics: once we know forecasted regional demand, how do we ship it most cheaply? We modeled two distribution centers feeding four regions, each DC-to-region lane with its own freight cost and each DC with a capacity ceiling, and solved it as a linear program.
>
> The chart shows the optimal routing — the solver naturally serves each region from whichever DC is cheaper to reach it, and only splits a region's demand across both DCs when the cheaper option runs out of capacity, exactly the behavior a human planner would want, but faster and provably optimal. For this demand snapshot, minimum total shipping cost comes out to $879. The real value here isn't the one number — it's that this is a model we can re-run every single day against the latest forecast and promotion calendar, turning it into a standing planning tool rather than a one-time study.

## Slide 8 — Strategic Recommendations (~90 sec)

> Three concrete asks, each with a rough ROI so we're not just presenting analysis for its own sake.
>
> One: formalize the safety-stock policy we just walked through. It's already calculated, already validated by simulation — this is a decision to adopt it, not a research request. Two: take the distribution optimization model out of this notebook and into a scheduled daily job. Three: extend the same forecasting approach to our top 20 SKUs by revenue, since right now we've proven the method on one item.
>
> I want to be upfront that the ROI figures here are estimates built on reasonable assumptions — unit margin, current freight spend — and I'm happy to have finance validate them line by line before we lock a business case. But directionally, all three are low-cost-to-implement since the modeling work is already done; what we need is the operational green light.

## Q&A Segment (~90 sec–2 min)

**Anticipated CFO question:** *"Why do we need to carry so much safety stock? Isn't that just cash sitting on a shelf?"*

> That's exactly the right question to ask, and I'd push back gently on the framing: this isn't a round-number cushion, it's the minimum buffer the math requires at a 95% service level, sized directly from how much our forecast is actually off by. The alternative isn't zero safety stock at zero cost — it's roughly a coin-flip chance of stocking out every replenishment cycle, and a stock-out costs us lost sales and expedited freight, which is a more expensive way to fail than holding 163 units.
>
> What I'd also point out is that we deliberately avoided a generic "three weeks of cover" rule, because that over-buffers predictable items and under-buffers volatile ones — this number is specific to this SKU's real variability. And if the committee wants to trade some risk for lower carrying cost, we can absolutely dial the target down from 95% to, say, 90% — that roughly halves the buffer — and I can bring that sensitivity analysis back next cycle.

*Delivery tip: pause briefly after "that's exactly the right question to ask" — don't rush the answer, it should sound prepared, not defensive.*

## Closing (~20 sec)

> That's the review. To summarize the ask: approve the safety-stock policy, approve moving distribution optimization into a daily process, and green-light expanding the forecasting work to more SKUs. Happy to take any other questions.

---

### Recording notes
- **This script is timed for the video itself — it does not replace the deck.** Present alongside `Week8_Ops_Review_Slides.pptx` (or the exported PDF), advancing slides as you go.
- Each slide's full script is also embedded as **speaker notes** inside the PPTX file — open Presenter View in PowerPoint/Keynote to read from notes while recording, rather than juggling this document separately.
- Suggested recording tools: PowerPoint/Keynote's built-in "Record Slide Show," Zoom/Google Meet "record yourself presenting," Loom, or OBS Studio screen-record. Export/save as `.mp4` and name it exactly `Week8_Ops_Review_[YourName].mp4` per the assignment.
