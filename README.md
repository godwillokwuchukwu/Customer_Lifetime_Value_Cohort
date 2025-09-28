# Unlocking Customer Lifetime Value: A Cohort Analysis for MyOnlineShop

As a data analyst intern at MyOnlineShop during the Team Ace Internship Program, I had the opportunity to dive deep into one of the most critical metrics in e-commerce: Customer Lifetime Value (CLV). In Week 9 of the program, I led a project to refine our CLV calculations using a weekly cohort analysis. This approach not only provided a more accurate estimate of customer value but also uncovered actionable insights into retention, seasonality, and revenue trends. In this article, I'll walk you through the project step by step, highlighting the objectives, methodology, key findings, and long-term recommendations. This work demonstrates my expertise in data storytelling, cohort analysis, and translating complex data into strategic business recommendations skills I'm eager to bring to my next role in data analytics.

## Project Objectives

The primary goal was to enhance MyOnlineShop's understanding of CLV beyond simplistic formulas, such as Shopify's basic model, which often overlooks non-purchasing visitors and assumes indefinite customer engagement. Our manager emphasized the need for a granular, cohort-based approach to:

1. **Track Real-World Customer Behavior**: By grouping users by their registration week (cohort), we could monitor revenue generation over the first 12 weeks, revealing patterns in retention and churn.
2. **Incorporate All Users**: Unlike traditional models that focus only on buyers, this analysis included all visitors, providing a holistic view of average revenue per user (ARPU).
3. **Forecast Future Value**: Using historical trends, we projected CLV for newer cohorts to inform budgeting and strategy.
4. **Identify Opportunities for Growth**: Uncover seasonality, external influences (e.g., COVID-19 impacts), and retention risks to guide marketing and product decisions.

These objectives were crucial because CLV isn't just a number—it's a foundation for sustainable growth. A accurate CLV helps determine customer acquisition costs (CAC), optimize retention strategies, and ensure profitability. For MyOnlineShop, an e-commerce platform navigating post-pandemic shifts, this meant aligning resources with high-value customer segments to drive long-term revenue.

## Step-by-Step Process: From Data Extraction to Insights

I approached this project methodically, using SQL for data querying, Power BI for analysis and visualization, and cohort modeling techniques. The data spanned user events from November 2020 to January 2021. Here's how I executed each step, along with its importance.

### Step 1: Defining Registration Cohorts
- **Process**: I extracted each unique user's (`user_pseudo_id`) first event week as their "registration cohort." This involved querying the dataset to find the minimum `event_date` per user, formatting it as YYYY-MM-DD (e.g., "2020-11-01"), and aggregating users into weekly groups. Cohort sizes ranged from 16,232 (November 8, 2020) to 28,069 (December 6, 2020).

- **Importance**: Cohorts allow for apples-to-apples comparisons by isolating groups based on acquisition timing. This step is foundational because it accounts for external factors like holidays or pandemics, which could skew aggregate metrics. Without it, we'd miss nuances like how November cohorts benefited from Black Friday surges.

### Step 2: Extracting Weekly Revenue Data
- **Process**: I pulled weekly purchase data, aligning dates with cohorts. For each user, I calculated revenue per week post-registration (Week 0 being the registration week). This created a revenue table linked by `user_pseudo_id` and week offsets.

- **Importance**: Revenue isn't static; it fluctuates weekly due to user engagement. This granular extraction ensures we capture initial spikes (e.g., Week 0 purchases) and subsequent drops, providing a realistic view of value accrual. It's essential for e-commerce, where impulse buys can inflate short-term metrics but mask long-term churn.

### Step 3: Joining Tables and Calculating ARPU
- **Process**: I joined the cohort and revenue tables on `user_pseudo_id`. For each cohort and week (0–12), I computed ARPU as total revenue divided by cohort size. For example, the November 1, 2020 cohort (size: 20,078) had a Week 0 ARPU of $0.94, dropping to $0.02 by Week 12.

- **Importance**: ARPU democratizes CLV by including non-buyers, reflecting the true average value per visitor. This join step bridges acquisition and monetization data, highlighting inefficiencies like high acquisition costs for low-revenue cohorts.

### Step 4: Building the Weekly Cohort CLV Table
- **Process**: I pivoted the data into a table with cohorts as rows and weeks as columns, displaying weekly ARPU. I added a "Cohort Average" row for overall means. Visualizing this in a heatmap (greens for high ARPU, reds for low) revealed patterns, such as early cohorts peaking at $1.65 (November 22, 2020, Week 0) due to holiday shopping.

- **Importance**: This table exposes week-to-week volatility, like a 30-50% drop-off in momentum post-holidays. It's vital for spotting retention cliffs (e.g., Weeks 4–6), enabling targeted interventions like email campaigns.

### Step 5: Creating the Cumulative Cohort CLV Table
- **Process**: I calculated cumulative ARPU by summing weekly values (e.g., November 1 cohort reached $2.37 by Week 12). I added a "Cumulative Growth %" row, showing week-over-week percentage increases, and visualized it as a heatmap fading from green (growth) to red (stagnation).

- **Importance**: Cumulative views shift focus from snapshots to lifetime trajectories, revealing that 70–90% of value accrues in the first 6 weeks. This informs lifespan assumptions in predictive models and underscores the need for early engagement to combat churn.

### Step 6: Forecasting Future CLV for Incomplete Cohorts
- **Process**: For newer cohorts (e.g., January 24, 2021, with only Week 0 data at $0.19), I applied average cumulative growth rates from older cohorts. Starting from Week 0, I projected forward: Week 1 = $0.19 × (1 + 13.5%) ≈ $0.22, continuing to Week 12. This yielded a forecast table and line chart showing expected trajectories.

- **Importance**: Forecasting bridges data gaps, allowing proactive planning. In uncertain markets, this predictive element turns historical data into forward-looking strategy, estimating a 12-week CLV of ~$17.69 across cohorts.

### Step 7: Estimating Overall CLV and Visualizing Trends
- **Process**: Averaging cumulative ARPU across cohorts gave a 12-week CLV of $17.69, with total revenue at $362,165 from 267,942 customers. I created charts: a declining line for weighted average growth % (from 300% in November 2020 to 19% by January 2021) and heatmaps for cohorts.

- **Importance**: This final estimate integrates all steps, providing a benchmark for CAC (aim for 3:1 ratio). Visuals make data accessible, turning numbers into stories for stakeholders.

## Key Findings and Insights

The analysis revealed a weighted average cumulative ARPU trend declining from 300% growth in late 2020 to near-zero by early 2021, influenced by COVID-19 surges, holiday peaks, and post-holiday churn. Early cohorts (November 2020) showed robust initial ARPU ($0.94–$1.65) fueled by lockdowns and promotions, but value halved within 6 weeks. Newer cohorts (January 2021) started lower ($0.19–$0.90) but projected steady growth.

Insights:
- **Seasonality Drives Value**: Holiday cohorts captured 80% of value in Weeks 0–5, but non-seasonal ones declined faster, signaling dependency on external events.
- **Retention Risks**: 70–90% drop-off post-Week 6 highlights fragility; early engagement (e.g., Weeks 1–3) is key to extending lifespan.
- **Pandemic Impact**: COVID-19 boosted mid-2020 usage but led to saturation, with ARPU falling 43.3% by December 6.
- **Overall Metrics**: Average baseline growth was 175.5%, but cumulative ARPU plateaued at $17.69, suggesting room for upselling.

## Recommendations for Long-Term Improvement (2–10 Years)

To elevate MyOnlineShop from a transactional platform to a loyalty-driven powerhouse, I recommend the following, phased over 2–10 years:

- **Short-Term (2–3 Years)**: Implement personalized retention tactics, like AI-driven recommendations in Weeks 1–3, to lift ARPU by 20–30%. Integrate loyalty programs (e.g., points for repeat visits) to counter post-holiday churn, targeting a 4:1 CLV:CAC ratio.
  
- **Medium-Term (4–6 Years)**: Diversify beyond seasonality by expanding product lines (e.g., subscriptions) and markets. Use predictive CLV models with machine learning (e.g., via PyTorch) to forecast churn, reducing it by 15–20%. Invest in omnichannel experiences to capture value from non-buyers, potentially increasing cumulative ARPU to $25+.

- **Long-Term (7–10 Years)**: Build a data ecosystem for real-time CLV tracking, incorporating external data (e.g., economic indicators). Foster community features (e.g., user forums) to extend lifespans to 24+ weeks, aiming for $50+ CLV. Sustainability initiatives, like eco-friendly products, could attract high-value segments, ensuring resilience against market shifts.

These strategies could double revenue streams by addressing churn and enhancing engagement, positioning MyOnlineShop as an industry leader.

## Conclusion

This CLV project showcased the power of cohort analysis in transforming raw data into strategic insights. By meticulously building tables, forecasts, and visuals, I not only estimated a realistic CLV but also provided a roadmap for growth. This experience honed my skills in data manipulation, visualization, and storytelling—core to my career aspirations in data analytics. If you're hiring for roles involving customer analytics or business intelligence, I'd love to connect on LinkedIn to discuss how I can contribute to your team.

*Note: All visuals and data referenced are based on anonymized MyOnlineShop datasets. For full portfolio details, reach out via LinkedIn.*
