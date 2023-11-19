-- Table Schema: Employees
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Age INT,
    DepartmentID INT,
    Salary DECIMAL(10, 2)
);

-- Table Schema: Orders
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    OrderDate DATE,
    ShippedDate DATE,
    CustomerID INT
);
INSERT INTO Orders (OrderID,OrderDate ,ShippedDate ,CustomerID )VALUES(11,12-02-2022,21-02-2022,1234),(12,2-03-2023,21-03-2023,234);


-- Table Schema: Products
CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    Category VARCHAR(50),
    Price DECIMAL(10, 2)
);
INSERT INTO Products (ProductID,Category ,Price) VALUES (23,'Electronics',1200),(253,'Vegetables',500),(122,'Stationery',900);

-- Table Schema: Customers
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    CustomerName VARCHAR(100),
    CustomerAge INT (5)
);
INSERT INTO Customers (CustomerID ,CustomerName ,CustomerAge) VALUES (101,'Anu',20),(102,'Yash',12);
INSERT INTO Customers (CustomerID ,CustomerName ,CustomerAge) VALUES (1234,'Anuja',20),(234,'Yashraj',12);


-- Table Schema: Departments
CREATE TABLE Departments (
    DepartmentID INT PRIMARY KEY,
    DepartmentName VARCHAR(100),
    ManagerID INT
);
INSERT INTO Departments (DepartmentID ,DepartmentName,ManagerID) VALUES (1,'Shipping',101),(2,'Supplier',102),(3,'Manager',103);



-- Queries

-- 1. Insert a new employee
INSERT INTO Employees (EmployeeID, FirstName, LastName, Age, DepartmentID, Salary)
VALUES (101, 'John', 'Doe', 28, 1, 60000.00);

-- 2. Update the salary of all employees in the Sales department by 10%
UPDATE Employees
SET Salary = Salary * 1.10
WHERE DepartmentID = 2; -- Assuming Sales department has DepartmentID = 2

-- 3. Delete all orders placed before a certain date
DELETE FROM Orders
WHERE OrderDate < '2023-01-01'; -- Replace with the specific date

-- 4. Retrieve names and ages of customers who made a purchase in the last month
SELECT CustomerName, Age
FROM Customers
JOIN Orders ON Customers.CustomerID = Orders.CustomerID
WHERE OrderDate >= DATEADD(MONTH, -1, GETDATE());

-- 5. Increase the price of all products in the "Electronics" category by 5%
UPDATE Products
SET Price = Price * 1.05
WHERE Category = 'Electronics';

-- 6. Find the total number of products in each category
SELECT Category, COUNT(ProductID) AS TotalProducts
FROM Products
GROUP BY Category;

-- 7. Assign a new manager to a specific department
UPDATE Departments
SET ManagerID = 201 -- Assuming ManagerID 201 corresponds to a specific manager
WHERE DepartmentID = 3; -- Replace with the specific department

-- 8. Transfer an employee from one department to another
UPDATE Employees
SET DepartmentID = 4 -- Assuming DepartmentID 4 corresponds to the new department
WHERE EmployeeID = 102; -- Replace with the specific employee

-- 9. Mark an order as shipped and update the shipped date
UPDATE Orders
SET ShippedDate = GETDATE()
WHERE OrderID = 11; -- Replace with the specific order


-- 10. Retrieve the highest salary among all employees
SELECT MAX(Salary) FROM employees;
