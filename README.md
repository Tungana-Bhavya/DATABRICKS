
# Foodie-Fi Customer & Revenue Analytics Dashboard with AIBI Genie & Databricks

<p align = "center"><img src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/PROJECT_LOGO.png" alt="Image"></p>

### *** Project Title ***

Foodie-Fi Customer & Revenue Analytics Dashboard with AIBI Genie & Databricks

----------------

### *** Project Description ***</br>
<p>This project, which is a part of the 8-Week SQL Challenge, is an in-depth analysis of subscription trends and purchasing habits for the Foodie-Fi SQL Case Study. The project investigates important customer and revenue metrics obtained from the plans and subscriptions datasets using Databricks and AIBI Genie, a BI assistant powered by natural language.</p>

<p>An AI-powered multi-page dashboard was created to visualize insights using charts, tables, and KPI cards. Understanding customer upgrade/downgrade behavior, revenue growth, and churn are just a few of the strategic business decisions that the analysis supports.</p>

----------------


### *** Tools/Technologies Used ***</br>
- Databricks SQL: a unified platform for creating and running SQL queries</br>
- AIBI Genie (within Databricks)—for AI-powered, natural language-based data exploration and dashboard creation</br>
- SQL is used to determine KPIs such as customer growth, MRR, ARPU, and churn rate.</br>
- Databricks AIBI Dashboards: to create interactive multi-page dashboards with charts, KPIs.</br>

----------------

### *** key Features ***</br>
 #### Revenue KPIs:</br>
Total Revenue ($), Average Revenue Per User($), Monthly Recurring Revenue (MRR) ($), Overall Churn Rate (%), Trial Plan Churn Rate (%) and Monthly Trial Plan Signups.</br>

#### Customer KPIs:</br>
Total Customers, Pro Annual Customers, Downgraded Customers, Cummulative Customer Growth, Foodie-Fi Customer Distribution by Plan Type (%) and Foodi-Fi Subscription Plan Rates ($).</br>

#### Dashboard Features:</br>
- AIBI Multi-Page Dashboard </br>
- Responsive Charts like bar charts, area charts, line charts and pie charts.</br>
- Included custom logo with appropriate title and Footer.

----------------

### *** Description & Screenshots ***</br>
Here is a visual walkthrough of the project that includes data exploration and dashboarding driven by AI using Databricks SQL and AIBI Genie.</b>

#### A. Dataset Exploration Using AIBI Genie
NLP Queries were used to understand the structure of the data before peformaing analysis.
<h3 align ='left'>1. How many tables are there?</h3>

#### Source Code:</br>
The foodie-fi database consists of two tables i.e plans and subscriptions.
SELECT table_name FROM INFORMATION_SCHEMA.TABLES</br>
WHERE TABLE_SCHEMA = 'foodie_fi' AND TABLE_TYPE = 'BASE TABLE';

#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/1_TABLES_COUNT.jpg">
</p>

<h3 align ='left'>2. Print the Schema for Plans table?</h3>

#### Source Code:</br>
SELECT `column_name`, `data_type`FROM `information_schema`.`columns`WHERE `table_name` = 'plans' AND `table_schema` = 'foodie_fi' AND `table_catalog` = 'workspace';</br>
  
#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/2_PLANS_PRINT_SCHEMA.jpg">
</p>

<h3 align ='left'>3. Print the Schema for Subscriptions table?</h3>

#### Source Code:</br>
SELECT `column_name`, `data_type` FROM `information_schema`.`columns` WHERE `table_name` = 'subscriptions' AND `table_schema` = 'foodie_fi' AND `table_catalog` = 'workspace';

#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/3_SUBSCRIPTIONS_PRINT_SCHEMA.jpg">
</p>

<h3 align ='left'>4. List the number of rows and columns in Plans ?</h3>

#### Source Code:</br>
SELECT (</br>
    SELECT COUNT(*) FROM `workspace`.`foodie_fi`.`plans`) AS Total_rows,</br>
  (
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = 'plans' </br>
    AND table_schema = 'foodie_fi' AND table_catalog = 'workspace'</br>
) AS Total_columns</br>
    
#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/4_ROWS_AND_COLUMNS_PLANS.jpg">
</p>

<h3 align ='left'>5. List the number of rows and columns in subscriptions table ?</h3>

#### Source Code:</br>
SELECT (</br>
    SELECT COUNT(*) FROM `workspace`.`foodie_fi`.`subscriptions`) AS Total_rows,</br>
  ( SELECT COUNT(*) FROM information_schema.columns WHERE table_name = 'subscriptions'</br>
  AND table_schema = 'foodie_fi' AND table_catalog = 'workspace'</br>
) AS Total_columns</br>
    
#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/5_ROWS_AND_COLUMNS_SUBSCRIPTONS.jpg">
</p>

------------

#### B. Case Study Questions - SQL Analysis
#### 1. Customer Journey

<h3 align ='left'>1. Find the unique customers based on the given sample = [1, 2, 11, 13, 15, 16, 18, 19] from the subscriptions table including details with their plans ?</h3>

#### Source Code:</br>
SELECT
  `subscriptions`.`customer_id`,
  `subscriptions`.`plan_id`,
  `subscriptions`.`start_date`,
  `plans`.`plan_name`,
  `plans`.`price`
FROM
  `workspace`.`foodie_fi`.`subscriptions`
    JOIN `workspace`.`foodie_fi`.`plans`
      ON `subscriptions`.`plan_id` = `plans`.`plan_id`
WHERE
  `subscriptions`.`customer_id` IN (1, 2, 11, 13, 15, 16, 18, 19)
  
#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/11_UNIQUE_CUSTOMERS_BASED_ON_SAMPLE.jpg">
</p>

------------
#### 2. Data Analysis Questions

<h3 align ='left'>1. What are the different plan names available in the plans table ?</h3>

#### Source Code:</br>
SELECT DISTINCT `plan_name` FROM `workspace`.`foodie_fi`.`plans`;
    
#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/6_DIFFERENT_PLAN_NAMES_AVAILABLE.jpg">
</p>

<h3 align ='left'>2. What is the most expensive plan available in the plans table ?</h3>

#### Source Code:</br>
SELECT `plan_name`, `price` FROM `workspace`.`foodie_fi`.`plans` WHERE </br>
`price` = ( SELECT MAX(`price`) FROM `workspace`.`foodie_fi`.`plans`)    

#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/7_MOST_EXPENSIVE_PLAN.jpg">
</p>

<h3 align ='left'>3. What is the cheapest plan available in the plans table ?</h3>

#### Source Code:</br>
SELECT `plan_name`, `price` FROM `workspace`.`foodie_fi`.`plans` WHERE </br>
`price` = ( SELECT MIN(`price`) FROM `workspace`.`foodie_fi`.`plans`)

#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/8_CHEAPEST_PLAN.jpg">
</p>

<h3 align ='left'>4. What are the prices of all the plans available in the plans table ?</h3>

#### Source Code:</br>
SELECT `plan_name`, `price` FROM `workspace`.`foodie_fi`.`plans`;

#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/9_PRICES_FOR_TYPES.jpg">
</p>

<h3 align ='left'>5. How many customers has Foodie-Fi ever had ?</h3>

#### Source Code:</br>
SELECT COUNT(DISTINCT `customer_id`) AS total_customers</br>
FROM `workspace`.`foodie_fi`.`subscriptions`

#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/12_UNIQUE_CUSTOMERS_COUNT_FOODIE_FI.jpg">
</p>

<h3 align ='left'>6. What is the monthly distribution of trial plan with only start_date values for the dataset - use the start of the month as the group by value and result in descending order ?</h3>

#### Source Code:</br>
SELECT DATE_TRUNC('month', `start_date`) AS month_start, COUNT(*) AS trial_count</br>
FROM `workspace`.`foodie_fi`.`subscriptions` WHERE `plan_id` = ( SELECT `plan_id`</br>
FROM `workspace`.`foodie_fi`.`plans` WHERE `plan_name` = 'trial')</br>
GROUP BY month_start ORDER BY month_start DESC

#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/13_MONTHLY_DISTRIBUTION_TRIAL_PLAN.jpg">
</p>

<h3 align ='left'>7. What plan start_date values occur after the year 2020 for the dataset? Show the breakdown by count of events for each plan_name ? Rename count as event_count_2021 in ascending order ?</h3>

#### Source Code:</br>
SELECT `plans`.`plan_name`, COUNT(*) event_count_2021 </br>
FROM `workspace`.`foodie_fi`.`subscriptions` JOIN `workspace`.`foodie_fi`.`plans`</br>
ON `subscriptions`.`plan_id` = `plans`.`plan_id` WHERE</br>
YEAR(`subscriptions`.`start_date`) > 2020</br>
GROUP BY `plans`.`plan_name ORDER BY event_count_2021 ASC</br>

#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/14_EVENT_COUNT_2020.jpg">
</p>

<h3 align ='left'>8. What is the customer count and percentage of customers who have churned rounded to 1 decimal place ?</h3>

#### Source Code:</br>
SELECT COUNT(`customer_id`) AS churned_customers, ROUND(</br>
(</br>
try_divide(COUNT(`customer_id`) * 100.0,</br>
( SELECT COUNT(`customer_id`) FROM</br>
`workspace`.`foodie_fi`.`subscriptions`))),1) AS churned_percentage</br>
FROM `workspace`.`foodie_fi`.`subscriptions`WHERE</br>
`plan_id` = ( SELECT `plan_id` FROM `workspace`.`foodie_fi`.`plans`WHERE</br>
  `plan_name` = 'churn')</br>

#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/15_CUSTOMER_COUNT_CHURNED_PERCENTAGE.jpg">
</p>

<h3 align ='left'>9. How many customers have churned straight after their initial free trial - what percentage is this rounded to the nearest whole number ?</h3>

#### Source Code:</br>

SELECT COUNT(`customer_id`) AS churned_customers, ROUND(</br>
(</br>
try_divide(COUNT(`customer_id`) * 100.0,</br>
( SELECT COUNT(`customer_id`) FROM</br>
`workspace`.`foodie_fi`.`subscriptions`))),1) AS churned_percentage</br>
FROM `workspace`.`foodie_fi`.`subscriptions`WHERE</br>
`plan_id` = ( SELECT `plan_id` FROM `workspace`.`foodie_fi`.`plans`WHERE</br>
  `plan_name` = 'churn')</br>

#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/26_CUSTOMER_CHURNED_ANALYSIS.jpg">
</p>

<h3 align ='left'>10. What is the number and percentage of customer plans after their initial free trial ?</h3>

#### Source Code:</br>
SELECT `plans`.`plan_name`, COUNT(`subscriptions`.`customer_id`) AS customer_count,</br>
ROUND( (try_divide( COUNT(`subscriptions`.`customer_id`) * 100.0,</br>
( SELECT COUNT(`customer_id`) FROM `workspace`.`foodie_fi`.`subscriptions`</br>
WHERE `plan_id` = ( SELECT `plan_id` FROM `workspace`.`foodie_fi`.`plans`</br>
WHERE `plan_name` = 'trial')))),1) AS customer_percentage</br>
FROM `workspace`.`foodie_fi`.`subscriptions` JOIN `workspace`.`foodie_fi`.`plans`</br>
ON `subscriptions`.`plan_id` = `plans`.`plan_id` WHERE</br>
`subscriptions`.`customer_id` IN ( SELECT `customer_id` </br>
FROM `workspace`.`foodie_fi`.`subscriptions` WHERE</br>
`plan_id` = ( SELECT `plan_id` FROM `workspace`.`foodie_fi`.`plans` </br>
WHERE `plan_name` = 'trial')) AND `plans`.`plan_name` != 'trial'</br>
GROUP BY `plans`.`plan_name`</br>

#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/17_NUMBER_AND_PERCENTAGE_CUSTOMERS_AFTER_INITIAL.jpg">
</p>

<h3 align ='left'>11. What is the customer count and percentage breakdown of all 5 plan_name values ? Find the breakdown of customers with existing plans on or after 2020-12-31 ?</h3>

#### Source Code:</br>
SELECT
  `plans`.`plan_name`,
  COUNT(`subscriptions`.`customer_id`) AS customer_count,
  ROUND(
    (
      try_divide(
        COUNT(`subscriptions`.`customer_id`) * 100.0,
        (
          SELECT
            COUNT(`customer_id`)
          FROM
            `workspace`.`foodie_fi`.`subscriptions`
          WHERE
            `start_date` >= '2020-12-31'
        )
      )
    ),
    1
  ) AS customer_percentage
FROM
  `workspace`.`foodie_fi`.`subscriptions`
    JOIN `workspace`.`foodie_fi`.`plans`
      ON `subscriptions`.`plan_id` = `plans`.`plan_id`
WHERE
  `subscriptions`.`start_date` >= '2020-12-31'
GROUP BY
  `plans`.`plan_name`

#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/18_CUSTOMER_COUNT_PERCENTAGE_BREAKDOWN.jpg">
</p>

<h3 align ='left'>12. How many customers have upgraded to an annual plan in 2020 ?</h3>

#### Source Code:</br>
SELECT
  COUNT(`customer_id`) AS upgraded_customers
FROM
  `workspace`.`foodie_fi`.`subscriptions`
WHERE
  `plan_id` = (
    SELECT
      `plan_id`
    FROM
      `workspace`.`foodie_fi`.`plans`
    WHERE
      `plan_name` = 'pro annual'
  )
  AND YEAR(`start_date`) = 2020`

#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/20_UPGRADED_CUSTOMERS.jpg">
</p>

<h3 align ='left'>13. How many days on average does it take for a customer to upgrade to an annual plan from the day they join Foodie-Fi ?</h3>

#### Source Code:</br>
SELECT
  ROUND(
    AVG(DATEDIFF(`subscriptions`.`start_date`, `initial`.`start_date`)), 0
  ) AS average_days_to_upgrade
FROM
  `workspace`.`foodie_fi`.`subscriptions` AS `subscriptions`
    JOIN `workspace`.`foodie_fi`.`subscriptions` AS `initial`
      ON `subscriptions`.`customer_id` = `initial`.`customer_id`
WHERE
  `subscriptions`.`plan_id` = (
    SELECT
      `plan_id`
    FROM
      `workspace`.`foodie_fi`.`plans`
    WHERE
      `plan_name` = 'pro annual'
  )
  AND `initial`.`plan_id` = (
    SELECT
      `plan_id`
    FROM
      `workspace`.`foodie_fi`.`plans`
    WHERE
      `plan_name` = 'trial'
  )

#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/21_AVERAGE_DAYS_TO_UPGRADE.jpg">
</p>

<h3 align ='left'>14. Can you further break down this average value into 30 day periods (i.e. 0-30 days, 31-60 days etc) ? </h3>

#### Source Code:</br>
SELECT
  CASE
    WHEN
      DATEDIFF(`subscriptions`.`start_date`, `initial`.`start_date`) BETWEEN 0 AND 30
    THEN
      '0-30 days'
    WHEN
      DATEDIFF(`subscriptions`.`start_date`, `initial`.`start_date`) BETWEEN 31 AND 60
    THEN
      '31-60 days'
    WHEN
      DATEDIFF(`subscriptions`.`start_date`, `initial`.`start_date`) BETWEEN 61 AND 90
    THEN
      '61-90 days'
    ELSE '91+ days'
  END AS period,
  COUNT(*) AS customer_count
FROM
  `workspace`.`foodie_fi`.`subscriptions` AS `subscriptions`
    JOIN `workspace`.`foodie_fi`.`subscriptions` AS `initial`
      ON `subscriptions`.`customer_id` = `initial`.`customer_id`
WHERE
  `subscriptions`.`plan_id` = (
    SELECT
      `plan_id`
    FROM
      `workspace`.`foodie_fi`.`plans`
    WHERE
      `plan_name` = 'pro annual'
  )
  AND `initial`.`plan_id` = (
    SELECT
      `plan_id`
    FROM
      `workspace`.`foodie_fi`.`plans`
    WHERE
      `plan_name` = 'trial'
  )
GROUP BY
  period
ORDER BY
  period

#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/22_30_DAYS_PERIOD_AVERAGE_VALUE.jpg">
</p>

<h3 align ='left'>15. How many customers downgraded from a pro monthly to a basic monthly plan in 2020 ? </h3>

#### Source Code:</br>
WITH plan_tiers AS (
  SELECT plan_id, plan_name,
    CASE plan_name
      WHEN 'trial' THEN 1
      WHEN 'basic monthly' THEN 2
      WHEN 'pro monthly' THEN 3
      WHEN 'pro annual' THEN 4
      ELSE 0
    END AS tier_rank
  FROM workspace.foodie_fi.plans
),

customer_plans AS (
  SELECT s.customer_id, s.start_date, pt.tier_rank
  FROM workspace.foodie_fi.subscriptions s
  JOIN plan_tiers pt ON s.plan_id = pt.plan_id
),

earliest_latest AS (
  SELECT
    customer_id,
    MIN(tier_rank) AS min_tier,
    MAX(tier_rank) AS max_tier
  FROM customer_plans
  GROUP BY customer_id
)

SELECT COUNT(*) AS total_downgraded_customers
FROM earliest_latest
WHERE max_tier > min_tier
  AND max_tier = 4;

#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/23_DOWNGRADED_CUSTOMERS.jpg">
</p>

------------

#### C. Metrics Calculation
#### 1. Revenue Analysis Metrics

<h3 align ='left'>1. How to calculate average revenue per user ?</h3>

#### Source Code:</br>
SELECT ROUND(SUM(p.price) / COUNT(DISTINCT s.customer_id), 2) AS arpu </br>
FROM workspace.foodie_fi.subscriptions s</br>
JOIN workspace.foodie_fi.plans p ON s.plan_id = p.plan_id</br>

#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/28_ARPU.jpg">
</p>

<h3 align ='left'>2. How to calculate total churn rate ?</h3>

#### Source Code:</br>
SELECT ROUND(100.0 * COUNT(DISTINCT customer_id)</br>
FILTER (WHERE plan_id = 4)  / COUNT(DISTINCT customer_id), 1) AS churn_rate</br>
FROM workspace.foodie_fi.subscriptions;

#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/27_OVERALL_CHURN_RATE.jpg">
</p>

<h3 align ='left'>3. How to calculate trial churn rate ?</h3>

#### Source Code:</br>
WITH cte AS (</br>
  SELECT s.customer_id, p.plan_name, LEAD(p.plan_name) OVER (</br>
  PARTITION BY s.customer_id ORDER BY s.start_date) next_plan</br>
  FROM workspace.foodie_fi.subscriptions AS s</br>
  JOIN workspace.foodie_fi.plans p ON s.plan_id = p.plan_id</br>
)</br>
  
SELECT COUNT(customer_id) AS churned_customers,</br>
ROUND(100.0 * COUNT(customer_id) / (SELECT COUNT(DISTINCT customer_id) </br>
FROM workspace.foodie_fi.subscriptions)</br>
  ) churn_percentage </br>
FROM cte</br>
WHERE plan_name = 'trial' AND next_plan = 'churn';</br>

#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/29_TRIAL_CHURN_RATE.jpg">
</p>

<h3 align ='left'>4. How to calculate monthly trial plan signups ?</h3>

#### Source Code:</br>
-- monthly new customers
SELECT DATE_FORMAT(DATE_TRUNC('month', start_date), 'MMM-yyyy') AS month,</br>
COUNT(DISTINCT customer_id) AS new_customers </br>
FROM workspace.foodie_fi.subscriptions</br>
GROUP BY DATE_TRUNC('month', start_date)</br>
ORDER BY DATE_TRUNC('month', start_date);</br>

#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/30_MONTHLY_TRIAL_PLAN_SIGNUPS.jpg">
</p>

<h3 align ='left'>5. How to calculate Monthly Recurring Revenue ?</h3>

#### Source Code:</br>
WITH months AS (</br>
  SELECT DISTINCT DATE_TRUNC('month', start_date) AS month</br>
  FROM workspace.foodie_fi.subscriptions</br>
),</br>
month_ranges AS (</br>
  SELECT month, LAST_DAY(month) AS month_end FROM months</br>
)</br>

SELECT</br>
  DATE_FORMAT(m.month, 'yyyy-MM') AS month,</br>
  SUM(p.price) AS MRR</br>
FROM month_ranges m</br>
JOIN workspace.foodie_fi.subscriptions s</br>
  ON s.start_date <= m.month_end</br>
JOIN workspace.foodie_fi.plans p</br>
  ON s.plan_id = p.plan_id</br>
GROUP BY m.month</br>
ORDER BY m.month DESC;</br>


SELECT DATE_FORMAT(m.month, 'yyyy-MM') AS month,</br>
  SUM(p.price) AS MRR</br>
FROM month_ranges m</br>
JOIN workspace.foodie_fi.subscriptions s</br>
  ON s.start_date <= m.month_end</br>
JOIN workspace.foodie_fi.plans p</br>
  ON s.plan_id = p.plan_id</br>
GROUP BY m.month</br>
ORDER BY m.month DESC;</br>

#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/31_MRR.jpg">
</p>

#### 2. Customer Analysis Metrics
<h3 align ='left'>1. How to calculate total customers count ?</h3>

#### Source Code:</br>
SELECT COUNT(DISTINCT customer_id) AS total_customers</br>
FROM workspace.foodie_fi.subscriptions;</br>

#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/32_TOTAL_CUSTOMERS.jpg">
</p>

<h3 align ='left'>2. How to calculate pro annual subscribed customers count ?</h3>

#### Source Code:</br>
SELECT COUNT(DISTINCT customer_id) AS upgraded_annual_customers</br>
FROM foodie_fi.subscriptions WHERE plan_id = 3 AND EXTRACT(YEAR FROM start_date) = 2020;</br>

#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/33_PRO_ANNUAL_CUSTOMERS.jpg">
</p>

<h3 align ='left'>3. How to calculate total downgraded customers ?</h3>

#### Source Code:</br>
WITH plan_tiers AS (</br>
  SELECT plan_id, plan_name,</br>
    CASE plan_name</br>
      WHEN 'trial' THEN 1</br>
      WHEN 'basic monthly' THEN 2</br>
      WHEN 'pro monthly' THEN 3</br>
      WHEN 'pro annual' THEN 4</br>
      ELSE 0</br>
    END AS tier_rank</br>
  FROM workspace.foodie_fi.plans</br>
),</br>

customer_plans AS (</br>
  SELECT s.customer_id, s.start_date, pt.tier_rank</br>
  FROM workspace.foodie_fi.subscriptions s</br>
  JOIN plan_tiers pt ON s.plan_id = pt.plan_id</br>
),</br>

earliest_latest AS (</br>
  SELECT customer_id, MIN(tier_rank) AS min_tier, MAX(tier_rank) AS max_tier</br>
  FROM customer_plans GROUP BY customer_id)</br>

SELECT COUNT(*) AS total_downgraded_customers</br>
FROM earliest_latest WHERE max_tier > min_tier AND max_tier = 4;</br>

#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/23_DOWNGRADED_CUSTOMERS.jpg">
</p>

<h3 align ='left'>4. How to calculate cumulative customer growth ?</h3>

#### Source Code:</br>
WITH monthly_signups AS (</br>
  SELECT DATE_TRUNC('month', start_date) AS raw_month,</br>
  DATE_FORMAT(DATE_TRUNC('month', start_date), 'yyyy-MM') AS month,</br>
  COUNT(DISTINCT customer_id) AS new_customers</br>
  FROM workspace.foodie_fi.subscriptions</br>
  GROUP BY DATE_TRUNC('month', start_date)</br>
),</br>
cumulative_growth AS (</br>
SELECT month, SUM(new_customers) OVER (ORDER BY raw_month) AS cumulative_customers</br>
FROM monthly_signups)</br>
SELECT month, cumulative_customers FROM cumulative_growth;</br>

#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/34_CUMULATIVE_CUSTOMER_GROWTH.jpg">
</p>

<h3 align ='left'>5. How to calculate customer distribution by different plans ?</h3>

#### Source Code:</br>
SELECT p.plan_name, COUNT(s.customer_id) AS customer_count,</br>
  ROUND(COUNT(s.customer_id) * 100.0 /</br>
    (</br>
      SELECT COUNT(customer_id)</br>
      FROM workspace.foodie_fi.subscriptions</br>
      WHERE start_date >= '2020-12-31'</br>
    ),</br>
    1</br>
  ) AS customer_percentage</br>
FROM workspace.foodie_fi.subscriptions s</br>
JOIN workspace.foodie_fi.plans p</br>
  ON s.plan_id = p.plan_id</br>
WHERE s.start_date >= '2020-12-31'</br>
GROUP BY p.plan_name</br>
ORDER BY customer_count DESC;</br>

#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/24_CUSTOMER_DISTRIBUTION_PLAN_TYPE.jpg">
</p>

<h3 align ='left'>6. How to calculate customer distribution by different plans ?</h3>

#### Source Code:</br>
SELECT plan_name, price FROM workspace.foodie_fi.plans</br>
WHERE plan_name != 'churn' ORDER BY price ASC;</br>

#### Output Screens:</br>
<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/25_FOODIE_FI_SUBCRIPTION_PLAN_RATE.jpg">
</p>

------------

#### C. Databricks Monitoriing View

<p>A Databricks monitoring view gives a detailed look at user interactions and data quality over time. It combines user ratings, creation and update timestamps, and user request status. This setup helps track data quality attributes such as accuracy, consistency, and completeness. It also monitors the performance of machine learning models.</p>

<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/FOODIE_FI_DATABRICKS_MONITORING.jpg">
</p>

------------

#### D. Interactive Dashboards
####  Revenue Analytics Dashboard (Page 1)

<p>The following dashboard provides an overview of foodie-fi revenue analysis:</p>

<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/REVENUE_ANALYSIS_DASHBOARD.jpg">
</p>

#### Customer Analytics Dashboard (Page 2)

<p>The following dashboard provides an overview of foodie-fi customer analysis:</p>

<p align="left">
  <img  src="https://github.com/Tungana-Bhavya/DATABRICKS/blob/main/FILES/IMAGES/CUSTOMER_ANALYSIS_DASHBOARD.jpg">
</p>

----------------

### E. *** Key Learnings ***</br>
- Gained Practical experience using Databricks SQL workspace, Genie workspace including notebooks for efficient data analysis.</br>
- Utilized Databricks AIBI Genie feature for natural language querying.</br>
- Calculated KPI Metrics, learned when to use which type of charts.</br>
- Gained deeper understanding of subscription-based metrics like churn, ARPU, and MRR.</br>
- Developed Multi-page Dashboard using Databricks AIBI Genie feature.</br>
- Improved storytelling capabilities with dashboards and visualizations powered by AI.
- Practiced end-to-end project execution: data analysis, visualization, business insight generation, and report presentation.

