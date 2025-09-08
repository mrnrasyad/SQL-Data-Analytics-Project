## Exploratory Data Analysis (EDA) using Custom SQL Queries
<details>
  <summary>Queries</summary>
  
  ```sql
--total orders by payment method
SELECT 
    pm.Name,
    COUNT(o.OrderID) AS Total
FROM [Order] o
JOIN PaymentMethod pm ON o.PaymentMethodID = pm.PaymentMethodID
GROUP BY pm.Name
ORDER BY Total DESC;

--total sales by cities
SELECT 
    c.CustomerLocation AS City,
    SUM(ol.TotalAmount) AS TotalSales
FROM OrderLine ol
JOIN [Order] o 
    ON ol.OrderID = o.OrderID
JOIN Customer c 
    ON o.CustomerID = c.CustomerID
GROUP BY c.CustomerLocation
ORDER BY TotalSales DESC;   

--total sales per category
SELECT 
    p.Category AS Category,
    SUM(ol.TotalAmount) AS TotalSales
FROM OrderLine ol
JOIN Product p 
    ON ol.ProductID = p.ProductID
GROUP BY p.Category
ORDER BY TotalSales DESC;   

--total sales per month
SELECT  
    FORMAT(o.OrderDate, 'MM') AS Month,
    SUM(ol.TotalAmount) AS Revenue
FROM OrderLine ol
JOIN [Order] o 
    ON ol.OrderID = o.OrderID
GROUP BY FORMAT(o.OrderDate, 'MM')
ORDER BY Month;

--total selling products
SELECT 
    p.ProductName AS ProductName,
    SUM(ol.TotalAmount) AS TotalSales
FROM OrderLine ol
JOIN Product p 
    ON ol.ProductID = p.ProductID
GROUP BY p.ProductName
ORDER BY TotalSales DESC;   

--total orders by status
SELECT 
    os.Name,
    COUNT(o.OrderID) AS Total
FROM [Order] o
JOIN OrderStatus os ON o.OrderStatusID = os.OrderStatusID
GROUP BY os.Name
ORDER BY Total DESC;
  ```
</details>

#### **Orders** by **Payment Method** Analysis
PayPal is the most used payment method (60 orders), followed by credit card (54) and debit card (53). Gift card (42) and Amazon Pay (41) trail behind, showing customers prefer traditional digital payments over alternative options.
<p align="center">
SQL Output: Orders by Payment Method<br>
  <kbd><img src="image/1.png" width=400px> </kbd> <br>
</p>

<br>
<p align="center">
  <kbd><img src="image/1-1.png" width=600px> </kbd> <br>
 Chart: Orders by Payment Method
</p>

**Recommendation:** Maintain strong support for PayPal and card payments, as they dominate customer preference. At the same time, consider promotions or incentives (e.g., discounts, cashback) for Gift Card and Amazon Pay to encourage broader adoption and diversify payment usage.

#### **Orders** by **Status** Analysis
Out of the total orders, 88 were completed, 85 are still pending, and 77 were cancelled. While completed orders slightly lead, the high number of pending and cancelled orders indicates potential issues in order processing or customer experience.
<p align="center">
SQL Output: Orders by Status<br>
  <kbd><img src="image/6.png" width=400px> </kbd> <br>
</p>

<br>
<p align="center">
  <kbd><img src="image/6-6.png" width=600px> </kbd> <br>
 Chart: Orders by Status
</p>

**Recommendation:** Focus on reducing pending orders by streamlining order fulfillment and improving communication with customers. Investigate cancellation reasons—such as payment failures, stock issues, or customer dissatisfaction—and address them with better inventory management, clearer checkout processes, or improved customer support.

#### **Sales** by **City** Analysis
Miami leads with the highest sales (31,700), followed by Denver (29,785) and Houston (28,390). Meanwhile, San Francisco (16,195) and Los Angeles (17,820) record the lowest sales. This indicates significant differences in city-level performance, with some markets outperforming others.
<p align="center">
SQL Output: Sales by City<br>
  <kbd><img src="image/2.png" width=400px> </kbd> <br>
</p>

<br>
<p align="center">
  <kbd><img src="image/2-2.png" width=600px> </kbd> <br>
 Chart: Sales by City
</p>

**Recommendation:** Focus on strong-performing cities like Miami and Denver with continued investment in marketing and customer engagement. For lower-performing cities such as San Francisco and Los Angeles, investigate demand gaps—consider localized promotions, partnerships, or customer experience improvements to boost sales.

#### **Sales** by **Product Category**
Electronics (129,950) and Home Appliances (105,000) dominate sales, far outperforming other categories. In contrast, Footwear (4,320), Clothing (3,540), and Books (1,035) contribute minimally, showing a highly uneven distribution of revenue across categories.
<p align="center">
SQL Output: Sales by Product Category<br>
  <kbd><img src="image/3.png" width=400px> </kbd> <br>
</p>

<br>
<p align="center">
  <kbd><img src="image/3-4.png" width=600px> </kbd> <br>
 Chart: Sales by Product Category
</p>

**Recommendation:** Sustain investment in Electronics and Home Appliances, as they are the main revenue drivers. For low-performing categories, consider whether to improve visibility (through targeted promotions, bundling, or discounts) or reduce focus if they are not strategically important. Diversification could also help reduce over-reliance on top categories.

#### **Revenue** per **Month**
Revenue was strong in February (122,695) and March (117,730) but dropped sharply in April (3,420), indicating a sudden decline in sales activity.
<p align="center">
SQL Output: Revenue per Month<br>
  <kbd><img src="image/4.png" width=400px> </kbd> <br>
</p>

<br>
<p align="center">
  <kbd><img src="image/4-4.png" width=600px> </kbd> <br>
 Chart: Revenue per Month
</p>

**Recommendation:** Investigate April’s drop — check for seasonality, data issues, or operational challenges. If seasonal, prepare targeted promotions for low months. If operational, address bottlenecks (e.g., inventory shortages or payment issues) to stabilize monthly revenue.

#### Top Selling Products
Refrigerators (78,000), laptops (58,400), and smartphones (48,500) dominate sales, while items like books (1,035) and T-shirts (1,060) contribute minimally. The product mix shows a heavy reliance on high-value electronics and appliances.
<p align="center">
SQL Output: Top Selling Products<br>
  <kbd><img src="image/5.png" width=400px> </kbd> <br>
</p>

<br>
<p align="center">
  <kbd><img src="image/5-5.png" width=600px> </kbd> <br>
 Chart: Top Selling Products
</p>

**Recommendation:** Maintain focus on high-performing electronics and appliances through promotions and inventory prioritization. For low-selling items, evaluate whether to reduce stock, bundle with popular products, or run targeted campaigns to boost demand.


## Summary
- PayPal is the most used payment method, while Gift Card and Amazon Pay are least used.
- Completed orders lead, but pending and cancelled orders are still high.
- Miami, Denver, and Houston are the top-performing cities.
- Electronics and Home Appliances dominate sales categories.
- Revenue was strong in Feb–Mar but dropped sharply in April.
- Refrigerators, laptops, and smartphones are the best-selling products.
