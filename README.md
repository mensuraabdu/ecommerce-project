# E-Commerce Data Analysis - Google Data Analytics Capstone
## Step 1: E-Commerce Data Cleaning Process

**Objective**: Clean and standardize Sales, Customer, and Product datasets to produce a unified merged_data.csv for analysis.

**Dataset**:
- Sales Data (~3,000 rows, columns: user_id, product_id, Interaction Type, Timestamp, etc.).
- Customer Details (~3,000 rows, ~18 columns: customer_id, Age, Gender, Location, etc.).
- Product Details (product details x.xlsx, ~10,002 rows, ~24 columns: unique_id, product_name, selling_price, etc.).

**Process**:

**Sales Data:**
- Filtered for Interaction Type = purchase (Google Sheets).
- Removed unnecessary columns (e.g., “Unnamed: 4”) (Google Sheets).
- Renamed user_id to Customer ID, product_id to Product ID (Google Sheets).
- Handled missing values: Replaced blanks in Interaction Type with “unknown”; removed rows missing Customer ID or Product ID (Google Sheets).
- Standardized Timestamp: Removed spaces with TRIM(); converted to date-time (Google Sheets).
- Removed duplicates using Data Cleanup (Google Sheets).
- Saved as final_cleaned_interactions.csv (Google Sheets) 

**Customer Details:**
- Cleaned customer_id: Removed spaces with TRIM(); removed duplicates (Google Sheets).
- Validated Age: Replaced missing/unrealistic values with median or “Unknown” (Google Sheets).
- Standardized Gender: Unified to “Male”/“Female”; filled missing with “Unknown” (Google Sheets).
- Ensured numeric purchase data using text-to-columns (Google Sheets).
- Saved as final_cleaned_customer_details.csv (Google Sheets).

**Product Details:**
- Resolved encoding: Saved product details x.xlsx as UTF-8 CSV (Excel).
- Trimmed text columns (e.g., product_name, category) with CLEAN(TRIM()) (Excel) and str.strip() (Python).
- Dropped redundant columns (category, product_dimensions, category_level5+) (Python).
- Cleaned selling_price: Removed “$”; averaged ranges; converted to float (Python).
- Cleaned shipping_weight: Extracted numbers; converted to pounds; made float (Python).
- Parsed product_dimensions into length, width, height (Python).
- Standardized is_amazon_seller to boolean (Excel: =IF(cell="true",1,0); Python: mapped to True/False).
- Handled missing values: Filled categoricals with “No [column name]”; imputed numerics with category-specific medians; dropped rows missing selling_price or category_level1 (Python).
- Removed duplicate unique_id (Excel, Python).
- Saved as final_cleaned_product_details.csv (~9,500 rows, ~19 columns) using clean_product_details_csv_custom.py (Python).

**Merge:**
- Loaded cleaned CSVs using pandas (Python).
- Renamed columns for consistency: user_id, customer_id, unique_id to Customer ID or Product ID (Python).
- Merged Sales with Products on Product ID (left join), then with Customers on Customer ID (left join) (Python).
- Handled missing values: Dropped critical missing rows; filled categoricals with “Unknown”; imputed numerics with medians (Python).
- Saved as merged_data.csv and merged_data.xlsx using merge_ecommerce_datasets_excel.py (Python).

**Key Findings**:
- Sales Data: Filtered to ~2,800 purchase records; no duplicates; standardized Timestamp and names.
- Customer Details: ~2,900 unique Customer ID; valid Age (18–80); consistent Gender.
- Product Details: ~9,500 rows; ~19 columns; numeric selling_price (~$5–$500), shipping_weight, length, width, height; minimal missing values
- Merged Dataset: merged_data.csv (~2,800 rows, ~40 columns) ready for analysis.

**Tools Used**: Google Sheets, Excel, Python (pandas, openpyxl), Jupyter Notebook.


## Step 2: Exploratory Data Analysis (EDA)

**Objective**: Understand the structure, quality, and key characteristics of the merged e-commerce dataset to prepare for further analysis.

**Dataset**: merged_data.csv (~3,000 rows, 40 columns), combining Sales, Customer, and Product Details.

**Process**:
- Loaded merged_data.csv using pandas.
- Converted time_stamp to Timestamp (datetime format) for time-based analysis.
- Explored dataset shape, columns, data types, missing values, summary statistics, and unique product categories.
- Identified high missingness in Timestamp; planned to drop or impute in further analysis.
- Saved merged_data.xlsx for Excel and Tableau analysis.

**Key Findings**:
- Shape: 2,950 rows, 40 columns.
- **Columns**: Includes Customer ID, Product ID, selling_price, Purchase Amount (USD), product_name, category_level1, Age, Gender, Timestamp, item_purchased, category, location, size, season, review_rating, subscription_status, shipping_type, discount_applied, promo_code_used, previous_purchases, payment_method, frequency_of_purchases, etc.
- **Missing values**: ~1% in Customer ID, Product ID, selling_price, product_name, category_level1; ~2% in Age, Gender; ~60% in Timestamp; minimal in others.
- **Categories:** 22 unique category_level1 values: Sports & Outdoors, Clothing, Shoes & Jewelry, Toys & Games, Health & Household, Baby Products, Home & Kitchen, Arts, Crafts & Sewing, Pet Supplies, Office Products, Hobbies, Patio, Lawn & Garden, Grocery & Gourmet Food, Beauty & Personal Care, Industrial & Scientific, Tools & Home Improvement, Video Games, Remote & App Controlled Vehicle Parts, Automotive, Remote & App Controlled Vehicles & Parts, Electronics, Musical Instruments, Unknown (to be addressed in further cleaning).
- **Summary Statistics:** Average selling_price ~$30, Purchase Amount (USD) ~$59, Age ~44.
- **Planned Visualizations:** Histograms for Age, selling_price; bar plots for category_level1 to explore distributions.

**Tools Used**: Python (pandas, numpy), Jupyter Notebook.

**Step 3: Deeper Analysis**

**Objective:** Analyze top products and categories by revenue, and explore customer segments by age, gender, and location to identify sales drivers.

**Dataset:** merged_data.csv (~2,950 rows, 40 columns), combining Sales, Customer, and Product Details.

**Process:**
Loaded merged_data.csv using pandas.
Dropped rows with missing selling_price, purchase_amount(usd), product_name, category_level1, age, gender, or location.
Calculated total revenue (purchase_amount(usd)) by:
Product (product_name): Top 10 products.
Category (category_level1): Top 5 categories.
Customer segments: Age groups (<25, 25–34, 35–44, 45+), gender, and top 5 location.
Generated bar plots for top products, categories, age groups, gender, and locations.
Saved results as product_summary.csv, category_summary.csv, age_summary.csv, gender_summary.csv, and location_summary.csv, and plots as PNGs.

**Key Findings:**

**Top Products:** Wildkin Microfiber Nap Mat with Pillow for Toddler Boys and Girls, Perfect Size for Daycare and Preschool, Designed to Fit on a Standard Cot, Patterns Coordinate with Our Lunch Boxes and Backpacks :$150, Rubie's Women's Batman v Superman: Dawn of Justice Wonder Woman Costume Top : $136, Ceaco Perfect Piece Count Puzzle - Thomas Kinkade Disney Dreams Collection - Beauty and the Beast : $126, Childrens Christmas Bunny Jumper : $100, Fisher-Price #Selfie Fun Phone, Baby Rattle, Mirror and Teething Toy :$100, DC Comics Multiverse DC Rebirth the Ray Figure : $100, Random Esoteric Creature Generator for Classic Fantasy Rpgs & Their Modern Simulacra : $100, Batgirl Child Costume in Pink : $100, Creative Converting 991199 Graduation Cap Cutouts, One Size, Black : $100, Amscan Suspenders, Party Accessory, Rainbow : $100. 
Top Categories: Toys & Games : $123165, Unknown : $16395, Clothing, Shoes & Jewelry : $10489, Home & Kitchen : $9713, Sports & Outdoors : $6657.

**Customer Segments:**
- **Age Groups:** <25 : $18772, 25-34 : $35381, 35-44 : $33328, 45+ : $88500.
- **Gender:** Female : $20704, Male : $155277. 
- **Location:** West Virginia : $4259, Idaho : $4215, California : $4157, Illinois : $4137, Nevada : $4120. 

**Insights**
- Toys & Games is the dominant category, generating over 70% of total revenue, indicating strong demand for toys and games. The business should prioritize inventory and marketing for this category.

- Customers aged 45+ drive the majority of revenue, likely purchasing toys for younger family members. Marketing campaigns targeting older adults (e.g., parents, grandparents) could boost sales.

- Males account for nearly 90% of revenue, suggesting products or marketing may appeal more to male customers. Exploring female-targeted products (e.g., clothing, jewelry) could diversify the customer base.

- The significant revenue from the “Unknown” category indicates data quality issues that need resolution to improve analysis accuracy.

- Revenue is evenly distributed across locations, suggesting a broad market reach. Targeted regional promotions may further increase sales.

**Data Note:** Excluded Timestamp due to ~60% missing values; focused on non-time-based metrics.

**Tools Used:** Python (pandas, numpy, matplotlib, seaborn), Jupyter Notebook.

**Outputs:**
product_summary.csv: Top 5 products by revenue.
category_summary.csv: Top 5 categories by revenue.
age_summary.csv: Revenue by age group.
gender_summary.csv: Revenue by gender.
location_summary.csv: Top 5 locations by revenue.
Plots: top_products.png, top_categories.png, age_revenue.png, gender_revenue.png, location_revenue.png.








