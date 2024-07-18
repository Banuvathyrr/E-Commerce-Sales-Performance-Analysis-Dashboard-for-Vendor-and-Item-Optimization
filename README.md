
<h1 align="center">ECommerce Company Sales Performance Analysis</h1>


### Introduction 
ABC is an ecommerce company that sells over 25,000 items online. These items are sold by different vendors from across the country. Currently there is no dashboard available to help the Sales team monitor the performance of various vendors or items. Also, they need a ranking / categorization of the products to identify the products they need to keep an eye on.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Project Overview
This dashboard will enable the Sales team to monitor the performance of both vendors and products effectively. It will provide insights into sales metrics, highlight top-performing vendors and items, and offer a ranking/categorization system to identify products requiring attention. This initiative aims to optimize inventory management and drive strategic decisions for improved sales outcomes.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Data Sources
The dataset contains 3 excel files:
1. Sales
2. Item-Vendor
3. Vendor-Manager
   
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Tools
- PowerBi -Data Cleaning, Data analysis and creating dashboards
- Powerpoint - Creating video presentation

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Data Cleaning/Preparation
- Column names renamed.  
- Checked datatype of each column and changed it if there is any mismatch.  
- Rows having errors and empty values were checked and removed.
- New columns such as Sales, VendorName and Manager were created in Sales table for better analysis of the data.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
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

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Following Calculated Columns, Measures and tables were created
 - **Calculated columns added in Sales table**
   1) VendorName  
      ![image](https://github.com/user-attachments/assets/8f321f3d-39b0-4d56-aa3d-7b7512d7ea6a)  

   3) Manager  
      ![image](https://github.com/user-attachments/assets/7f7239cf-52d1-486b-9988-e93604c8093e)  

   5) Order Month  
      ![image](https://github.com/user-attachments/assets/f895008d-7a52-4318-8d47-562c948abe52)  

      
 - **Tables**
   1) PeriodSelection  
      ![image](https://github.com/user-attachments/assets/2487cef6-03d6-4a96-b1ff-1b3defa53f3a)
   2) MASales  
      ![image](https://github.com/user-attachments/assets/ba3ff9f3-ac09-4759-ba42-057a49939229)
   3) Total Sales per Item  
      ![image](https://github.com/user-attachments/assets/9cd54ca6-bc3f-4c6d-a4e9-9c97eafb7819)  
   4) Ranked Items    
      ![image](https://github.com/user-attachments/assets/e4bc5025-034b-4c35-be2d-52869b4ba178)    
   5) Second best selling item  
      ![image](https://github.com/user-attachments/assets/a471c516-dce9-4c6a-918d-88454071e80a)
   6) Total quantity sold per item  
      ![image](https://github.com/user-attachments/assets/9db85c3a-f04b-4d1c-8161-5254ddf047d4)
   7) Select Items  
      ![image](https://github.com/user-attachments/assets/a479ee10-3611-4ad8-8aa4-7ee9d890dfe4)

        
 - **Measures created in Sales table**
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
   6) Average sales amount  
      ```Average sales amount = AVERAGE(Sales[Sales])```
   7) SelectPeriodsales (Last 7, 14 and 28 days sales)  
        ![image](https://github.com/user-attachments/assets/22453726-846b-4c95-b3fb-3c6811b321cf)
   8) MASelecsales (14 days moving average, latest 3 months sales  
      ![image](https://github.com/user-attachments/assets/7ea59026-b758-4b9e-9eb0-6f08dfd3e342)  
      ![image](https://github.com/user-attachments/assets/ee6880a2-3491-4e19-86c9-35c99e54dc50)
   9) Total items by each manager  
      ![image](https://github.com/user-attachments/assets/85dbcbcc-7f86-428e-b4ed-2ca99d111f8a)  

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Exploratory Data Analysis

I have added 3 important pages.  
1) Sales performance tracking
2) Vendor performance analysis
3) Manager level analysis  

Additional information will be available in Top 10 vendor, Manager and vendor info pages.  

**Sales Performance**   
a) In sales performance report page, 4 cards were inserted to show Total sales, Total quantity sold, Average sales amount and Total orders.  
b) A **line chart** with total sales over Order month shown in the left of the report.  
c) Two Period selector slicer has been created. One for showing **14 days Moving average and latest 3 months sales over order date** (line plot)  
d) Second Period selector slicer helps to view the **last 7, 14 and 28 days sales amount**  (line plot)  
e) Page navigator icons (buttons with image) added at the left of the report page to help for navigation to other pages  

**Vendor Performance**    
a) In Vendor performance report page, total no. of vendors card was added along with other cards.   
b) Two **slicers** were added: Vendor and Manager. To choose vendor or manager based on the need.  
c) **Pie chart** added to display the top 10 vendors based on the sales.  
d) **Horizontal bar chart** added to display the total quantity sold by each vendor with the vendor having maximum sales in the top.  
e) Total orders by order month have been shown as **vertical bar chart** with the month having higher orders in the beginning and lower orders at the end.  
f) Vendors with second best selling item has been shown with the Item ID in a table visual  

**Manager level analysis**   
a) A **funnel chart** has been used to show total sales by manager  
b) Total number of managers in the company is shown as card visual on top of the report.  
c) **Tree map** shown to display the total quantity sold under each manager.  
d) Count of distinct items, sales amount, count of vendor name with respect to each manager has been listed in the form of **tabular visual**  
e) Table with manager on each row is provided with **drill through** option to see the details about the selected manager in the table of Manager report.



----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Results/ Findings
**Sales Trends**:  
- Total sales amount saw a significant increase in March, reaching its peak towards the end of the month. After this peak, sales began to gradually decline.    

**Top Vendors by Sales Amount**:  
- Onus Global Fulfillment: Contributed approximately 10% of the total sales amount.  
- Liola Home: Contributed approximately 7% of the total sales amount.  
- South Store: Contributed approximately 6.1% of the total sales amount.  

**Quantity Sold**:  
- The total quantity sold by Onus Global Fulfillment was 61,931 units, making up approximately 10% of the overall quantity sold. This was followed by OJCommerce, South Store, and Fulfillment Concepts in terms of quantity sold.

**Order Volume by Month**:   
- The highest number of orders was recorded in March, followed by April, May, and January.

**Total Sales by Manager**:  
Manager A: Highest sales amount of $41.81M, managing 179 vendors and 29,199 distinct items.  
Manager M: Total sales of 80.20K, managing 98 vendors and 7,770 distinct items.  
Manager J: Total sales of 2.10M, managing 29 vendors and 4,707 distinct items.  
Manager V: Total sales of 2.40M, managing 46 vendors and 4,571 distinct items.  
Manager N: Total sales of 153.04K, managing 61 vendors and 859 distinct items.  
Manager X: Total sales of 80.20K, managing 9 vendor and 294 distinct items.    

**Linear Trend Analysis**:  
There is a clear linear trend between the **count** of distinct **items**(item_id) and **total sales**, indicating that increasing the number of items significantly boosts total sales.
In contrast, the count of vendors does not exhibit a linear trend with total sales, suggesting that simply increasing the number of vendors does not lead to a significant rise in sales

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Recommendation  
1) **Focus on March Sales Peaks**:  
- Promotional Campaigns: Since March saw a significant increase in sales, consider running targeted promotional campaigns during this month to capitalize on the trend.  
- Stock Management: Ensure that inventory levels are adequate to meet the expected increase in demand in March.  

2) **Leverage Top Vendors**:  
- Partnership Development: Strengthen relationships with top vendors like Onus Global Fulfillment, Liola Home, and South Store to maintain and potentially increase their contribution to overall sales.  
- Vendor Incentives : Provide incentives or support to these vendors to encourage the introduction of new items or exclusive deals that could drive higher sales.  

3) **Optimize Product Offerings**:
- Expand Item Range: Since there is a linear trend between the count of distinct items and total sales, increasing the variety of items offered could lead to higher sales.
- Analyze Item Performance: Regularly review the performance of distinct items and focus on promoting high-performing items while reconsidering or discontinuing low-performing ones.

4) **Monthly Sales Analysis**:
- Seasonal Adjustments: Given the high order volumes in March, April, May, and January, plan for seasonal adjustments in inventory and marketing strategies to align with these peak months.  
- Continuous Monitoring: Use historical sales data to predict future trends and adjust sales strategies accordingly.    

5) **Enhance Vendor Management**:
- Vendor Count vs. Item Count: The findings indicate that simply increasing the number of vendors does not significantly impact sales. Focus on increasing the count of distinct items from each vendor instead.  
- Performance Benchmarks: Establish performance benchmarks for vendors based on sales, item count, and other relevant metrics to ensure consistent performance across the board.  

6) **Sales and Item Correlation**:
- Data-Driven Decisions: Utilize the clear correlation between item count and sales to make data-driven decisions on inventory management and product offerings.    
- Predictive Analytics: Implement predictive analytics tools to forecast the impact of adding new items on overall sales and adjust strategies accordingly.    

**Example Action Plan**  
-  March Promotions: Launch a "Spring Sale" campaign every March, featuring discounts and special offers on popular items.  
-  Vendor Partnerships: Schedule quarterly meetings with top vendors to discuss performance, introduce new products, and negotiate better terms.  
-  Inventory Expansion: Conduct market research to identify new product categories that could be introduced to increase item variety and boost sales.  
-  Performance Dashboards: Develop and regularly update Power BI dashboards that provide real-time insights into vendor and item performance for the sales team.  
-  Training: Train the sales team on using data analytics tools to monitor performance and make informed decisions.    

By implementing these recommendations, the sales team at ABC eCommerce can effectively monitor and improve the performance of various vendors and items, ultimately driving higher sales and better customer satisfaction.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Dashboard 
- Check the dashboard here:


 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Video Presentation link:
- 

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Acknowledgements
- 














