
<h1 align="center">ECommerce Company Sales Performance Analysis</h1>


### Introduction  
ABC is an ecommerce company that sells over 25,000 items online. These items are sold by different vendors from across the country. Currently there is no dashboard available to help the Sales team monitor the performance of various vendors or items. Also, they need a ranking / categorization of the products to identify the products they need to keep an eye on.

### Project Overview
This dashboard will enable the Sales team to monitor the performance of both vendors and products effectively. It will provide insights into sales metrics, highlight top-performing vendors and items, and offer a ranking/categorization system to identify products requiring attention. This initiative aims to optimize inventory management and drive strategic decisions for improved sales outcomes.

### Data Sources
The dataset contains 3 excel files:
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
e) 


### Results/ Findings


### Recommendation


### Dashboard 
- Check the dashboard here: 

### Video Presentation link:
- 

### Acknowledgements
- 














