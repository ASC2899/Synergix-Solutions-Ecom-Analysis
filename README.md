# 📦 Synergix Solutions Ecom Analysis

Synergix Solutions is a multinational consumer goods e-commerce company that sells a wide range of consumer products. With a strong presence in the market, the company continually strives to enhance its market share, drive revenue growth, and strengthen its brand equity. The Company's e-commerce portal was launched two years ago, and it has been successful in attracting customers from various parts of the world.

However, in the recent past, the sales have not been increasing as predicted, and the management is concerned about the future of the business. They have tried various strategies such as discounts, promotions, and ads but these have not yielded desired results. The management believes that there may be underlying issues that need to be addressed to improve sales performance.

## 🧾 Dataset Overview

The dataset provided by Synergix Solutions includes the following key components:

- **POS Data**: Sales transaction details such as SKU ID, revenue, quantity sold, price per unit, and product attributes like brand, category, and manufacturer.

- **Online**: Online advertising metrics including impressions, clicks, cost, and campaign information linked to each SKU.

- **Offline**: Traditional media performance data for video and image campaigns, covering impressions, clicks, and costs by brand.

- **Product Attributes**: Granular product-level metadata including star ratings, content availability (videos, images, descriptions), and product availability status.

- **Vendor-Powered Coupons (VPC)**: Data on promotional campaigns funded by vendors — including units sold using coupons and promotional spend.

- **Search Rank**: Organic search visibility data showing how often products are searched and their median search ranking.

👉 [View Full Data Dictionary](Synergix-Solutions-Ecom-Analysis/Data/Data_Dictionary.png)


## 📌 Problem Statements, Solution approach and Key Findings

❓ **Synergix has been aggressively channeling their resources into online marketing to attract more people on their ecom portal. Now after a period of rigorous marketing there is one question looming large at synergix, "_Was the online marketing investment worth it?_"**

🔍 
[Calendar Table](#-table-relation-model)
💡

## 🔗 Table Relation Model

Before proceeding with any steps in this project, it is **mandatory to create a Calendar Table** in Power BI. This table acts as a central reference for all time-based analysis and relationships across the data model.

Since multiple tables in this dataset contain date fields (e.g., POS data, media campaigns, product activity), a dedicated Calendar Table ensures:
- Consistent and accurate date filtering
- Enables Time Intelligence functions
- Simplifies relationships across fact tables

👉 **Use the following DAX formula in Power BI to create the Calendar Table:**

```
Calendar Table =
VAR StartYear = 2021
VAR EndYear = 2022
RETURN
    ADDCOLUMNS (
        CALENDAR ( DATE ( StartYear, 1, 1 ), DATE ( EndYear, 12, 31 ) ),
        "Year", YEAR ( [Date] ),
        "Month No.", MONTH ( [Date] ),
        "Day", DAY ( [Date] ),
        "Day Name", FORMAT ( [Date], "DDDD" ),
        "Day Name Short", FORMAT ( [Date], "DDD" ),
        "Month Name", FORMAT ( [Date], "MMMM" ),
        "Month Name Short", FORMAT ( [Date], "MMM" ),
        "Quarter", QUARTER ( [Date] ),
        "Quarter Name", "Q" & FORMAT ( [Date], "Q" ),
        "Week of Year", WEEKNUM ( [Date] )
    )
```
After creating the Calendar Table, you must establish relationships between the Calendar Table and every other table that contains a Date column.
Once all relationships are built correctly, your model should look similar to [this](Synergix-Solutions-Ecom-Analysis/Assets/Table_Relation_Model.png).