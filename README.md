
<h1 align="center">ECommerce Company Sales Performance Analysis</h1>


### Introduction  
ABC is an ecommerce company that sells over 25,000 items online. These items are sold by different vendors from across the country. Currently there is no dashboard available to help the Sales team monitor the performance of various vendors or items. Also, they need a ranking / categorization of the products to identify the products they need to keep an eye on.

### Project Overview
This dashboard will enable the Sales team to monitor the performance of both vendors and products effectively. It will provide insights into sales metrics, highlight top-performing vendors and items, and offer a ranking/categorization system to identify products requiring attention. This initiative aims to optimize inventory management and drive strategic decisions for improved sales outcomes.

### Data Sources
The dataset contains 3 CSV files:
1. Sales
2. Item-Vendor
3. Vendor-Manager

### Tools
- PowerBi -Data Cleaning, Data analysis and creating dashboards
- Powerpoint - Creating video presentation

### Data Cleaning/Preparation
- Column names renamed.  
- Checked datatype of each column and changed it if there is any mismatch.  
- Rows having errors and empty values were checked and removed.
- New columns such as Sales, VendorName and Manager were created in Sales table for better analysis of the data.

### Data Modelling
To resolve the ambiguity caused by many-to-many relationships between the Sales table and ItemVendor table, and between the ItemVendor table and VendorManager table, 
two bridge tables were created: BridgeItem and BridgeVendor. This approach transformed the many-to-many relationships into one-to-many relationships, ensuring clearer 
and more accurate data connections.
<p align="center">
  <img src="https://github.com/user-attachments/assets/74cd5132-ba46-43b0-8f4f-f5b77446b316" alt="Data Model">
</p>  

- Sales[item_id] connected to BridgeItemId[item_id] (many-to-one) 
- BridgeItemId[item_id] connected to ItemVendor[item_id] (one-to-many)  
- ItemVendor[vendor] connected to BridgeVendor[vendor] (many-to-one)  
- BridgeVendor[vendor] connected to VendorManager[vendor] (one-to-many)

Note: BridgeItemId table should contain distinct rows of Item_ID and BridgeVendor table should contain distinct rows of Vendors

### Exploratory Data Analysis


### Following Measures, Calculated Columns and tables were created
 - Calculated columns added in Sales table  
   1) VendorName
   2) Manager
   3) Order Month
 - Tables
   1) PeriodSelection  
      ![image](https://github.com/user-attachments/assets/2487cef6-03d6-4a96-b1ff-1b3defa53f3a)
   2) 

  
 - Measures created in Sales table
   1) Total Sales   
      ```TotalSales = SUM(Sales[Sales])```  
   2) Total No. of Vendors  
      ```Total No Of Vendors = DISTINCTCOUNT(Sales[VendorName])```
   3) Total Quantity Sold  
      ```Total Quantity = SUM(Sales[Quantity])```
   4) Total Orders  
      ```Total Orders = SUM(Sales[Order_ID])```
   5) Total no. of Managers  
      ```Total Managers = DISTINCTCOUNT(Sales[Manager])```  

### Data Analysis
```
1. SELECT 
	  store_id,Incremental_Revenue
  FROM
	  fact_events
  ORDER BY 
	  Incremental_Revenue DESC
  LIMIT 10;
```

```
2. WITH CTE_rank as
(
SELECT 
	dp.category as Category_name, 
	AVG(fe.Incremental_Sold_Units_Percentage) as ISU_perc
FROM
	fact_events fe
INNER JOIN
	dim_products dp ON fe.product_code = dp.product_code
INNER JOIN
	dim_campaigns dc ON fe.campaign_id = fe.campaign_id
WHERE 
	dc.campaign_name ='Diwali'
GROUP BY 
	dp.category
)
SELECT
	Category_name,
	ISU_perc,
    RANK() OVER (ORDER BY ISU_perc DESC) as rankn
FROM CTE_rank;

```
```
3. SELECT
	*,
	CASE 
		WHEN promo_type = '50% OFF' THEN base_price* 0.50
        WHEN promo_type = '25% OFF' THEN base_price* 0.75
        WHEN promo_type = '33% OFF' THEN base_price* 0.67
        WHEN promo_type = '500 Cashback' THEN base_price - 500
        ELSE base_price
	END AS base_price_after_promo
FROM 
	fact_events;
```

### Results/ Findings
- During the **Diwali campaign**, the **500 cashback** promotional offer resulted in significant **revenue**. Conversely, during the **Sankranti campaign**, the **BOGOF promotion** demonstrated notable success.
- In the case of the BOGOF promotion, it was observed that as the incremental units sold increased, the corresponding incremental revenue did not exhibit a proportional increase. 
- Instead, the relationship between incremental sold units and incremental revenue appeared to follow a linear trend with a lesser slope. 
- This suggests that while sales volume increased, the generated revenue did not rise at an equivalent rate, indicating potential factors, such as the type of product, promo-type influencing revenue generation beyond solely increasing sales volume.
- Although the product category remained the same (Combo) for both the Diwali and Sankranti campaigns in the case of the 500 cashback promotion, **the total revenue yielded during the Diwali campaign was significantly higher compared to the Sankranti campaign**. 
- This disparity may be attributed to the **timing** of the campaigns, as the Diwali campaign preceded the Sankranti campaign, allowing consumers to utilize the cashback promotion for purchasing combo sets during the Diwali campaign itself.
- During the **Sankranti campaign**, there was a **surge in purchases of groceries, home appliances, and home care products, resulting in increased quantity sold**. However, this did not translate into significantly higher revenue, as these product categories typically do not yield substantial revenue.

### Recommendation
- **Store Expansion Strategy**: Implementing a store expansion strategy by adding number of stores in each city can significantly enhance revenue generation. 
- **Streamlining Promotional Strategies**: To optimize our campaign strategy and maximize revenue potential, we propose removing the 25% off, 33% off, and 50% off promotions for both campaigns. Our analysis demonstrates that these promotions have shown to be less effective compared to the Cashback and BOGOF promotions. By reallocating resources to focus on the more successful promotions, we aim to drive greater impact and ensure the highest possible return on investment.
- **Strategic Expansion of BOGOF Promotion**: For the Diwali campaign, we propose extending the BOGOF (Buy One, Get One Free) promotion strategy to include groceries. This strategic adjustment aims to capitalize on the high demand for groceries during the festive period. 
- **Introducing 500 Cashback Offer**: During the Sankranti campaign, we propose introducing the 500 cashback promotional offer to a new set of product categories, apart from combo sets. Recognizing that customers may have already purchased combo sets during the Diwali campaign, this strategic adjustment aims to maintain consumer interest and incentivize purchases in different product categories.

### Dashboard 
- Check the dashboard here: https://www.novypro.com/project/retail-mart-promotion-analysis-power-bi

### Video Presentation link:
- Check for the presentation in google drive: https://drive.google.com/drive/folders/1F1y6BL5GIRh6MmGLdEedMCvBPxGwC36f

### Acknowledgements
- This Project is a Codebasics Resume project challenge#9 (https://codebasics.io/challenge/codebasics-resume-project-challenge)














