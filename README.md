# E-Commerce Data Analysis - Google Data Analytics Capstone
## Step 1: E-Commerce Data Cleaning Process

**Objective**: Clean and standardize Sales, Customer, and Product datasets to produce a unified merged_data.csv for analysis.

**Dataset**:
Sales Data (~3,000 rows, columns: user_id, product_id, Interaction Type, Timestamp, etc.).
Customer Details (~3,000 rows, ~18 columns: customer_id, Age, Gender, Location, etc.).
Product Details (product details x.xlsx, ~10,002 rows, ~24 columns: unique_id, product_name, selling_price, etc.).

**Process**:
Sales Data:
Filtered for Interaction Type = purchase (Google Sheets).
Removed unnecessary columns (e.g., “Unnamed: 4”) (Google Sheets).
Renamed user_id to Customer ID, product_id to Product ID (Google Sheets).
Handled missing values: Replaced blanks in Interaction Type with “unknown”; removed rows missing Customer ID or Product ID (Google Sheets).
Standardized Timestamp: Removed spaces with TRIM(); converted to date-time (Google Sheets).
Removed duplicates using Data Cleanup (Google Sheets).
Saved as final_cleaned_interactions.csv (Google Sheets) 

Customer Details:
Cleaned customer_id: Removed spaces with TRIM(); removed duplicates (Google Sheets).
Validated Age: Replaced missing/unrealistic values with median or “Unknown” (Google Sheets).
Standardized Gender: Unified to “Male”/“Female”; filled missing with “Unknown” (Google Sheets).
Ensured numeric purchase data using text-to-columns (Google Sheets).
Saved as final_cleaned_customer_details.csv (Google Sheets).

Product Details:
Resolved encoding: Saved product details x.xlsx as UTF-8 CSV (Excel).
Trimmed text columns (e.g., product_name, category) with CLEAN(TRIM()) (Excel) and str.strip() (Python).
Dropped redundant columns (category, product_dimensions, category_level5+) (Python).
Cleaned selling_price: Removed “$”; averaged ranges; converted to float (Python).
Cleaned shipping_weight: Extracted numbers; converted to pounds; made float (Python).
Parsed product_dimensions into length, width, height (Python).
Standardized is_amazon_seller to boolean (Excel: =IF(cell="true",1,0); Python: mapped to True/False).
Handled missing values: Filled categoricals with “No [column name]”; imputed numerics with category-specific medians; dropped rows missing selling_price or category_level1 (Python).
Removed duplicate unique_id (Excel, Python).
Saved as final_cleaned_product_details.csv (~9,500 rows, ~19 columns) using clean_product_details_csv_custom.py (Python).

Merge:
Loaded cleaned CSVs using pandas (Python).
Renamed columns for consistency: user_id, customer_id, unique_id to Customer ID or Product ID (Python).
Merged Sales with Products on Product ID (left join), then with Customers on Customer ID (left join) (Python).
Handled missing values: Dropped critical missing rows; filled categoricals with “Unknown”; imputed numerics with medians (Python).
Saved as merged_data.csv and merged_data.xlsx using merge_ecommerce_datasets_excel.py (Python).

**Key Findings**:
Sales Data: Filtered to ~2,800 purchase records; no duplicates; standardized Timestamp and names.
Customer Details: ~2,900 unique Customer ID; valid Age (18–80); consistent Gender.
Product Details: ~9,500 rows; ~19 columns; numeric selling_price (~$5–$500), shipping_weight, length, width, height; minimal missing values
Merged Dataset: merged_data.csv (~2,800 rows, ~40 columns) ready for analysis.

**Tools Used**: Google Sheets, Excel, Python (pandas, openpyxl), Jupyter Notebook.


## Step 2: Exploratory Data Analysis (EDA)
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




