# 📦 Case Study: Supply Chain Efficiency Analysis

## Background
A global logistics provider (DataCo) is struggling with "Hidden Late Deliveries"—orders that appear on time in the system but arrive late to the customer.

## The Solution: Tiered Analytics

### Phase 1: Operational Monitoring (The "Now")
Using `[On-Time Delivery %]` and `[Late Deliveries Count]`, we created a real-time alerting system.
- **Threshold:** Any region dropping below 85% OTD triggers an automated email via Power Automate.

### Phase 2: Strategic Comparison (The "Trend")
Using `[Sales YoY Growth %]` combined with `[Average Delivery Delay]`.
- **Finding:** We discovered that as sales grew by 20% in the EMEA region, the delivery delay also increased by 1.5 days.
- **Action:** This justified the hiring of two additional regional carriers to handle the surge.

### Phase 3: Financial Impact (The "So What?")
We utilized `[Profit Margin %]` and filtered it by `Fact_Orders[is_late]`.
- **Insight:** Late deliveries resulted in a 12% lower profit margin due to customer compensation and "Express Shipping" costs to rectify errors.
