# SQL---Practice-using-AdventureWorksDW
Identify customers who consistently make purchases above the average order value.
WITH cte_sales AS (
SELECT
D.FirstName + ' ' + D.LastName AS FullName,
SalesAmount
FROM FactInternetSales F
JOIN DimCustomer D ON F.CustomerKey = D.CustomerKey
WHERE SalesAmount > (
SELECT AVG(SalesAmount)
FROM FactInternetSales
)
)
SELECT
FullName,
COUNT(*) AS OrdersAboveAvg
FROM cte_sales
GROUP BY FullName
ORDER BY OrdersAboveAvg DESC;
