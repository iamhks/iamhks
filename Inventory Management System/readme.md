# Inventory Management System

The aim of the project was to make a Database for Chain Of Stores to manage their Inventory by tracking the Items present and maintaining the transactions for all the items between warehouses to branch and warehouse to warehouse. 

# Assumptions

### Main Inventory 
From Here one can access the data from all the warehouses and have he count of all the items present
### Warehouse 
Each warehouse contains some specific products in some specific Quantity which can be ordered by customer 
### Customers 
They visit any of the warehouse and orders the items for desired quantity if they are present in the warehouse then the transaction is complete 
### Items
 This contains all the list of item and cost of item we can import the products if required some products might get expired which will have to be sent back to the imported company
### Orders 
Orders are placed to company for receiving the items, which are further processed 
### Transaction 
This contains all the details regarding the transactions which took place either through Cash , Card
### Products 
This contains all the items along with the quantity which are imported, Expiry date and the date of order are also mentioned 
### E-items
These are the items which are expired and returned back to the company
### Employee
This contains the details of employees working in warehouses along with the manager details
### Supplier
This contains the details of the supplier who is supplying the items to the warehouse

## Flow of Process 
The items are distributed to various Branches by various Warehouses,Main Inventory of Each branch is managed by a manager, the items are ordered by customers, they are imported and if any product is expired they are returned back to the company , If an order is valid the transaction is carried out by either cash or Card.

## ER Diagram

![ER Diagram](https://github.com/iamhks/projects/blob/master/Inventory%20Management%20System/ER.jpg)
![Schema](https://github.com/iamhks/projects/blob/master/Inventory%20Management%20System/Schema.jpg)
![Entities@Attributes](https://github.com/iamhks/projects/blob/master/Inventory%20Management%20System/Entity%26Attributes.jpg)

## CREATION AND INSERTION OF TABLES MENTIONED ABOVE

create table PRODUCTS(
ITEMID VARCHAR(10),
Itname VARCHAR(20),
Company VARCHAR(20),
costT INTEGER,
warehousenum VARCHAR(10),
PRIMARY KEY (ITEMID));
create table warehouse(
Itemid VARCHAR(10),
quantity INTEGER,
expirydate DATE,
status VARCHAR(10),
warehousenum VARCHAR(10),
PRIMARY KEY (itemid);
CREATE TABLE Maininventory(
Managerid VARCHAR(10),
mfirstname VARCHAR(20),
mlastname VARCHAR(20),
memailid VARCHAR(20),
warehousenum VARCHAR(10),
PRIMARY KEY (MANAGERID));
CREATE TABLE EMPLOYEE(
empid VARCHAR(10),
efirstname VARCHAR(20),
elastname VARCHAR(20),
eemailid VARCHAR(20),
warehousenum VARCHAR(10),
managerid VARCHAR(10),
PRIMARY KEY (empid),
FOREIGN KEY (Managerid) REFERENCES Maininventory(Managerid));
CREATE TABLE IMPORTEDBY(
supplierid VARCHAR(10),
sname VARCHAR(20),
PRIMARY KEY (supplierid));
CREATE TABLE SUPPLIER(
supplierid VARCHAR(10),
sphonenumber VARCHAR(10),
FOREIGN KEY (supplierid) REFERENCES IMPORTEDBY(supplierid));
CREATE TABLE IMPORTED(
Itemid VARCHAR(10),
quantity INTEGER,
expirydate DATE,
supplierid VARCHAR(10),
FOREIGN KEY (supplierid) REFERENCES IMPORTEDBY(supplierid),
FOREIGN KEY (ITEMID) REFERENCES PRODUCTS(ITEMID));
CREATE TABLE VISITEDBY(
customerid VARCHAR(10),
CName  VARCHAR(20),
cemailid VARCHAR(20),
PRIMARY KEY (customerid));
CREATE TABLE CUSTOMER(
customerid VARCHAR(10),
cphonenumber VARCHAR(10),
FOREIGN KEY (customerid) REFERENCES VISITEDBY(customerid));
CREATE TABLE ORDERER(
orderid  VARCHAR(10),
datee  date,        
customerid VARCHAR(10),
status VARCHAR(10),
PRIMARY KEY (ORDERID),
FOREIGN KEY (customerid) REFERENCES VISITEDBY(customerid));
CREATE TABLE ITEMSORDERED(
orderid  VARCHAR(10),
quantity INTEGER,
itemid   VARCHAR(10),
PRIMARY KEY (ORDERID),
FOREIGN KEY (ITEMID) REFERENCES PRODUCTS(ITEMID),
FOREIGN KEY (orderid) REFERENCES ORDERER(orderid));
CREATE TABLE TRANSACTIONS(
orderid  VARCHAR(10),
totalprice INTEGER,
discountPERCENTAGE INTEGER,
grossprice INTEGER,
PAYMENTtype VARCHAR(10),
PRIMARY KEY (ORDERID),
FOREIGN KEY (orderid) REFERENCES ORDERER(orderid));
CREATE TABLE CARD(
orderid  VARCHAR(10),
Cvv INTEGER,
Cardname VARCHAR(20),
Cardnumber INTEGER,
cexpirydate INTEGER,
PRIMARY KEY (ORDERID),
FOREIGN KEY (orderid) REFERENCES ORDERER(orderid));
create table eitems(
supplierid VARCHAR(10),
itemid   VARCHAR(10),
quantity integer,
FOREIGN KEY (ITEMID) REFERENCES PRODUCTS(ITEMID),
FOREIGN KEY (supplierid) REFERENCES IMPORTEDBY(supplierid));

## Output
![Output-1](https://github.com/iamhks/projects/blob/master/Inventory%20Management%20System/Output%201.jpg)
![Output-2](https://github.com/iamhks/projects/blob/master/Inventory%20Management%20System/Output%202.jpg)

## Values
### RODUCTS
```
INSERT INTO products VALUES(1,"Bread","Thomas",10,10);
INSERT INTO products VALUES(2,"Noodles","Thomas",200,11);
INSERT INTO products VALUES(3,"Soup","Henry",70,10);
INSERT INTO products VALUES(4,"Steak","Henry",80,10);
INSERT INTO products VALUES(5,"Cheese","George",30,12);
INSERT INTO products VALUES(6,"Butter","George",50,12);
```
### WAREHOUSE
```
INSERT INTO warehouse VALUES(1,1000,2020-03-20,"NO",10);
INSERT INTO warehouse VALUES(2,1500,2020-04-20,"NO",11);
INSERT INTO warehouse VALUES(3,2000,2020-03-25,"NO",11);
INSERT INTO warehouse VALUES(4,500,2020-04-20,"NO",10);
INSERT INTO warehouse VALUES(5,1000,2020-03-25,"NO",12);
INSERT INTO warehouse VALUES(6,1000,2020-03-24,"NO",12);
```
### Main Inventory
```
INSERT INTO maininventory VALUES('A1','Ganesh','Gola',"ganesh@mmail.com",10);
INSERT INTO maininventory VALUES('A2','Chandro','Goli',"Chandro@mmail.com",11);
INSERT INTO maininventory VALUES('A3','Ramesh','Garatla',"Ramesh@mmail.com",12);
```
### Employee
```
INSERT INTO employee VALUES('B1','Ramesh','Kande',"Ramesh@email.com",10,'A1');
INSERT INTO employee VALUES('B2','Suresh','Sama','Suresh@email.com',10,'A1');
INSERT INTO employee VALUES('B3','Ganesh','Konda','Ganesh@email.com',11,'A2');
INSERT INTO employee VALUES('B4','Rajesh','Kande','Rajesh@email.com',11,'A2');
INSERT INTO employee VALUES('B5','Ravi','Sama','Ravi@email.com',12,'A3');
INSERT INTO employee VALUES('B6','Satish','Gogla','Satish@email.com',12,'A3');
```
### Importedby
```
INSERT INTO importedby values('C1','Sai Baba');
INSERT INTO importedby values('C2','Laxmi');
INSERT INTO importedby values('C3','Maha Laxmi');
```
### Supplier
```
INSERT INTO supplier VALUES('C1',9101112567);
INSERT INTO supplier VALUES('C2',9010125341);
INSERT INTO supplier VALUES('C3',9384512345);
```
### Imported
```
INSERT INTO imported VALUES(1,500,2020-04-20,'C1');
INSERT INTO imported VALUES(2,750,2020-04-20,'C1');
INSERT INTO imported VALUES(3,1000,2020-03-25,'C2');
INSERT INTO imported VALUES(4,250,2020-04-20,'C2');
INSERT INTO imported VALUES(5,500,2020-03-25,'C3');
INSERT INTO imported VALUES(6,500,2020-03-24,'C3');
```
### Visitedby
```
INSERT INTO visitedby VALUES('D1','John','John@Dmail.com');
INSERT INTO visitedby VALUES('D2','George','George@Dmail.com');
INSERT INTO visitedby VALUES('D3','Seinfeld','Seinfeld@Dmail.com');
INSERT INTO visitedby VALUES('D4','Kramer','Kramer@Dmail.com');
INSERT INTO visitedby VALUES('D5','Sheldon','Sheldon@Dmail.com');
INSERT INTO visitedby VALUES('D6','Leonard','Leonard@Dmail.com');
```
### Customer
```
INSERT INTO customer VALUES('D1',9000054321);
INSERT INTO customer VALUES('D2',9000054322);
INSERT INTO customer VALUES('D3',9000054323);
INSERT INTO customer VALUES('D4',9000054324);
INSERT INTO customer VALUES('D5',9000054325);
INSERT INTO customer VALUES('D6',9000054326);
```
### Itemsordered
```
INSERT INTO itemsordered VALUES('O1',10,1);
INSERT INTO itemsordered VALUES('O2',11,2);
INSERT INTO itemsordered VALUES('O3',12,3);
INSERT INTO itemsordered VALUES('O4',13,4);
INSERT INTO itemsordered VALUES('O5',14,5);
INSERT INTO itemsordered VALUES('O6',15,6);
```
### Orderer
```
INSERT INTO orderer VALUES('O1',2020-02-28,'D1',"YES");
INSERT INTO orderer VALUES('O2',2020-02-29,'D2',"YES");
INSERT INTO orderer VALUES('O3',2020-02-27,'D3',"YES");
INSERT INTO orderer VALUES('O4',2020-02-27,'D4',"YES");
INSERT INTO orderer VALUES('O5',2020-02-26,'D4',"YES");
INSERT INTO orderer VALUES('O6',2020-02-26,'D5',"YES");
```
### Transactions
```
INSERT INTO transactions VALUES('O1',100,0,100,"Cash");
INSERT INTO transactions VALUES('O2',2200,5,2090,"Cash");
INSERT INTO transactions VALUES('O3',840,2,823,"Cash");
INSERT INTO transactions VALUES('O4',960,2,940,"Card");
INSERT INTO transactions VALUES('O5',420,1,415,"Card");
INSERT INTO transactions VALUES('O6',750,2,735,"Card");
```
### Card
```
INSERT INTO card VALUES('O4',211,'John',04005684,721);
INSERT INTO card VALUES('O5',212,'George',05005792,822);
INSERT INTO card VALUES('O6',213,'Kramer',06008943,923);
```
## Final Output 
![All the Tables in Database](https://github.com/iamhks/projects/blob/master/Inventory%20Management%20System/Output%203.jpg)
