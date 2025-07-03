# Amazon-Product-Review-Analysis
product analysis, customer review for data generation and insights leading to product improvement, marketing strategies, and customer engagement.
. Average Discount Percentage by Product Category
We'll group by category and calculate the mean of discount_percentage.

avg_discount_by_category = df_clean.pivot_table(values='discount_percentage', index='category', aggfunc='mean').sort_values(by='discount_percentage', ascending=False)
avg_discount_by_category


1. Average Discount Percentage by Product Category

Here are the top categories with the highest average discount percentages:

Category	Avg. Discount %
Electronics → Mobile Accessories	90.0%
Computers & Accessories → Peripherals (Cables/Adapters)	90.0%
Electronics → Headphones, Earbuds & Accessories → Earpads	90.0%
Electronics → Headphones, Earbuds & Accessories → Adapters	88.0%
Computers & Accessories → Keyboards	87.5%

Many categories have 0% discount, suggesting no markdowns for those items.

Proceeding to Question 2: How many products are listed under each category. 

2. Number of Products Listed Under Each Category

Top 5 categories with the most products:

Category	Number of Products
Computers & Accessories → Accessories & Peripherals → Cables	233
Electronics → Wearable Technology → Smartwatches	76
Electronics → Smartphones & Basic Mobiles	68
Electronics → Televisions	63
Electronics → Headphones & Earbuds	52

Next, let's answer Question 3: What is the total number of reviews per category. 

3. Total Number of Reviews per Category

Top categories with the most customer reviews:

Category	Total Reviews
Electronics → Headphones & Earbuds	4,204,939
Computers & Accessories → Cables	3,547,816
Electronics → Smartphones & Basic Mobiles	2,493,269
Electronics → TV Accessories → Cables	1,906,054
Electronics → Smartwatches	1,644,476

Now moving to Question 4: Which products have the highest average ratings.
We’ll identify top-rated products based on rating and then sort by number of reviews as a secondary criterion. 

4. Products with the Highest Average Ratings

Here are the top-rated products:

Product Name	Rating	Number of Reviews
Amazon Basics Wireless Mouse	5.0	23
Syncwire Lightning to USB Cable	5.0	5
REDTECH USB-C to Lightning Cable	5.0	0
Swiffer Instant Electric Water Heater Faucet Tap	4.8	53,803
Instant Pot Air Fryer, Vortex 2QT	4.8	3,964

While several products have perfect 5.0 ratings, Swiffer Instant Electric Water Heater Faucet Tap stands out for having a high rating and a large number of reviews.

Next, we’ll address Question 5: What is the average actual price vs discounted price by category. 

5. Average Actual Price vs Discounted Price by Category

Here are the top 5 categories with the highest average actual prices:

Category	Avg. Actual Price	Avg. Discounted Price
Home → Air Conditioners	₹75,990	₹42,990
Laptops	₹59,890	₹37,247
Home → Vacuum & Cleaning Appliances	₹44,949	₹23,449
Televisions	₹40,132	₹24,840
Tablets	₹37,999	₹26,999

This illustrates how high-end categories receive significant markdowns.

6: Which products have the highest number of reviews? 

6. Products with the Highest Number of Reviews

These products have received the most customer reviews:

Product Name	No. of Reviews	Rating
Amazon Basics HDMI Cable (multiple listings)	426,973	4.4
boAt Bassheads 100 Wired Earphones	363,713	4.1
Redmi 9 Series Smartphones (various models)	313,836	4.1

Multiple duplicate listings for the same products suggest they are either bundled differently or sold by different sellers.

7: How many products have a discount of 50% or more? 

7. Number of Products with a Discount of 50% or More

751 products have a discount of 50% or more, which is over half the dataset (51.2%).

Question 8: What is the distribution of product ratings (e.g., how many products are rated 3.0, 4.0, etc.)? 

8. Distribution of Product Ratings

Here’s how product ratings are distributed:

Most common ratings:

4.0 → 181 products

4.1 → 244 products

4.2 → 228 products

4.3 → 230 products

Less common ratings:

Only 3 products are rated 5.0

Very few products fall below 3.0

This shows that the majority of products cluster around the 4.0 to 4.3 range.

9: What is the total potential revenue (actual_price × rating_count) by category? 

9. Total Potential Revenue by Category
(Calculated as actual_price × rating_count)

Top categories with the highest revenue potential:

Category	Potential Revenue (₹)
Smartphones & Basic Mobiles	₹38.5 billion
Televisions	₹26.2 billion
Smartwatches	₹13.3 billion
Headphones & Earbuds	₹7.9 billion
Cables (Computers & Accessories)	₹3.0 billion

This metric highlights where the biggest commercial opportunities lie based on popularity and pricing.

Question 10: What is the number of unique products per price range bucket (<₹200, ₹200–₹500, >₹500)?
# 9. Total potential revenue (actual_price × rating_count) by category

# Create a new column for potential revenue
df_clean['potential_revenue'] = df_clean['actual_price'] * df_clean['rating_count']

# Group by category to calculate total potential revenue
revenue_by_category = df_clean.pivot_table(
    values='potential_revenue',
    index='category',
    aggfunc='sum'
).sort_values(by='potential_revenue', ascending=False)

revenue_by_category.head(10)  # top 10 categories by potential revenue

                                                  potential_revenue
category                                                             
Electronics|Mobiles&Accessories|Smartphones&Bas...       3.850072e+10
Electronics|HomeTheater,TV&Video|Televisions|Sm...       2.623706e+10
Electronics|WearableTechnology|SmartWatches              1.327448e+10
Electronics|Headphones,Earbuds&Accessories|Head...       7.891731e+09
Computers&Accessories|Accessories&Peripherals|C...       2.988615e+09
Electronics|Accessories|MemoryCards|MicroSD              2.615838e+09
Home&Kitchen|Kitchen&HomeAppliances|SmallKitche...       1.641979e+09
Electronics|Mobiles&Accessories|MobileAccessori...       1.597848e+09
Electronics|Headphones,Earbuds&Accessories|Head...       1.585623e+09
Electronics|HomeTheater,TV&Video|Accessories|Ca...       1.569589e+09

10. Number of Unique Products per Price Range Bucket

Price Range	Number of Products
< ₹200	39
₹200 – ₹500	181
> ₹500	1,245

The vast majority of products are priced above ₹500, indicating a focus on mid-to-premium priced items.

Question 11: How does the rating relate to the level of discount?
We'll examine this by computing the correlation between rating and discount_percentage. 

11. Relationship Between Rating and Discount
12.
13. The correlation between rating and discount percentage is approximately -0.155.

Interpretation:
There’s a weak negative correlation, meaning products with higher discounts tend to have slightly lower ratings — but the relationship is not strong enough to be definitive.

Question 12: How many products have fewer than 1,000 reviews? 

12. Number of Products with Fewer Than 1,000 Reviews

328 products have fewer than 1,000 reviews, which is about 22.4% of the dataset.

Question 13: Which categories have products with the highest discounts?
We’ll find the maximum discount percentage in each category. 

13. Categories with the Highest Product Discounts

Top 5 categories with products having the highest discount percentages:

Category	Max Discount %
Accessories & Peripherals → Adapters	94%
Smartwatches	91%
Mobile Accessories (e.g., Cables, Chargers, etc.)	90%
Small Kitchen Appliances	90%
Headphone Accessories → Earpads	90%

Many accessories and wearable categories show extremely high discounting strategies.

14: Identify the top 5 products in terms of rating and number of reviews combined.
We'll define a combined score using a weighted sum or product of rating × log(review count). 

Top 5 Products by Combined Rating & Number of Reviews

Using a combined score of rating × log(review count), here are the top performers:

Product Name	Rating	Reviews	Combined Score
Amazon Basics HDMI Cable (multiple listings)	4.4	426,973	57.04
SanDisk Extreme SD UHS I 64GB Card

PREPARATION
Before starting, we make sure:

You clean your data by:

Removing ₹ symbols and commas from actual_price

Use: =SUBSTITUTE(SUBSTITUTE(A2,"₹",""),",","")

Converting rating to numeric (if it says "out of 5 stars", use: =LEFT(A2,3) and format as number)

EDA QUESTIONS & EXCEL OPERATIONS
1. What is the average discount percentage by product category?
Steps:

Select all data.

Go to Insert → PivotTable.

In Pivot Table:

Rows: category

Values: discount_percentage (set to Average)

This gives average discounts by category.

2. How many products are listed under each category?
Pivot Table Steps:

Rows: category

Values: product_id or product_name (set to Count)

This counts products per category.

3. What is the total number of reviews per category?
Pivot Table Steps:

Rows: category

Values: rating_count (set to Sum)

Shows total reviews by category.

4. Which products have the highest average ratings?
Steps:

Sort your data:

Select all data.

Go to Data → Sort:

Sort by rating (Largest to Smallest)

Then by rating_count (Largest to Smallest)

Top rows are your highest-rated products.

5. What is the average actual price vs discounted price by category?
Pivot Table Steps:

Rows: category

Values:

actual_price (set to Average)

discounted_price (set to Average)

Compare average pricing across categories.

6. Which products have the highest number of reviews?
Steps:

Sort your data:

By rating_count (Largest to Smallest)

Top rows show most-reviewed products.

7. How many products have a discount of 50% or more?
Steps:

Use formula:
=IF(discount_percentage>=0.5,1,0)

Sum this new column.

Total gives number of 50%+ discounted products.

8. What is the distribution of product ratings (e.g., 3.0, 4.0, etc.)?
Steps:

Create a Pivot Table:

Rows: rating

Values: product_id (set to Count)

You’ll get a distribution of ratings.

9. What is the total potential revenue (actual_price × rating_count) by category?
Steps:

Create new column:

=actual_price * rating_count

Create Pivot Table:

Rows: category

Values: new column (set to Sum)

Gives potential revenue by category.

10. Unique products per price range bucket (<₹200, ₹200–₹500, >₹500)
Steps:

Create a helper column:

=IF(actual_price<200,"<₹200",IF(actual_price<=500,"₹200–₹500",">₹500"))
Create Pivot Table:

Rows: new bucket column

Values: product_name (set to Count (Distinct))

Bucketed price ranges.

11. How does the rating relate to the level of discount?
Steps:

Use CORREL function:

=CORREL(rating_range, discount_percentage_range)
Returns correlation coefficient (should be weak negative).

12. How many products have fewer than 1,000 reviews?
Steps:

Use formula:

=IF(rating_count<1000,1,0)
Sum this column.

Gives count of low-reviewed products.

13. Which categories have products with the highest discounts?
Pivot Table Steps:

Rows: category

Values: discount_percentage (set to Max)

Shows highest discount % per category.

14. Top 5 products by rating × number of reviews combined
Steps:

Add new column:

=rating * LN(rating_count + 1)
Sort this column in descending order.

Top 5 products at the top.

BONUS: FORMULAS SUMMARY
Task	Formula
Clean actual_price	=SUBSTITUTE(SUBSTITUTE(A2,"₹",""),",","")
Clean rating	=LEFT(A2,3)
Discount ≥ 50%	=IF(discount_percentage>=0.5,1,0)
Revenue	=actual_price * rating_count
Price Bucket	=IF(actual_price<200,"<₹200",IF(actual_price<=500,"₹200–₹500",">₹500"))
Correlation	=CORREL(rating_range, discount_percentage_range)
Combined Score	=rating * LN(rating_count + 1)

![image](https://github.com/user-attachments/assets/c55e8fe7-b9ae-4561-9010-cf3911f78ffd)

![image](https://github.com/user-attachments/assets/1e80d734-d128-47b9-a22f-2796f04e91ac)

![image](https://github.com/user-attachments/assets/63559e74-bd29-4a90-a367-78590e8d5166)


