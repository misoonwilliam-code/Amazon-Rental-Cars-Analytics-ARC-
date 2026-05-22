📊 [View Interactive Power BI Dashboard](https://shorturl.at/8HlU3)
📈 [Access Raw Data & Excel Sheets](https://shorturl.at/seNvx)
---

## 💻 SQL Data Modeling & Analytics

In this project, I structures and optimizes a relational database for a car rental system using SQL Server. This includes defining Primary Keys, enforcing Referential Integrity through Foreign Keys, and conducting business performance analysis.

### 1. Database Schema & Relationships (DDL)
The script below sets up constraints to build a robust star/snowflake schema, ensuring data consistency across contracts, customers, vehicles, and locations.

```sql
USE [Car Rental];
GO

-- 1. Defining Primary Keys for Dimension Tables
ALTER TABLE [dbo].[Vehicle$] 
ALTER COLUMN [Vehicle ID] INT NOT NULL;
ALTER TABLE [dbo].[Vehicle$] 
ADD CONSTRAINT PK_Vehicle_ID PRIMARY KEY ([Vehicle ID]);

ALTER TABLE [dbo].[Customer$] 
ALTER COLUMN [Customer ID] INT NOT NULL;
ALTER TABLE [dbo].[Customer$] 
ADD CONSTRAINT PK_Customer_ID PRIMARY KEY ([Customer ID]);

ALTER TABLE [dbo].[Pickup$] 
ALTER COLUMN [Pickup ID] INT NOT NULL;
ALTER TABLE [dbo].[Pickup$] 
ADD CONSTRAINT PK_Pickup_ID PRIMARY KEY ([Pickup ID]);

ALTER TABLE [dbo].[Location_Dropoff$] 
ALTER COLUMN [Drop off ID] INT NOT NULL;
ALTER TABLE [dbo].[Location_Dropoff$] 
ADD CONSTRAINT PK_Dropoff_ID PRIMARY KEY ([Drop off ID]);

ALTER TABLE [dbo].[All_Contract$] 
ALTER COLUMN [Contract ID] INT NOT NULL;
ALTER TABLE [dbo].[All_Contract$] 
ADD CONSTRAINT PK_All_Contract PRIMARY KEY ([Contract ID]);

-- 2. Establishing Foreign Key Relationships
ALTER TABLE [dbo].[All_Contract$]
ADD CONSTRAINT FK_Vehicle_Link 
FOREIGN KEY ([Vehicle ID]) REFERENCES [dbo].[Vehicle$]([Vehicle ID]);

ALTER TABLE [dbo].[All_Contract$]  
ADD CONSTRAINT FK_Customer_Link 
FOREIGN KEY ([Customer ID]) REFERENCES [dbo].[Customer$]([Customer ID]);

ALTER TABLE [dbo].[All_Contract$]
ADD CONSTRAINT FK_Pickup_Link 
FOREIGN KEY ([Pickup Branch ID]) REFERENCES [dbo].[Pickup$]([Pickup ID]);

ALTER TABLE [dbo].[All_Contract$]
ADD CONSTRAINT FK_Dropoff_Link 
FOREIGN KEY ([Drop Off Branch ID]) REFERENCES [dbo].[Location_Dropoff$]([Drop off ID]);

ALTER TABLE [dbo].[Contract_Line$] 
ADD CONSTRAINT FK_Line_To_Contract
FOREIGN KEY ([Contract ID]) REFERENCES [dbo].[All_Contract$]([Contract ID]);
