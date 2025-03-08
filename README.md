CREATE DATABASE BankManagement;
USE BankManagement;

CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY AUTO_INCREMENT,
    Name VARCHAR(100) NOT NULL,
    Email VARCHAR(100) UNIQUE NOT NULL,
    Phone VARCHAR(15) UNIQUE NOT NULL,
    Address TEXT
);

CREATE TABLE Accounts (
    AccountID INT PRIMARY KEY AUTO_INCREMENT,
    CustomerID INT,
    AccountType ENUM('Savings', 'Current') NOT NULL,
    Balance DECIMAL(10,2) DEFAULT 0.00,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID) ON DELETE CASCADE
);

CREATE TABLE Transactions (
    TransactionID INT PRIMARY KEY AUTO_INCREMENT,
    AccountID INT,
    TransactionType ENUM('Deposit', 'Withdraw', 'Transfer') NOT NULL,
    Amount DECIMAL(10,2) NOT NULL,
    TransactionDate TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (AccountID) REFERENCES Accounts(AccountID) ON DELETE CASCADE
);

INSERT INTO Customers (Name, Email, Phone, Address) 
VALUES 
('John Doe', 'john@example.com', '9876543210', '123 Main St');

INSERT INTO Accounts (CustomerID, AccountType, Balance) 
VALUES 
(1, 'Savings', 5000.00);

INSERT INTO Transactions (AccountID, TransactionType, Amount) 
VALUES 
(1, 'Deposit', 2000.00);

SELECT Name, AccountType, Balance 
FROM Customers 
JOIN Accounts ON Customers.CustomerID = Accounts.CustomerID 
WHERE Customers.CustomerID = 1;

UPDATE Accounts SET Balance = Balance + 1000 WHERE AccountID = 1;
INSERT INTO Transactions (AccountID, TransactionType, Amount) VALUES (1, 'Deposit', 1000.00);

UPDATE Accounts SET Balance = Balance - 500 WHERE AccountID = 1 AND Balance >= 500;
INSERT INTO Transactions (AccountID, TransactionType, Amount) VALUES (1, 'Withdraw', 500.00);
