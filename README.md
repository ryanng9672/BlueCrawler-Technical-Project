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









