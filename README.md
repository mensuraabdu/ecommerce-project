# ecommerce-project
Google Data Analytics Capstone: E-Commerce Sales Analysis
E-Commerce Data Cleaning Process
This document outlines the cleaning process for the e-commerce dataset used in the Google Data Analytics Capstone project. The dataset comprises three components: Sales Data, Customer Details, and Product Details, cleaned to produce UTF-8 encoded CSVs (final_cleaned_interactions.csv, final_cleaned_customer_details.csv, final_cleaned_product_details.csv) for merging and analysis. Tools used include Google Sheets, Excel, and Python (pandas, openpyxl).
1. Sales Data Cleaning

Dataset: Sales data (columns: user_id, product_id, Interaction Type, Timestamp, etc.).
Issues:
Missing values in Interaction Type.
Unnecessary columns (e.g., “Unnamed: 4”).
Inconsistent column names (user_id, product_id).
Extra spaces in Timestamp.
Duplicates and inconsistent categorical formats.
Non-standardized timestamps.


Cleaning Steps:
Filtered Purchases (Google Sheets): Kept rows where Interaction Type = purchase using filters.
Removed Columns (Google Sheets): Deleted “Unnamed: 4” via column deletion.
Standardized Names (Google Sheets): Renamed user_id to Customer ID, product_id to Product ID.
Handled Missing Values (Google Sheets): Replaced blanks in Interaction Type with “unknown”; removed rows missing Customer ID or Product ID; labeled other blanks as “Unknown”.
Standardized Timestamps (Google Sheets): Used TRIM() to remove spaces; converted to date-time format; removed out-of-range dates.
Removed Duplicates (Google Sheets): Used Data > Remove Duplicates.
Standardized Categoricals (Google Sheets): Converted Interaction Type to lowercase (e.g., “purchase”).
Output (Google Sheets): Saved as final_cleaned_interactions.csv (UTF-8).


Outcome: Clean sales dataset with purchases only, standardized names, no duplicates, consistent timestamps, and minimal missing values.

2. Customer Details Cleaning

Dataset: Customer details (~18 columns: Customer ID, Age, Gender, Location, purchase data).
Issues:
Duplicate/inconsistent Customer ID.
Missing/unrealistic Age.
Inconsistent Gender categories.
Non-numeric purchase data.
Missing values.


Cleaning Steps:
Cleaned IDs (Google Sheets): Used TRIM() and Remove Duplicates for Customer ID.
Validated Age (Google Sheets): Replaced missing/unrealistic ages (e.g., negative, >100) with median or “Unknown”; removed invalid entries.
Standardized Gender (Google Sheets): Unified “M”/“Male” to “Male”; filled missing with “Unknown”.
Cleaned Purchase Data (Google Sheets): Converted purchase columns to numeric using text-to-columns.
Handled Missing Values (Google Sheets): Filled categorical blanks with “Unknown”.
Standardized Formats (Google Sheets): Ensured lowercase categoricals and numeric formats.
Output (Google Sheets): Saved as final_cleaned_customer_details.csv (UTF-8).


Outcome: Standardized dataset with unique IDs, valid ages, consistent genders, numeric purchases, and minimal missing values.

3. Product Details Cleaning

Dataset: Product details (product details x.xlsx, ~10,002 rows, 24 columns: unique_id, product_name, category, selling_price, etc.).
Issues:
Non-UTF-8 encoding.
Spaces in text columns.
High missing values (~85% in model_number, ~50% in length, width, height, ~70–100% in category_level3+).
Redundant columns (category, product_dimensions).
Non-numeric selling_price (e.g., “$48.99”).
Non-standard shipping_weight (e.g., “1.2 pounds (View shipping rates)”).
Long about_product text.
Non-boolean is_amazon_seller.
Duplicate unique_id.


Cleaning Steps:
Resolved Encoding (Excel): Saved product details x.xlsx as product details x - Sheet1.csv (UTF-8).
Trimmed Text (Excel): Used =CLEAN(TRIM(cell)) on text columns.
Dropped Columns (Python): Removed category (redundant), product_dimensions, category_level5 to category_level7 (~70–100% missing).
Cleaned selling_price (Python): Removed “$”; averaged ranges (e.g., “$48.99 - $75.49” → 62.24); converted to float.
Cleaned shipping_weight (Python): Extracted numbers; converted ounces to pounds; removed text; converted to float.
Parsed product_dimensions (Python): Split into length, width, height (numeric).
Split category (Python): Created category_level1 to category_level4.
Cleaned image, variants (Python): Kept first URL.
Standardized is_amazon_seller (Excel): Used =IF(cell="true",1,0). (Python): Mapped to boolean.
Limited about_product (Excel): Capped at 1000 characters with =LEFT(CLEAN(cell),1000). (Python): Used str[:1000].
Handled Missing Values (Excel): Replaced blanks with “No [column name]”; imputed numerics with category-specific medians. (Python): Dropped rows missing selling_price or category_level1 (~5–10% loss).
Removed Duplicates (Excel): Eliminated duplicate unique_id. (Python): Confirmed with drop_duplicates().
Output (Python): Used clean_product_details_csv_custom.py to produce final_cleaned_product_details.csv (~9,500–10,000 rows, ~19 columns).


Outcome: Clean dataset with numeric columns, no spaces, minimal missing values, and standardized formats.

4. Merge Process

Process:
Loaded final_cleaned_interactions.csv, final_cleaned_customer_details.csv, final_cleaned_product_details.csv using Python (pandas, openpyxl).
Renamed columns: user_id to Customer ID, product_id to Product ID, customer_id to Customer ID, unique_id to Product ID.
Merged Sales with Products on Product ID (left join), then with Customers on Customer ID (left join).
Handled missing values: Dropped rows missing critical columns; filled categoricals with “Unknown”; imputed numerics with medians.
Saved as merged_data.csv using merge_ecommerce_datasets_excel.py.


Outcome: Unified dataset (merged_data.csv) for analyzing sales trends, customer segments, and product performance.

Tools Used: Google Sheets, Excel, Python (pandas, openpyxl).

# E-Commerce Data Analysis - Google Data Analytics Capstone
## Step 1: Exploratory Data Analysis (EDA)
**Objective**: Understand the structure, quality, and key characteristics of the merged e-commerce dataset to prepare for further analysis.

**Dataset**: `merged_data.csv` (~3,000 rows, ~40 columns), combining Sales, Customer, and Product Details.

**Process**:
- Loaded `merged_data.csv` using pandas.
- Converted `time_stamp` to `Timestamp` (datetime format) for time-based analysis.
- Explored shape, columns, data types, missing values, summary statistics, and unique product categories.
- Saved `merged_data.xlsx` for use in Excel and Tableau.

**Key Findings**:
- Shape: (rows, columns): (2950, 40)
- Columns: Includes `Customer ID`, `Product ID`, `selling_price`, `Purchase Amount (USD)`, `product_name`, `category_level1`, `Age`, `Gender`, `Timestamp`.
- Missing Values: ~ 0% in Customer ID, Product ID, interaction type, time_stamp, product_name, selling_price, model_number, about_product, product_specification, technical_details, shipping_weight, image, variants, product_url, is_amazon_seller, length, width, height, category_level1,category_level2, category_level3, category_level4, age, genderr, item_purchased, category, purchase_amount(usd), location, size, season, review_rating, subscription_status, shippingg type, discount_applied, promo_code_used, previous_purchases, payment_method, frequency_of_purchases; >60% in Timestamp. 
- Categories: Unique categories: 22 ['Sports & Outdoors' 'Clothing, Shoes & Jewelry' 'Toys & Games' 'Unknown'
 'Health & Household' 'Baby Products' 'Home & Kitchen'
 'Arts, Crafts & Sewing' 'Pet Supplies' 'Office Products' 'Hobbies'
 'Patio, Lawn & Garden' 'Grocery & Gourmet Food' 'Beauty & Personal Care'
 'Industrial & Scientific' 'Tools & Home Improvement' 'Video Games'
 'Remote & App Controlled Vehicle Parts' 'Automotive'
 'Remote & App Controlled Vehicles & Parts' 'Electronics'
 'Musical Instruments']
- Summary Stats: Average selling_price ~$30, Purchase Amount (USD) ~$59, Age ~44

**Tools Used**: Python (pandas, numpy), Jupyter Notebook
## Next Steps
- Analyze top products, sales trends, customer segments, and marketing impact.
- Use Excel for PivotTables and Tableau for visualizations.
- Document in `analysis.ipynb` and `README.md`.

## Setup
```bash
pip install pandas numpy openpyxl
jupyter notebook

