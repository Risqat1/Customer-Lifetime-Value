# Customer Lifetime Value Analysis Dashboard

### TABLE OF CONTENT

- [PROJECT OVERVIEW](#CustomerLifetimeValue Analysis-overview)
- DATA SOURCE
- TOOLS
- OBJECTIVES
- METHODOLOGY (Step-Step)
- DATA ANALYSIS
- DASHBOARD
- OBSERVATIONS
- RECOMMENDATIONS

### Customer Lifetime Value Analysis OVERVIEW
This project analyzes Customer Lifetime Value (CLV) across user cohorts to measure long-term engagement and spending patterns. Using cohort-based ARPU (Average Revenue Per User), the analysis tracks cumulative growth over 12 weeks and forecasts future performance. By comparing early, mid, and late cohorts, the study highlights retention, churn, and value creation trends that can guide product, marketing, and growth strategies.

The analysis was performed using SQL for data extraction and Power BI for visualization. This project demonstrates the ability to transform raw data into actionable insights that support decision-making and revenue optimization.


### DATA SOURCE
The dataset was gotten as a project during my internship.

### TOOLS
  The tools used for this project are;
- SQL
- Microsoft Power BI

### PROJECT OBJECTIVES
- Objectives: The primary goal is to calculate and visualize weekly retention rates for user cohorts, identify trends in user engagement and churn and communicate insights in a visual  format that supports data-driven decision-making.
- Track Real-World Customer Behavior: By grouping users by their registration week (cohort), we could monitor revenue generation over the first 12 weeks, revealing patterns in retention and churn.
- Measure ClV by Cohort: This analysis includes all visitors, providing a holistic view of average revenue per user (ARPU). Calculate average revenue generated per user over their lifecycle (up to 12 weeks after signup).
- Track Value Growth: Visualize cumulative ARPU growth per cohort to identify patterns in user spending and engagement.
- Enable Business Decisions: Provide Actionable insights to help teams design better acquisition, retention and monetization strategies.


### Step-by-Step Process: From Data Extraction to Insights.
Step 1: Defining  Registration Cohorts
Process: I extracted each unique user's (user_pseudo_id) first event week as their "registration cohort." This involved querying the dataset to find the minimum event_date per user, formatting it as YYYY-MM-DD (e.g., "2020-11-01"), and aggregating users into weekly groups. Cohort sizes ranged from 16,232 (November 8, 2020) to 28,069 (December 6, 2020).

Step 2: Extracting Weekly Revenue per user
Process: I aggregated purchase revenue for each user on a weekly basis, making sure to normalize the week numbers so they aligned with the cohort offsets (Week 0 = the registration week) and then filtered the dataset to keep only purchase events (revenue > 0), ensuring that the ARPU calculation reflects actual spending behavior rather than just user activity.

Step 3: Joining Tables and Calculating ARPU
Process: i joined the cohort and revenue tables on user_pseudo_id. For each cohort and week (0-12), i computed ARPU as total revenue divided by cohort size . E.g. November 1, 2020 cohort (size:20,078) had a week 0 ARPU of $0.94, dropping to $0.02 by week 12.


Step 4: Building the Weekly Cohort CLV Table
- Process: i unpivoted the data into a table with cohorts as rows and weeks as columns, displaying weekly ARPU. I added a "Cohort Average" row for overall means. Visualizing this in a heatmap(Green for high ARPU, Red for low ARPU) shows that early cohorts at $1.65(Nov 22,2020, week 0).
- Observation: This shows how much average revenue per user is generated each week after acquisition from Nov 2020 to Jan 2021.
Highest ARPU is in Week 0–1 (onboarding/first purchase stage).
- Insight:
After Week 1, ARPU drops sharply across all cohorts. By Week 7–12, most cohorts contribute almost no additional revenue.
This means customers spend heavily at the start, but engagement and spending fade quickly .
N.B: This chart shows that most user spending happens in the first 1-3 weeks.
  
<img width="1276" height="735" alt="Screenshot 2025-09-23 200851" src="https://github.com/user-attachments/assets/b945c91a-b4e1-430b-a27e-d3b3595feff9" />

Step 5: Creating the cumulative ARPU Table
- Process: I converted weekly ARPU into cumulative ARPU by calculating a running total across week.(e.g. Nov 1 cohort reached $2.37 by week 12)
- Observations:This chart tracks how much revenue each user group (cohort) generates over 12 weeks, starting from when they first joined.
  early cohorts (Nov 2020) show the strongest growth. 
 - For example, the Nov 1 cohort starts at $0.94 and grows steadily to $2.37 by Week 12. This means users from these early groups were highly engaged and kept spending over time.
-  Mid cohorts (Dec 2020) grew at first but no further growth afterward. For example, the Dec 6 cohort rises from $1.20 to only $1.72, then stops growing after Week 7. 
- Late cohorts (Jan 2021) show the weakest performance. For example, the Jan 1 cohort starts  low ($0.23) and increase($0.23→ $0.39) from week 0 to week 3 and the remaining weeks was blank because this cohorts are new and haven’t reached later weeks.

<img width="1271" height="724" alt="Screenshot 2025-09-23 201052" src="https://github.com/user-attachments/assets/950fa47d-88f2-4e41-9492-87dbaa688b9a" />

Step 6: Creating the cumulative growth table 
- Process: I added a Cumulative Growth%, showing week-over-week percentage increases and visualized it as a heatmap fading from green(growth) to red(stagnation) and  Cumulative Baseline Growth shows how much a cohort grows in total from the start (Week 0 = 0). It resets the baseline so you can see the full growth path. For example, the Nov 1 cohort rose from 34.8% in Week 1 to 153.2% by Week 12.

- Observations:Weekly Growth shows that early cohorts (Nov 2020) from 34.8 in week 1 and by week 12 0.8 showing the cumulative growth became weaker over the weeks and baseline Growth shows the total outcome: By Week 12, the Nov 1 cohort had grown from 34.8% in Week 1 to 153.2%, showing strong sustained growth.
Mid-December cohorts (e.g., Dec 6) slowed much earlier, peaking around 43% by Week 7.
Newer cohorts (Jan 2021) look shorter only because they haven’t had enough weeks to accumulate yet so just Week 1.


<img width="1259" height="713" alt="Screenshot 2025-09-23 201748" src="https://github.com/user-attachments/assets/77d92a6f-6ce0-40eb-acda-51ff6643fd17" />
<img width="1253" height="713" alt="Screenshot 2025-09-23 202122" src="https://github.com/user-attachments/assets/c9d473fe-a20d-4764-a360-3f18a4cdf4f3" />

### Dashboard 
<img width="1262" height="754" alt="Screenshot 2025-09-23 200743" src="https://github.com/user-attachments/assets/72bf4771-00dd-41ac-8c49-1d382641ea57" />

### Recommendations
- Strengthen Onboarding (Week 0–1):Since the biggest drop happens right after signup, focus on improving the first-week user experience.

- Target Post-Week 2 Churn: Many cohorts drop sharply after Week 3 the average revenue per user dropped by week 4. Introduce retention campaigns (email nudges, loyalty points, referral rewards) around this time to keep users engaged.

- Leverage High-Performing Cohorts: Some cohorts (e.g., holiday or promotional signups) show stronger retention. Study what worked (timing, offers, channels) and replicate those strategies in weaker periods.

- Monitor Cohort Trends Continuously: Cohort retention should be tracked monthly. Continuous monitoring allows the business to catch declines early and test new strategies in real time.




