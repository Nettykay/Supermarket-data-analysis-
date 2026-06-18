# Supermarket-data-analysis-

A Data-Driven Operations Analysis of Q1 2019 Supermarket Sales


Cleaning the noise. Finding the signal. Telling the story behind every transaction.




📌 Overview

This project simulates the role of Lead Data Analyst for a global supermarket chain operating across three branches — Alexandria, Cairo, and Giza. Starting from a raw, messy extract of ~1,000 transactions from Q1 2019, the goal was to turn noisy data into actionable business intelligence in a single, end-to-end analytical workflow.

The analysis moves through five stages — data cleaning → descriptive statistics → visual dashboarding → probability modeling → hypothesis formulation — entirely in Microsoft Excel. Every figure computed answers a real business question; every chart tells management something it actually needs to know.

Completed as the capstone for an Excel for Data Analysis course.


📂 *Repository Structure*

FileDescriptionREADME.mdProject documentation (this file)SuperMarket Analysis.csvRaw, uncleaned transaction extract (~1,000 rows)CLEAN_DATA_PROJECT.xlsxFull Excel workbook — cleaning, stats, charts, probability models, and hypothesis tests, organized across five sheets (see below)

*Workbook sheet map:*

SheetContentsClean dataThe cleaned, analysis-ready dataset (single source of truth)Stats SummaryMean, median, mode, variance, standard deviation, confidence intervalVisualsSource tables and charts: scatter, bar, pie, histogramDistributionsNormal, binomial, Poisson, exponential, and uniform probability modelsHypothesisNull/alternative hypotheses and test framing for two business questions


🗂️ *Dataset*

AttributeDetailPeriodQ1 2019 (January – March)BranchesAlexandria, Cairo, GizaTotal Rows974 (after cleaning, from ~1,000 raw)Unique Transaction Dates89Tool UsedMicrosoft Excel (Power Query + Formulas + Charts)

Key columns: Invoice ID, Branch, City, Customer Type, Gender, Product Line, Unit Price, Quantity, Tax (5%), Sales (Total), Date, Time, Payment Method, COGS, Gross Margin %, Gross Income, Customer Rating.


🔧 Part 1 — *DATA CLEANING* (Power Query)

The raw extract arrived with several structural issues that would have corrupted any downstream analysis:


Split columns: A merged City_CustType field was separated into distinct City and Customer Type columns.
Text standardization: Inconsistent capitalization in Product Line was normalized with a Capitalize Each Word transform.
Null handling: Rows with a blank Rating were filtered out, since they couldn't contribute to satisfaction analysis.
Data types: Unit Price and Sales were cast to Currency; Quantity was cast to Whole Number.


The result was loaded into a dedicated Clean data sheet — the single source of truth for everything downstream.


📊 Part 2 — *BASELINE METRICS AND STATISTICAL SUMMARY*

MetricValueMean Total Bill$322.26Median Total Bill$253.39Standard Deviation (Total Bill)~$245.65Standard Deviation (Rating)~1.72Margin of Error (95% CI, n = 60)±$61.04 (Z = 1.96)

🔍 *Observation — Skewness in Sales Revenue*

<img width="521" height="165" alt="image" src="https://github.com/user-attachments/assets/f18910ad-09bb-4398-833d-a544aad2ab20" />


The mean ($322.26) sits well above the median ($253.39) — a gap of $68.87, the classic fingerprint of a right-skewed distribution: a small number of large purchases pull the mean upward while most transactions cluster lower.

Implication: The median is the more reliable measure of a typical transaction. Management shouldn't anchor operational expectations to the mean.


📈 Part 3 — *VISUAL DASHBOARD*

Scatter Plot — Total Bill vs. Quantity

<img width="509" height="314" alt="image" src="https://github.com/user-attachments/assets/2b5f28c8-ce3b-4d65-b914-eaacf4d3d9ed" />


A positive linear relationship exists between quantity and total bill (R² = 0.4957) — roughly 49.6% of the variation in total bill is explained by quantity alone. A moderate, meaningful correlation.

Bar Chart — Revenue by Branch

<img width="602" height="355" alt="image" src="https://github.com/user-attachments/assets/e7c953ae-533e-4676-8331-5287c35d3787" />


BranchTotal RevenueAlexandria$103,013Cairo$102,875Giza$107,993

All three branches land in a tight revenue band; Giza leads by a slim but consistent margin.

Pie Chart — Payment Method Breakdown

<img width="543" height="348" alt="image" src="https://github.com/user-attachments/assets/7834f2bd-046d-4a5b-9486-c9c4a5ed5d31" />


MethodShareEwallet35%Cash34%Credit Card31%

Near-parity across all three channels signals a diverse, digitally-engaged customer base — and room for targeted payment promotions.

Histogram — Distribution of Customer Ratings

<img width="558" height="427" alt="image" src="https://github.com/user-attachments/assets/93e4d24f-06da-4850-b55e-b04407857f29" />


Ratings (scale 4–10) are spread fairly uniformly across the range, with a slight bump at the low end and a modest dip at the very top. No strong concentration of top scores — satisfaction is consistent but unremarkable.

🔍 Observation — Ewallet Promotion Strategy


Giza is the strongest candidate for an Ewallet promotion. It posts the highest total revenue ($107,993), the widest Ewallet transaction spread, and an estimated Ewallet revenue of ~$37,797 (35% × $107,993) — the highest of any branch. A focused promotion here reinforces existing high-value Ewallet behavior for the greatest revenue impact per marketing dollar.


🎲 Part 4 — *PROBABILITY MODELING*

Normal Distribution — Sales Revenue

Using Mean = $322.26 and SD = $245.66:

ScenarioProbabilityCustomer spends ≤ $50076.53%Customer spends ≥ $8002.59%

Over three-quarters of customers spend under $500, while purchases above $800 are statistically rare (≈1 in 39). The data favors a volume-over-premium strategy: stock for smaller, frequent baskets rather than high-ticket inventory that sits on shelves.

Binomial Distribution — Credit Card Usage (p = 0.31)

ScenarioProbabilityExactly 20 of 50 customers pay by credit card4.63%Exactly 0 of 10 customers pay by credit card2.45%

Both outcomes are statistical edge cases — credit card usage is consistent but never dominant, so staffing or POS terminals shouldn't be planned exclusively around it.

Poisson, Exponential & Uniform Distributions


Poisson (Daily Foot Traffic): Average ≈ 11 transactions/day (λ ≈ 10.94). Extreme volumes (e.g., 85 or 120/day) carry essentially zero probability — staff for a typical 10–15 transaction day, not for outliers.
Exponential (Equipment Failure): With incidents (e.g., printer jams) averaging every 45 minutes, the probability of one occurring within 20 minutes is ~36%, and ~26% chance of going over 60 minutes without one — useful for setting preventive maintenance windows.
Uniform (Voucher Draw): Each of 300 receipts has an equal 1/300 (0.33%) chance of winning — no receipt number carries an edge.



🧪 Part 5 — *HYPOTHESIS FORMULATION*

Test 1 — Member vs. Normal Customer Spend


H₀: Average spend of Member customers = average spend of Normal customers.
H₁: Average spend of Member customers > average spend of Normal customers.
Type: One-tailed (directional) — marketing suspects Members spend more, not just differently.


Test 2 — Customer Rating by Gender


H₀: Average rating for Male shoppers = average rating for Female shoppers.
H₁: There is a difference in average rating between Male and Female shoppers.
Type: Two-tailed (non-directional) — no assumption is made about the direction of any difference.



🛠️ Tools & Techniques

CategoryTool / MethodData CleaningExcel Power QueryDescriptive StatisticsAVERAGE, MEDIAN, MODE, STDEV.S, VAR.SVisualizationsExcel Charts (Scatter, Bar, Pie, Histogram)Probability ModelingNORM.DIST, BINOM.DIST, POISSON.DIST, EXPON.DISTHypothesis FramingOne-tailed and two-tailed test structure


▶️ How to Use This Project


Download CLEAN_DATA_PROJECT.xlsx and open it in Excel (Power Query features require the desktop app).
Start with the Clean data sheet — it's the single source of truth feeding every other tab.
Walk through Stats Summary → Visuals → Distributions → Hypothesis to follow the analysis in order.
To explore with new data: refresh the Power Query connection on the Clean data sheet, and all downstream formulas and charts will recalculate automatically.



📚 Data Source & Acknowledgments

The base transaction data is adapted from the publicly available Supermarket Sales dataset (Kaggle), with branch and city labels recontextualized to Alexandria, Cairo, and Giza for this exercise.

This project was completed as part of an Excel for Data Analysis course capstone, applying statistical and analytical techniques to a real-world retail operations scenario.
