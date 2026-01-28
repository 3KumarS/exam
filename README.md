Practical No. 1
Aim: Implementation of Data partitioning through Range

CREATE DATABASE mca;
USE mca;

CREATE TABLE tr (
id INT, name VARCHAR(50), purchased DATE
)
PARTITION BY RANGE( YEAR(purchased) ) (
PARTITION p0 VALUES LESS THAN (1990), PARTITION p1 VALUES LESS THAN (1995), PARTITION p2 VALUES LESS THAN (2000), PARTITION p3 VALUES LESS THAN (2005), PARTITION p4 VALUES LESS THAN (2010), PARTITION p5 VALUES LESS THAN (2015)
);
INSERT INTO tr VALUES
(1, 'desk organiser', '2003-10-15'), (2, 'alarm clock', '1997-11-05'), (3, 'chair', '2009-03-10'), (4, 'bookcase', '1989-01-10'), (5, 'exercise bike', '2014-05-09'), (6, 'sofa', '1987-06-05'), (7, 'espresso maker', '2011-11-22'), (8, 'aquarium', '1992-08-04'), (9, 'study desk', '2006-09-16'), (10, 'lava lamp', '1998-12-25');

SELECT * FROM tr;

SELECT* FROM tr PARTITION (p2);

SELECT * FROM tr PARTITION (p5);

SELECT* FROM tr PARTITION (p4);

SELECT PARTITION_NAME, TABLE_ROWS FROM NFORMATION_SCHEMA.PARTITIONSWHERE TABLE_NAME='tr';

--------------------
Practical No. 2
Aim: Implementation of Analytical queries like Roll_UP, CUBE, First, Last.

1. ROLLUP: Aggregates data hierarchically. SELECT Region, Product, SUM(SalesAmount) AS TotalSales
FROM Sales
GROUP BY Region, Product WITH ROLLUP;

2. CUBE: Generates all possible subtotal combinations. SELECT Region, Product, SUM(SalesAmount) AS TotalSales FROMSales GROUP BYRegion, Product
UNION ALL
SELECT Region, NULL AS Product, SUM(SalesAmount) AS TotalSales FROMSales
GROUP BY Region
UNION ALL
SELECT NULL AS Region, Product, SUM(SalesAmount) AS TotalSales FROMSales
GROUP BY Product
UNION ALL
SELECT NULL AS Region, NULL AS Product, SUM(SalesAmount) AS TotalSales FROMSales;

3. FIRST_VALUE and LAST_VALUE: Retrieve the first or last value in a sorted
partition.

----------------------
Practical No. 3
Aim: Implementation of Abstract Data Type & Reference

1. Customer Table
CREATE TABLE Customer_reltab (
CustNo INT NOT NULL, CustName VARCHAR(200) NOT NULL, Street VARCHAR(200) NOT NULL, City VARCHAR(200) NOT NULL, State CHAR(2) NOT NULL, Zip VARCHAR(20) NOT NULL, Phone1 VARCHAR(20), Phone2 VARCHAR(20), Phone3 VARCHAR(20), PRIMARY KEY (CustNo)
);
2. Purchase Order Table
CREATE TABLE PurchaseOrder_reltab (
PONo INT, Custno INT, OrderDate DATE, ShipDate DATE, ToStreet VARCHAR(200), ToCity VARCHAR(200), ToState CHAR(2), ToZip VARCHAR(20), PRIMARY KEY (PONo), FOREIGN KEY (Custno) REFERENCES Customer_reltab(CustNo)
);

3. Stock Table
CREATE TABLE Stock_reltab (
StockNo INT PRIMARY KEY, Price DECIMAL(10, 2), TaxRate DECIMAL(5, 2)
);
4. Line Items Table
CREATE TABLE LineItems_reltab (
LineItemNo INT, PONo INT, StockNo INT, Quantity INT, Discount DECIMAL(5, 2), PRIMARY KEY (PONo, LineItemNo), FOREIGN KEY (PONo) REFERENCES PurchaseOrder_reltab(PONo), FOREIGN KEY (StockNo) REFERENCES Stock_reltab(StockNo)
);

------------------------
Practical No. 6
Aim: Linear Regression 

Code:
import numpy as np
class LinearRegression:
def __init__(self):
self.b0 = 0
self.b1 = 0
def fit(self, X, y):
X_mean = np.mean(X)
y_mean = np.mean(y)
numerator, denomintor = 0, 0
for i in range(len(X)):
numerator += (X[i] - X_mean) * (y[i] - y_mean)
denomintor += (X[i] - X_mean)**2
self.b1 = numerator / denomintor
self.b0 = y_mean - (X_mean * self.b1)
return self.b0, self.b1
def predict(self, X):
y_hat = self.b0 + (self.b1 * X)
return y_hat
if __name__ == '__main__':
X = np.array([173, 160, 154, 188, 168])
X = X.reshape(5, 1)
y = np.array([73, 65, 54, 80, 70])
model = LinearRegression()
b0, b1 = model.fit(X, y)
print(b0, b1)
y_pred = model.predict([165])
print(y_pred)

Output:
[-50.99209602] [0.70813817]
[65.85070258]

---------------------
Practical No. 7
Aim: Analysis of Regression

Code:
import numpy as np
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.metrics import r2_score
if __name__ == '__main__':
X = np.array([173, 160, 154, 188, 168], ndmin=2)
X = X.reshape(5, 1)
y = np.array([73, 65, 54, 80, 70])
model = LinearRegression()
model.fit(X, y)
y_hat = model.predict(X)
print(y_hat)
mse = mean_squared_error(y_true=y, y_pred=y_hat)
print(f'Loss Calculated : {mse}')
r2 = r2_score(y_true=y, y_pred=y_hat)
print(f'Goodness of Fit : {r2}')

Output:

[71.51580796 62.31081171 58.06118267 82.13788056 67.9751171 ]
Loss Calculated : 6.920550351288062
Goodness of Fit : 0.9082641788005293

----------------------
Practical No. 8
Aim: Logistic Regression

Code:
import numpy as np
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import log_loss
from sklearn.metrics import confusion_matrix, precision_score, recall_score, f1_score
if __name__ == '__main__':
# Input features (reshaped to 2D array)
X = np.array([6, 2, 5, 9, 1], ndmin=2)
X = X.reshape(5, 1)
# Target binary labels
y = np.array([1, 0, 1, 1, 0])
# Initialize and train the model
model = LogisticRegression()
model.fit(X, y)
# Predict outcomes
y_hat = model.predict(X)
print(y_hat)
# Calculate performance metrics
loss = log_loss(y_true=y, y_pred=y_hat)
print(f'Logarithimic Log : {loss}')
cm = confusion_matrix(y_true=y, y_pred=y_hat)
precision = precision_score(y_true=y, y_pred=y_hat)
recall = recall_score(y_true=y, y_pred=y_hat)
f1 = f1_score(y_true=y, y_pred=y_hat)
# Display results
print(f'Confusion Matrix : {cm}')
[1 0 1 1 0]
Logarithimic Log :
2.220446049250313e-16
Confusion Matrix : [[2 0]
[0 3]]
Precision : 1.0
Recall : 1.0
F1-Score : 1.0
print(f'Precision : {precision}')
print(f'Recall : {recall}')
print(f'F1-Score : {f1}') 

Output:

[1 0 1 1 0]
Logarithimic Log :
2.220446049250313e-16
Confusion Matrix : [[2 0]
[0 3]]
Precision : 1.0
Recall : 1.0
F1-Score : 1.0

----------------------------
Practical No. 9
Aim: SVM

Code:
from sklearn.datasets import load_iris
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.svm import SVC
from sklearn.metrics import precision_score, recall_score, f1_score
if __name__ == '__main__':
# Load the iris dataset
iris = load_iris()
X = np.array(iris.data)
y = np.array(iris.target)
# Split the dataset into training and testing sets
X_train, X_test, y_train, y_test = train_test_split(X, y, shuffle=True, test_size=0.1)
# Initialize and train the Support Vector Classifier (SVC)
model = SVC()
model.fit(X_train, y_train)
# Predict labels for the test set
y_hat = model.predict(X_test)
# Calculate performance metrics using micro-averaging
precision = precision_score(y_true=y_test, y_pred=y_hat, average='micro')
recall = recall_score(y_true=y_test, y_pred=y_hat, average='micro')
f1 = f1_score(y_true=y_test, y_pred=y_hat, average='micro')
# Print the results
print(f'Precision : {precision}')
print(f'Recall : {recall}')
print(f'F1-Score : {f1}')

Output:

Precision : 0.9333333333333333
Recall : 0.9333333333333333
F1-Score : 0.9333333333333333

----------------------
Practical No. 10
Aim: Varied Algorithms

Code:
from sklearn.datasets import load_iris
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier
from sklearn.ensemble import RandomForestClassifier
from sklearn.neighbors import KNeighborsClassifier
from sklearn.naive_bayes import GaussianNB
if __name__ == '__main__':
# Load the iris dataset
iris = load_iris()
X = np.array(iris.data)
y = np.array(iris.target)
# Split the dataset into training and testing sets
X_train, X_test, y_train, y_test = train_test_split(X, y, shuffle=True, test_size=0.1)
# 1. Decision Tree Classifier
dt = DecisionTreeClassifier()
dt.fit(X_train, y_train)
dt_pred = dt.predict([[1, 2, 3, 4]])
print(f'Decision Tree : {dt_pred}')
# 2. Random Forest Classifier
rf = RandomForestClassifier()
rf.fit(X_train, y_train)
rf_pred = rf.predict([[1, 2, 3, 4]])
print(f'Random Forest : {rf_pred}')
# 3. K-Neighbors Classifier
knn = KNeighborsClassifier()
knn.fit(X_train, y_train)
knn_pred = knn.predict([[1, 2, 3, 4]])
print(f'KNN : {knn_pred}')
# 4. Naive Bayes (GaussianNB)
nb = GaussianNB()
nb.fit(X_train, y_train)
nb_pred = nb.predict([[1, 2, 3, 4]])
print(f'Naive Bayes : {nb_pred}') 

Output:

Decision Tree : [2]
Random Forest : [2]
KNN : [1]
Naive Bayes : [2]

-----------------------------------------------------


1 >> Implementation of Data Partitioning through Range

-- Step 1: Create Database
CREATE DATABASE mca_db;
USE mca_db;

-- Step 2: Create table with RANGE partition
CREATE TABLE student (
    roll_no INT NOT NULL,
    name VARCHAR(50),
    marks INT
)
PARTITION BY RANGE (roll_no) (
    PARTITION p1 VALUES LESS THAN (101),
    PARTITION p2 VALUES LESS THAN (201),
    PARTITION p3 VALUES LESS THAN (301)
);

-- Step 3: Insert data
INSERT INTO student VALUES (10, 'Amit', 78);
INSERT INTO student VALUES (120, 'Ravi', 85);
INSERT INTO student VALUES (250, 'Neha', 92);

-- Step 4: View data
SELECT * FROM student;

o/p

	roll_no	name	marks
	10	Amit	78
	120	Ravi	85
	250	Neha	92


[SELECT
    PARTITION_NAME,
    TABLE_ROWS
FROM
    INFORMATION_SCHEMA.PARTITIONS
WHERE
    TABLE_NAME = 'student';]

    --------------------------

2 >> Implementation of Analytical queries like Roll_UP, CUBE, First, Last


-- Step 1: Create Database
CREATE DATABASE olap_db;
USE olap_db;

-- Step 2: Create Table
CREATE TABLE sales (
    region VARCHAR(20),
    product VARCHAR(20),
    amount INT
);

-- Step 3: Insert Data
INSERT INTO sales VALUES
('North', 'Laptop', 50000),
('North', 'Mobile', 20000),
('South', 'Laptop', 45000),
('South', 'Mobile', 25000),
('East',  'Laptop', 40000),
('East',  'Mobile', 15000);


-- Step 3: Check Table
SELECT * FROM sales;


--ROLLUP (Analytical Query)
code :
SELECT
    region,
    product,
    SUM(amount) AS total_sales
FROM sales
GROUP BY region, product WITH ROLLUP;

--CUBE (Analytical Query)
code:
SELECT
    region,
    product,
    SUM(amount) AS total_sales
FROM sales
GROUP BY CUBE (region, product);

--FIRST_VALUE (Analytical Function)
code:
SELECT
    region,
    product,
    amount,
    FIRST_VALUE(amount)
    OVER (PARTITION BY region ORDER BY amount) AS first_sale
FROM sales;

--LAST_VALUE
SELECT
    region,
    product,
    amount,
    LAST_VALUE(amount)
    OVER (
        PARTITION BY region
        ORDER BY amount
        ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
    ) AS last_sale
FROM sales;



-----------------------------------