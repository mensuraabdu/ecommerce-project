# ecommerce-project
Google Data Analytics Capstone: E-Commerce Sales Analysis
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
