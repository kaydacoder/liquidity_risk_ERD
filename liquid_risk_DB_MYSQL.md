    -- creating a database to store the tables. 
    CREATE DATABASE liquidity_risk;
    
    -- utilising the recently created database.
    USE liquidity_risk;
    
    -- Customers table.
    CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    FirstName VARCHAR(255),
    LastName VARCHAR(255),
    Email VARCHAR(255) UNIQUE,
    Phone VARCHAR(255),
    Address VARCHAR(255),
    City VARCHAR(255),
    State VARCHAR(255),
    ZipCode INT,
    Country VARCHAR(255)
    );
    
    -- Accounts table.
    CREATE TABLE Accounts(
    AccountID INT PRIMARY KEY,
    CustomerID INT,
    AccountType VARCHAR(255),
    Balance FLOAT,
    CreatedAt DATE NOT NULL,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
    );
    
    -- Transactions table
    CREATE TABLE Transactions(
    TransactionID INT PRIMARY KEY,
    AccountID INT,
    TransactionType VARCHAR(255),
    Amount FLOAT,
    TransactionDate DATE NOT NULL,
    FOREIGN KEY (AccountID) REFERENCES Accounts(AccountID)
    );
    
    -- Liquidity_Positions table
    CREATE TABLE Liquidity_Positions (
    PositionID INT PRIMARY KEY,
    AccountID INT,
    LiquidityType VARCHAR(255),
    -- 'Value_' the underscore alleviates conflict with the 'value' keyword.  
    Value_ FLOAT,
    AsOfDate DATE NOT NULL,
    FOREIGN KEY (AccountID) REFERENCES Accounts(AccountID)
    );
    
    -- Liquidity_Risks table
    CREATE TABLE Liquidity_Risks (
    RiskID INT PRIMARY KEY,
    PositionID INT,
    Risk_Type VARCHAR(255),
    Risk_Value VARCHAR(255),
    AssessmentDate DATE NOT NULL,
    FOREIGN KEY (PositionID) REFERENCES Liquidity_Positions(PositionID)
    );
