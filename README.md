## Project Overview
This project analyzes retail inventory and supply chain data to minimize stockouts and optimize inventory distribution by analyzing historical sales, weather patterns, and forecast accuracy. The objective is to help retail businesses maintain optimal stock levels, minimize stockouts and overstocking, and enhance demand fulfillment across the supply chain.

Using historical sales, inventory level, pricing, and demand forecast, the analysis evaluates forecast accuracy, weather impact analysis, holiday/promotion effectiveness, and regional inventory distribution. Key metrics such as stock gap, stockout risk, and price difference are assessed to uncover gaps between demand and actuals.

The project applies data cleaning, business Impact, and visualization techniques to reveal forecast accuracy, seasonality, and bottlenecks within the supply chain.

Business Impact analysis are provided on the following key areas:

- Weather Impact Analysis
- Forecast Accuracy
- Holiday/Promotion Effectiveness
- Regional Inventory Distribution

Check out complete project [here](https://docs.google.com/spreadsheets/d/1v7W445TIZtJWWsrbyfztTBqpNGzUeaUdcH9KupQbxbI/edit?usp=sharing).

## Data Structure
The Retail Store Inventory Forecasting Dataset consists of 15 columns: Date, Store_ID, Product_ID, Category, Region, Inventory_Level, Units_Sold, Units_Ordered, Demand_Forecast, Price, Discount, Weather Condition, Holiday/Promotion, Competitor_Pricing, Seasonality with a total row counts of 73,100 rows.

Source: [Kaggle](https://www.kaggle.com/datasets/anirudhchauhan/retail-store-inventory-forecasting-dataset)

*P.S:* After data cleaning, validation and analysis, three(3) more columns were added to the data. Stock_Gap, Stockout_Risks and Price_Difference were the new columns added.

You can see the project report [here]().

## Business Impact

### Weather Impact Analysis:

- Weather variability significantly did not necessarily impacts demand and must be included in inventory planning
- Since sales don't drop during "Snowy" or "Rainy" conditions, the supply chain must remain fully operational regardless of the weather.
- Unlike many retail datasets where rain or snow kills sales, this store is "weather-resilient."

### Forecast Accuracy

- Since the forecast is always higher than reality, the store is likely holding too much safety stock, which ties up cash flow in inventory that isn't moving as fast as expected. This indicates a risk of overstocking.
- There is a strong, steady correlation, but the system is consistently "over-forecasting" by a small margin.

### Holiday/Promotion Effectiveness

- This is a huge finding, because their promotions were ineffective at driving extra volume.
- The store were likely losing profit margin by offering discounts that aren't actually bringing in more customers.

### Regional Inventory Distribution

- Inventory is perfectly balanced across the four regions showing incredible operational consistency, with each holding almost exactly 25%.
- This suggests a very centralized and efficient distribution strategy. No single region is being neglected, and no single region is being overloaded.

## Recommendation

Based on business impacts:

- Re-evaluate the type of promotions being used. If "Yes" (Promotion) results in lower total units than "No", then the current marketing strategy is cannibalizing full-price sales without expanding the customer base.


















