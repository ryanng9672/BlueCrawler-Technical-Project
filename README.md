# Interim-Project-BlueCrawler

**Web Scraping** - for Wellcome and Panknshop

**Database** - connection for postgresSQL(ngrok)

**About Web crawler,data cleaning ,insert data , data visualisation**

# Table of Content
* [SET_UP](#SET_UP)
* [Features](#Features)
* [Example](#Example)
* [Technologies](#Technologies)
* [WebsiteRelated](#WebsiteRelated)

# SET_UP
To install the required packages, run the following command:

```shell
pip install -r requirements.txt
```
# Features
* ETL pipeline set-up
* Product detail URL Store in directory in your control
* Generate Csv file for different product detail for each sub-categories
* New data comparison with old data
* data-visualization(Analysis)
* Support for capturing information from websites anytime
* Accuracy according to Product ID(form the ParknShop and Wellcome get the Product ID)

# Example
```shell
#whole process of pns and wellcome data scraping
df_pns.to_csv('pns_data_{}.csv'.format(formatted_date))
df_wc.to_csv('wc_data_{}.csv'.format(formatted_date))
#DataFrame.merge
combined_df = pd.concat([df1, df2], ignore_index=True)
combined_df.to_csv('alldata_28-02-2024.csv', index=False)
# Connect to the database
def connect(host="localhost", database="blue", user="postgres", password="1234"):
    print('Connecting to the database...')
# SQL query to retrieve data from the product_table
sql_query = "SELECT market_id, type, brand, product_origin FROM product_table;"
# Plotting the bar chart
ax = brand_counts.plot(kind='bar', figsize=(10, 6), color=colors)
 plt.title("Number of Unique Brands per Market")
plt.xlabel("Market ID")
plt.ylabel("Number of Unique Brands")
```

**PostgreSQL**

<img width="707" alt="sql" src="https://github.com/ryanng9672/BlueCrawler-Technical-Project/assets/158177590/ffd63148-b734-412f-a99d-2c4f58efe3eb">



**ngrok**

<img width="859" alt="ngrok" src="https://github.com/ryanng9672/BlueCrawler-Technical-Project/assets/158177590/a4e155e6-164b-489d-ac57-594492233743">


**Python call SQL Get data**

<img width="667" alt="top20" src="https://github.com/ryanng9672/BlueCrawler-Technical-Project/assets/158177590/a95cbbd4-9f56-4932-a2d7-74a8caf0170a">



**seabron**

![seabron](https://github.com/ryanng9672/BlueCrawler-Technical-Project/assets/158177590/4dcff042-6e1e-481c-b10d-d21219606e77)

```shell
# Define price segments
price_segments = {
    'Budget-Friendly': (0, 100),
    'Economy': (101, 500),
    'Medium': (501, 1000),
    'Premium': (1001, 1500),
    'Luxury': (1501, float('inf'))
}
```
![螢幕擷取畫面 2024-04-18 091529](https://github.com/ryanng9672/BlueCrawler-Technical-Project/assets/158177590/bea92123-c856-4a1b-8693-0469a7cb5330)

```shell
# Query data from the database and convert it to a DataFrame
sql_query = """
SELECT p.type, p.brand, p.product_origin, d.current_price, p.product, p.product_id, d.market_id
FROM product_table p
JOIN daily_table d ON p.product_id = d.product_id
WHERE (p.brand LIKE '%%禾富巴斯%%' OR p.brand LIKE '%%夏迪%%');
"""

# Try to load data from the database
try:
    data = pd.read_sql_query(sql_query, engine)
    print("Data loaded successfully")
except Exception as e:
    print(f"Error loading data: {e}")
finally:
    engine.dispose()  # Close the database connection

# Add a new column to indicate whether the product name contains '箱'
data['contains_box'] = data['product'].str.contains('箱')
```
![螢幕擷取畫面 2024-04-18 091408](https://github.com/ryanng9672/BlueCrawler-Technical-Project/assets/158177590/c0284712-71b5-41a4-809d-24ce90d0ad08)


```shell
# Convert the 'date' column to datetime format
data['date'] = pd.to_datetime(data['date'], format='%d-%m-%Y')

# Check if the 'current_price' and 'sold_quantity' columns are numeric, if not convert them
data['current_price'] = pd.to_numeric(data['current_price'], errors='coerce')
data['sold_quantity'] = pd.to_numeric(data['sold_quantity'], errors='coerce')

# Group by date to find the average price and total sold quantity for each day
price_trends = data.groupby('date')['current_price'].mean()
sales_trends = data.groupby('date')['sold_quantity'].sum()
```

![螢幕擷取畫面 2024-04-18 091546](https://github.com/ryanng9672/BlueCrawler-Technical-Project/assets/158177590/4b401b34-81dd-4217-8f8d-2ffcade46a56)

```shell
# SQL query using window function to get the latest price record for each product_id and include the product name
sql_query = """
WITH RankedPrices AS (
    SELECT p.product, p.brand, p.product_origin, d.current_price, p.product_id, d.market_id,
           ROW_NUMBER() OVER(PARTITION BY p.product_id ORDER BY d.date DESC) as rn
    FROM product_table p
    JOIN daily_table d ON p.product_id = d.product_id
)
SELECT product, brand, product_origin, current_price, product_id, market_id
FROM RankedPrices
WHERE rn = 1;
"""
# Load data from the database into a DataFrame
try:
    data = pd.read_sql_query(sql_query, engine)
    print("Data loaded successfully")
except Exception as e:
    print(f"Error loading data: {e}")
finally:
    engine.dispose()  # Close the database connection
# Filter data for each supermarket
data_parknshop = data[data['market_id'] == 'parknshop']
data_wellcome = data[data['market_id'] == 'wellcome']
# Find the top 10 highest-priced products for each supermarket
top_10_parknshop = data_parknshop.nlargest(10, 'current_price')
top_10_wellcome = data_wellcome.nlargest(10, 'current_price')
```
![螢幕擷取畫面 2024-04-18 092336](https://github.com/ryanng9672/BlueCrawler-Technical-Project/assets/158177590/6b6b5c6d-f1d1-424f-b724-1a7e3886ff9e)




# Time management tool - Trello Kanban
* For team time management
  ![螢幕擷取畫面 2024-04-18 092930](https://github.com/ryanng9672/BlueCrawler-Technical-Project/assets/158177590/86aefa20-d599-4b53-b410-ae07cf26f8e5)



# Technologies
* pandas
* selenium
* re
* matplotlib
* seaborn
* more in requirements.txt<<<<

# WebsiteRelated
* [https://www.wellcome.com.hk/zh-hant/category/100001/1.html]
* [https://www.pns.hk/zh-hk/search?text=%E9%85%92&useDefaultSearch=false&brandRedirect=true&q=%E9%85%92:mostRelevant:categoryNameLevel2:04012000]
 
* PPT For US[https://tome.app/mid-term-project-team-blue/interim-project-presentation-team-blue-v2-clsmn360c00oyms61kky1tdg9]









