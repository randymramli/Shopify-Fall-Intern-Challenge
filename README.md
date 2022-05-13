# Shopify-Fall-Intern-Challenge

## Question 1:

Given some sample data, write a program to answer the following: [click here to access the required data set](https://docs.google.com/spreadsheets/d/16i38oonuX1y1g7C_UAmiK9GkY7cS-64DfiDMNiR41LM/edit#gid=0)

  On Shopify, we have exactly 100 sneaker shops, and each of these shops sells only one model of shoe. We want to do some analysis of the average order value (AOV). When we look at orders data over a 30 day window, we naively calculate an AOV of $3145.13. Given that we know these shops are selling sneakers, a relatively affordable item, something seems wrong with our analysis. 

##### 1. Think about what could be going wrong with our calculation. Think about a better way to evaluate this data. 
Answer:

The wrong answer could be attributed to the fact that the AOV simply counts the average of the 'order_amount' column.
In order to find the real average order value, we need to take into account the how many items have actually been sold in 'total_items' column.

```
test_AOV = df['order_amount'].mean()
print('The wrong average order value (AOV):', round(test_AOV, 2))
The wrong average order value (AOV): 3145.13
```

##### 2. What metric would you report for this dataset?

Answer:
In order to find the true AOV, we need to calculate the sum of 'order_amount' and then divide it by the sum of 'total_items'.
This way, we can get the real average order value.

```
order_amount = df['order_amount'].sum()
total_items = df['total_items'].sum()
print("Total order: ", order_amount)
print("Total Items: ", total_items)
Total order:  15725640
Total Items:  43936

real_AOV = order_amount/total_items
print("The actual AOV is: ", round(real_AOV,2))
The actual AOV is:  357.92
```

##### 3. What is its value?

Answer:
The correct average order vaule is 357.92.
(The total number of 'order_amount': 15725640; The total number of 'total_items': 43936)

```
print("The actual AOV is: ", round(real_AOV,2))
The actual AOV is:  357.92
```

## Question 2: 

For this question you’ll need to use SQL. [Follow this link](https://www.w3schools.com/SQL/TRYSQL.ASP?FILENAME=TRYSQL_SELECT_ALL) to access the data set required for the challenge. Please use queries to answer the following questions. Paste your queries along with your final numerical answers below.

##### 1. How many orders were shipped by Speedy Express in total?

-- Merge Employees record with order record on employee Id\n
-- Count how many times each employeeID has come up and sort it from the highest \n
-- Get only one of the employee and return the last name\n

```
SELECT LastName AS "Last Name of Employee With Most Orders"
FROM Orders JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID
GROUP BY  Employees.EmployeeID
ORDER BY COUNT(Employees.EmployeeID) DESC
LIMIT 1;
```
Answer:\
54

##### 2. What is the last name of the employee with the most orders?


-- Merge Employees record with order record on employee Id\n
-- Count how many times each employeeID has come up and sort it from the highest number\n
-- Get only one of the employee and return the last name\n

```
SELECT LastName AS "Last Name of Employee With Most Orders"
FROM Orders JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID
GROUP BY  Employees.EmployeeID
ORDER BY COUNT(Employees.EmployeeID) DESC
LIMIT 1;
```

-- Answer:\n
-- Peacock

##### 3. What product was ordered the most by customers in Germany?

-- Merge Customers, Orders, and OrderDetails with Product table using their respective IDs
-- Get only the orders with the customerID that correspond to Germany
-- Group them all based on the name of the product and sort it by how much that product has been ordered
-- Check the highest value and return the name of that product

```
SELECT Products.ProductName, SUM(OrderDetails.Quantity) AS Total_Orders, Customers.Country
FROM Products
JOIN Customers ON Customers.CustomerID = Orders.CustomerID
JOIN OrderDetails ON OrderDetails.ProductID = Products.ProductID
JOIN Orders ON Orders.OrderID = OrderDetails.OrderID
WHERE Customers.Country = "Germany"
GROUP BY Products.ProductName
ORDER BY Total_orders DESC
LIMIT 1;
```

-- Answer:
-- Boston Crab Meat