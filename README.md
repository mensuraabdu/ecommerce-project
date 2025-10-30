**E-Commerce Revenue Analysis - Google Data Analytics Capstone**
This repository contains my Google Data Analytics Capstone project, analyzing e-commerce data to identify key revenue drivers for marketing and inventory strategies, following the Ask, Prepare, Process, Analyze, Share, and Act framework.
**Project Overview**
The project analyzes a merged e-commerce dataset (~2,950 rows, 40 columns) combining Sales, Customer, and Product Details to answer specific business questions and provide actionable insights.

**Ask**
Business Problem: Identify key drivers of e-commerce revenue to optimize inventory, marketing, and sales strategies.
**Problem Questions:**
- Which products and categories generate the most revenue?
- Which customer segments (age, gender, location) contribute the most to revenue?
- Do discounts or subscription status increase purchase amounts or repeat purchases?
- How does customer age influence purchasing patterns for top categories?
- Which regions show potential for targeted marketing based on revenue distribution?

**Objective:** Provide insights to prioritize high-revenue products/categories, target key customer segments, and optimize marketing strategies.

**Prepare**
**Data Sources:**
- Sales Data: ~3,000 rows; columns: user_id, product_id, Interaction Type, Timestamp, etc.
- Customer Details: ~3,000 rows, ~18 columns; columns: customer_id, Age, Gender, Location, etc.
- Product Details: ~10,002 rows, ~24 columns; columns: unique_id, product_name, selling_price, etc.
- Process: Merged datasets into merged_data.csv and merged_data.xlsx using merge_ecommerce_datasets_excel.ipynb.
**Challenges:**
- Inconsistent column names (e.g., user_id vs. Customer ID).
- Solution: Standardized to Customer ID and Product ID using Python.

**Process**
-**Data Cleaning:**

- **Sales Data:**
- Filtered for Interaction Type = purchase (Google Sheets).
- Removed unnecessary columns (e.g., “Unnamed: 4”).
- Renamed user_id to Customer ID, product_id to Product ID.
- Handled missing values: Replaced blanks in Interaction Type with “unknown”; removed rows missing Customer ID or Product ID.
- Standardized Timestamp using TRIM(); converted to date-time.
- Removed duplicates using Data Cleanup.
- Saved as final_cleaned_interactions.csv.

**Customer Details:**
- Cleaned customer_id: Removed spaces with TRIM(); removed duplicates.
- Validated Age: Replaced missing/unrealistic values with median or “Unknown”.
- Standardized Gender: Unified to “Male”/“Female”; filled missing with “Unknown”.
- Ensured numeric purchase data using text-to-columns.
- Saved as final_cleaned_customer_details.csv.

**Product Details:**
- Resolved encoding: Saved product details x.xlsx as UTF-8 CSV.
- Trimmed text columns (e.g., product_name, category) with CLEAN(TRIM()) (Excel) and str.strip() (Python).
- Dropped redundant columns (e.g., category, product_dimensions).
- Cleaned selling_price: Removed “$”; averaged ranges; converted to float.
- Cleaned shipping_weight: Extracted numbers; converted to pounds; made float.
- Parsed product_dimensions into length, width, height.
- Standardized is_amazon_seller to boolean.
- Handled missing values: Filled categoricals with “No [column name]”; imputed numerics with category-specific medians; dropped rows missing selling_price or category_level1.
- Removed duplicate unique_id.
- Saved as final_cleaned_producct_details.csv. (~9,500 rows, ~19 columns).

**Merge:**
- Loaded cleaned CSVs using pandas.
- Merged Sales with Products on Product ID (left join), then with Customers on Customer ID (left join).
- Handled missing values: Dropped critical missing rows; filled categoricals with “Unknown”; imputed numerics with medians.
- Saved as merged_data.csv (~2,800 rows, ~40 columns) and merged_data.xlsx.

**Challenges:**
- ~60% missing Timestamp values, limiting time-based analysis.
- Non-numeric formats in selling_price and shipping_weight.
- Solution: Dropped Timestamp, filled missing categoricals with “Unknown,” converted to numeric formats.
- Outputs: final_cleaned_interactions.csv, final_cleaned_customer_details.csv, final_cleaned_product_details.csv, merged_data.csv, merged_data.xlsx.

**Analyze**

**Exploratory Data Analysis (EDA):**
- Loaded merged_data.xlsx using pandas in analysis.ipynb.
- Converted time_stamp to datetime (though excluded due to missingness).
- Explored dataset: shape (2,950 rows, 40 columns), columns (e.g., Customer ID, Purchase Amount (USD), product_name, Age, Gender, location, discount_applied, promo_code_used, subscription_status), data types, missing values (~1% in critical columns, ~60% in Timestamp), and 22 unique category_level1 values (e.g., Toys & Games, Clothing, Unknown).
- Summary statistics: Average selling_price ~$30, Purchase Amount (USD) ~$59, Age ~44.
- Planned visualizations: Histograms for Age, selling_price; bar plots for category_level1.

**Deeper Analysis:**
- Dropped rows with missing critical columns (selling_price, purchase_amount(usd), product_name, category_level1, age, gender, location, discount_applied, promo_code_used, subscription_status).
- Calculated revenue (purchase_amount(usd)) by:
- Products: Top 10 (product_name).
- Categories: Top 5 (category_level1).
- Customer segments: Age groups (<25, 25–34, 35–44, 45+), gender, top 5 location.
- Discounts: discount_applied, promo_code_used, subscription_status (avg purchase amount, frequency).
- Generated bar plots: top_products.png, top_categories.png, age_revenue.png, gender_revenue.png, location_revenue.png, discount_revenue.png, frequency_revenue.png.
- Saved summaries: product_summary.csv, category_summary.csv, age_summary.csv, gender_summary.csv, location_summary.csv, discount_summary.csv, frequency_summary.csv.

**Answered Questions:**
- Which products and categories generate the most revenue? (Top products/categories identified.)
- Which customer segments contribute the most to revenue? (Age, gender, location analyzed.)
- Do discounts or subscription status increase purchase amounts or repeat purchases? (No significant increase; avg purchase amounts range from $58.96 to $60.05, frequency is 1.0 across all groups.)
- How does customer age influence purchasing patterns for top categories? (45+ drive Toys & Games.)
- Which regions show potential for targeted marketing? (Even distribution suggests broad reach.)

**Key Findings:**
- Top Products: Wildkin Microfiber Nap Mat: $150, Rubie's Women's Batman Costume Top: $136, Ceaco Puzzle: $126, Childrens Christmas Bunny Jumper: $100, Fisher-Price #Selfie Fun Phone: $100.
- Top Categories: Toys & Games: $123,165, Unknown: $16,395, Clothing, Shoes & Jewelry: $10,489, Home & Kitchen: $9,713, Sports & Outdoors: $6,657.

**Customer Segments:**
- Age Groups: <25: $18,772, 25–34: $35,381, 35–44: $33,328, 45+: $88,500.
- Gender: Female: $20,704, Male: $155,277.
- Location: West Virginia: $4,259, Idaho: $4,215, California: $4,157, Illinois: $4,137, Nevada: $4,120.
- Discounts/Subscriptions (Based on discount_summary.csv and frequency_summary.csv):
- Average purchase amounts: $60.05 (no discount, no promo, not subscribed), $58.96 (discount and promo, not subscribed), $59.57 (discount, promo, and subscribed).
- Total revenue: $78,241 (no discount, no promo, not subscribed), $36,086 (discount and promo, not subscribed), $61,654 (discount, promo, and subscribed).
- Purchase counts: 1,303 (no discount, no promo, not subscribed), 612 (discount and promo, not subscribed), 1,035 (discount, promo, and subscribed).
- Average purchase frequency: 1.0 across all groups.

**Insights:**
- Toys & Games dominates (~70% of revenue); prioritize inventory/marketing.
- 45+ customers and males drive most revenue, likely for Toys & Games; target older males.
- Customers aged 45+ likely drive Toys & Games purchases, suggesting family-oriented buying.
- Males contribute ~90% of revenue; explore female-targeted products (e.g., clothing).
- Discounts and subscriptions show no significant increase in average purchase amounts ($58.96–$60.05) or purchase frequency (1.0 across all groups), possibly due to data limitations (e.g., no repeat purchases) or the need to isolate discount_applied and subscription_status effects.
- “Unknown” category (9% of revenue) includes products with missing category_level1 labels, likely spanning multiple categories, skewing insights; requires reclassification in Step 3.
- Evenly distributed location revenue suggests broad market reach; consider regional promotions.

**Challenges:**
- ValueError: All arrays must be of the same length when combining product and category summaries.
  Solution: Created separate CSVs for each summary.
- KeyError due to incorrect column names (e.g., Purchase Amount (USD) vs. purchase_amount(usd)).
  Solution: Standardized column names in code.
- ~60% missing Timestamp limited time-based analysis; focused on static metrics.
- “Unknown” category’s $16,395 revenue indicates missing labels across multiple categories.
  Solution: Noted for reclassification in Step 3 (e.g., via product_name analysis)
- FileNotFoundError for merged_data.csv due to incorrect file format.
 Solution: Updated to load merged_data.xlsx with openpyxl.
- Uniform purchase frequency (1.0) suggests data may not capture repeat purchases.
 Solution: Noted for further investigation in Step 3.

Outputs: analysis.ipynb, product_summary.csv, category_summary.csv, age_summary.csv, gender_summary.csv, location_summary.csv, discount_summary.csv, frequency_summary.csv, top_products.png, top_categories.png, age_revenue.png, gender_revenue.png, location_revenue.png, discount_revenue.png, frequency_revenue.png.

**Repository Structure**

- analysis.ipynb: EDA and deeper analysis code and findings.
- merge_ecommerce_datasets_excel.ipynb: Dataset merging code.
- merged_data.csv: Merged dataset (CSV version).
- merged_data.xlsx: Merged dataset (Excel version).
- final_cleaned_interactions.csv: Cleaned Sales data.
- final_cleaned_customer_details.csv: Cleaned Customer data.
- final_cleaned_product_details.csv: Cleaned Product data.
- product_summary.csv: Top 5 products by revenue.
- category_summary.csv: Top 5 categories by revenue.
- age_summary.csv: Revenue by age group.
- gender_summary.csv: Revenue by gender.
- location_summary.csv: Top 5 locations by revenue.
- discount_summary.csv: Purchase amount by discount/subscription status.
- frequency_summary.csv: Purchase frequency by discount/subscription status.
- data_cleaning.md: Data cleaning process.
- step2_analysis.md: Deeper analysis summary
Plots: top_products.png, top_categories.png, age_revenue.png, gender_revenue.png, location_revenue.png, discount_revenue.png, frequency_revenue.png.

**Tools Used**

- Python: pandas, numpy, matplotlib, seaborn, openpyxl (for cleaning, EDA, analysis).
- Jupyter Notebook: For code execution.
- Google Sheets: For initial Sales and Customer cleaning.
- Excel: For Product cleaning and dataset verification.
- Tableau: Planned for Step 3 visualizations.

## Share – Tableau Dashboard
- Created interactive dashboard in **Tableau Public** using `merged_data.xlsx` with 6 visualizations (Treenao, Bar, Pie, Map).  
- Removed Frequency chart (all values = 1.0) and summarized as insight.  
- Added KPI cards, title, and key insights directly on dashboard.  
- Exported as `.twb` (editable) and `.png` (presentation).

## Act

## Key Findings
1. **Toys & Games** = **70%** of total revenue ($123,165)  
2. **45+ age group** drives **50%** ($88,500) — **90% male**  
3. **Discounts reduce** avg order value: **$60.05 → $58.96**  
4. **No repeat purchases** (frequency = 1.0)

## Recommendations
| Action | Impact |
|-------|--------|
| **Increase Toys & Games inventory** | Capture 70% revenue segment |
| **Target 45+ males** via Facebook/YouTube ads | Reach high-value customers |
| **Re-evaluate discount strategy** | Prevent $1.09 loss per order |
| **Collect customer ID** in future data | Enable repeat purchase tracking |

**Prepared by: Mensura Abdo**  
**Date: October 27, 2025**




