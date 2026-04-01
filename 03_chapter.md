---
title: "The Accounting Data Environment"
---

::: {.chapter-meta}
[Conceptual Chapter]{.chapter-pill}
[Northwind]{.dataset-badge .dataset-nw}
[AdventureWorks]{.dataset-badge .dataset-aw}
[ERPNext]{.dataset-badge .dataset-erp}
:::

---

## Learning Objectives

After completing this chapter, you will be able to:

1. Explain the structure of a relational database and describe how tables, rows, columns, and data types organize accounting information.
2. Distinguish between primary keys and foreign keys and explain how they establish relationships between tables in an accounting database.
3. Read and interpret an Entity-Relationship diagram using crow's foot notation to identify tables, relationships, and cardinality.
4. Map familiar accounting structures such as the chart of accounts, general ledger, and sub-ledgers to their representations as related tables in a database.
5. Compare the database designs of Northwind, AdventureWorks, and ERPNext and evaluate how each design reflects the complexity of the underlying business.

---

## Opening Scenario

You are a junior auditor assigned to a new client that uses an enterprise resource planning system to manage its accounting records. During the planning meeting, the senior auditor mentions that the team will extract data directly from the client's database to perform analytical procedures. She pulls up a diagram showing dozens of interconnected boxes, each representing a table in the database, and explains that understanding this diagram is essential before writing any queries. You recognize some of the table names from your accounting courses, such as "GeneralLedger," "SalesInvoice," and "ChartOfAccounts," but the lines connecting the tables and the symbols at their endpoints are unfamiliar. You realize that to work effectively with this data, you need to understand not just accounting concepts but also how those concepts are represented in a database. This chapter provides that understanding. It introduces the relational database model, explains how accounting data is organized within it, and walks you through the database designs of the three datasets you will use throughout this book.

---

## From Accounting Records to Database Tables

In your introductory accounting courses, you learned to work with familiar structures such as the chart of accounts, the general journal, the general ledger, and various sub-ledgers. You recorded transactions as debits and credits, posted them to T-accounts, prepared trial balances, and produced financial statements. These structures have served the accounting profession for centuries, and they remain the conceptual foundation of financial record-keeping.

What has changed is how organizations store and access these structures. In a manual system, the general journal is a physical book. In a spreadsheet-based system, it is a worksheet. In a modern organization, it is a table in a relational database. The chart of accounts is another table. The accounts receivable sub-ledger is yet another table. These tables are connected to one another through defined relationships that mirror the connections you already understand from accounting. The CustomerID on an invoice connects that invoice to a specific customer record. The AccountCode on a journal entry connects that entry to a specific account in the chart of accounts. These connections exist in manual systems as cross-references and posting notations. In a database, they are formalized as structural features that the system enforces and that analytical tools can use.

Understanding how accounting data is organized in a database is a prerequisite for everything that follows in this textbook. When you write SQL queries in Part III, you will need to know which tables contain the data you need and how those tables connect to one another. When you build data models in Power BI in Part IV, you will define relationships between tables that determine how your calculations and visualizations behave. Even in the Excel chapters of Part II, understanding the source structure helps you anticipate what the data will look like when you import it and what preparation steps will be necessary. The concepts in this chapter are not abstract. They are the practical foundation for every analytical task you will perform.

> **[IN PRACTICE]**
> Accounting firms increasingly expect new hires to understand relational database concepts. Auditors who can read a database diagram and identify the tables relevant to a particular audit procedure work more efficiently during fieldwork. A 2018 survey of public accounting professionals found that understanding data structures and database concepts ranked among the most valuable technical skills for entry-level staff, second only to spreadsheet proficiency (Sledgianowski, Gomaa, and Tan, 2017).


## The Relational Database Model

A relational database stores data in a collection of tables that are related to one another through shared values. The relational model was proposed by Edgar F. Codd in 1970 and has become the dominant approach to data storage in business information systems (Codd, 1970). Virtually every enterprise resource planning system, accounting software package, and transaction processing system in use today stores its data in a relational database. Understanding this model is therefore essential for any accountant who needs to access data directly rather than relying on pre-built reports.

### Tables, Rows, and Columns

The fundamental unit of a relational database is the table. A table stores information about one type of entity or event. In an accounting context, a table might store information about customers, products, sales orders, journal entries, or accounts. Each table has a name that identifies what it contains. The Northwind database, for example, has a table called Customers that stores information about every customer the company does business with, and a table called Orders that records every sales order the company has received.

A table is organized into rows and columns. Each row represents a single instance of the entity or event that the table describes. In the Customers table, each row represents one customer. In the Orders table, each row represents one order. Each column represents a single attribute of that entity or event. In the Customers table, columns include CompanyName, ContactName, City, Country, and Phone. In the Orders table, columns include OrderID, CustomerID, OrderDate, ShippedDate, and Freight.

*[Figure 3.1: Anatomy of a Database Table. An annotated diagram showing the Northwind Customers table with labels identifying the table name, column headers, rows, and individual cell values. The annotation explains that each row is one customer and each column is one attribute of that customer.]*

If this structure looks familiar, it should. A database table is structurally identical to a well-organized spreadsheet or to the tidy data format described in Chapter 2. Each variable occupies its own column, and each observation occupies its own row. The difference is that a database enforces this structure. When a table is created, the database requires a definition that specifies the name, the data type, and the constraints for every column. This definition prevents the kind of structural drift that occurs in spreadsheets, where a user might insert a comment in a data column or merge cells in ways that break the tabular format.

### Data Types

Every column in a database table has a defined data type that specifies what kind of values the column can hold. The most common data types in accounting databases include integers (whole numbers used for identifiers and counts), decimal or numeric values (numbers with fractional parts used for monetary amounts, prices, and quantities), text or character strings (used for names, descriptions, and codes), dates (used for transaction dates, due dates, and posting dates), and Boolean values (true or false values used for status flags such as whether an invoice has been paid).

Data types matter for accounting analytics because they determine what operations are possible. You can calculate the sum of a column defined as a decimal but not the sum of a column defined as text. You can sort dates chronologically but only if the database recognizes the values as dates rather than text strings. Many of the data quality problems discussed in Chapter 2, such as a transaction amount stored as text because it includes a currency symbol, are essentially data type problems. When you work with the textbook datasets in later chapters, the data types are already defined correctly because the datasets were created as proper databases. In professional practice, however, you will encounter situations where data types are misconfigured, and understanding what the correct types should be will help you identify and resolve those problems.

*[Table 3.1: Common Data Types in Accounting Databases. A table with three columns (Data Type, Description, Accounting Example) and five rows covering INTEGER, DECIMAL/NUMERIC, TEXT/VARCHAR, DATE, and BOOLEAN. Each row includes an example from the textbook datasets.]*

> **[WATCH OUT]**
> A column that contains numbers is not necessarily a numeric data type. Account codes such as "4100" and "5200" are often stored as text rather than as numbers because they are identifiers, not quantities. You would never add two account codes together or calculate the average account code. Storing them as text prevents accidental arithmetic and preserves leading zeros that a numeric type would drop. When you encounter a column of numbers in a database, consider whether the values represent quantities to be calculated or codes to be matched.


## Keys and Relationships

The power of a relational database comes not from individual tables but from the connections between them. In an accounting system, transactions do not exist in isolation. An order is placed by a customer, fulfilled by an employee, and contains products purchased from suppliers. A journal entry debits one account and credits another, and both accounts appear in the chart of accounts. These connections are represented in a database through keys.

### Primary Keys

A primary key is a column, or a combination of columns, that uniquely identifies each row in a table. No two rows in the same table can have the same primary key value, and the primary key cannot be blank. In the Northwind Customers table, the primary key is CustomerID. Every customer has a unique CustomerID, and no two customers share the same value. In the Northwind Orders table, the primary key is OrderID. Every order has a unique OrderID that distinguishes it from every other order in the table.

Primary keys serve the same purpose in a database that unique identifiers serve in accounting. An invoice number uniquely identifies an invoice. A check number uniquely identifies a payment. An employee number uniquely identifies an employee. When these documents and records are stored in a database, the identifying number becomes the primary key of the corresponding table. The database enforces uniqueness automatically, meaning it will reject any attempt to insert a second row with an existing primary key value. This enforcement is a form of data integrity control that prevents the duplication problems discussed in Chapter 2.

### Foreign Keys

A foreign key is a column in one table that references the primary key of another table. Foreign keys create the connections between tables that make a relational database relational. In the Northwind Orders table, the column CustomerID is a foreign key that references the CustomerID primary key in the Customers table. This relationship means that every order is linked to a specific customer. If you know the CustomerID on an order, you can look up that customer's name, address, and contact information in the Customers table.

Foreign keys mirror the cross-references that exist in accounting records. When you post a journal entry to the general ledger, the account number on the entry refers to a specific account in the chart of accounts. That account number is functioning as a foreign key. When a sales invoice references a customer number, that customer number links the invoice to the customer master file. The database formalizes these references as structural constraints. A well-designed database will reject an order that references a CustomerID that does not exist in the Customers table, just as a well-designed accounting system will reject a journal entry that references an account code that does not appear in the chart of accounts.

*[Figure 3.2: Primary Keys and Foreign Keys Illustrated. A diagram showing the Northwind Customers table and the Orders table side by side. The CustomerID column in Customers is labeled "PK" (primary key). The CustomerID column in Orders is labeled "FK" (foreign key). An arrow connects the two columns, showing that each FK value in Orders points to a PK value in Customers. Sample data rows illustrate the connection.]*

The relationship between a primary key and a foreign key establishes what database designers call referential integrity. This means that every foreign key value must correspond to an existing primary key value in the referenced table. If a customer is deleted from the Customers table while orders referencing that customer still exist in the Orders table, the database has a referential integrity violation. The orders now reference a customer that does not exist, and any analysis that joins the two tables will produce incomplete results. Referential integrity constraints prevent this by blocking deletions or updates that would create orphaned references. In Chapter 2, the exercise that checked whether every CustomerID in the Orders table existed in the Customers table was essentially a manual referential integrity test.

> **[CONNECTING THE DOTS]**
> In Chapter 10, you will write SQL JOIN statements that use exactly these key relationships to combine data from multiple tables. A JOIN on Orders.CustomerID = Customers.CustomerID retrieves the customer name for each order. Understanding keys now will make JOIN syntax intuitive rather than mysterious when you encounter it in Part III.


## Relationships and Cardinality

The relationship between two tables has a direction and a cardinality, meaning it specifies how many rows in one table can be associated with a single row in the other table. Three types of cardinality are common in accounting databases.

A one-to-many relationship means that one row in the first table can be associated with many rows in the second table, but each row in the second table is associated with only one row in the first table. This is the most common relationship type in accounting data. One customer can place many orders, but each order belongs to one customer. One account in the chart of accounts can have many general ledger entries, but each entry is posted to one account. One product category can contain many products, but each product belongs to one category. In the Northwind database, the relationship between Customers and Orders is one-to-many. Customer "ALFKI" has placed multiple orders, and each of those orders has "ALFKI" as its CustomerID.

A one-to-one relationship means that each row in the first table is associated with exactly one row in the second table, and vice versa. One-to-one relationships are less common but do occur. In AdventureWorks, each employee row in the Employee table has a corresponding row in the Person table that stores personal details such as name and contact information. The two tables are linked by a shared identifier, and each employee has exactly one person record.

A many-to-many relationship means that each row in the first table can be associated with many rows in the second table, and each row in the second table can also be associated with many rows in the first table. In accounting, consider the relationship between orders and products. One order can contain many products, and one product can appear on many orders. Relational databases cannot directly represent a many-to-many relationship. Instead, they use a junction table (also called a bridge table or associative table) that sits between the two tables and converts the many-to-many relationship into two one-to-many relationships. In Northwind, the OrderDetails table serves this purpose. It sits between Orders and Products, with each row representing one product line on one order. The OrderDetails table has a foreign key to Orders (OrderID) and a foreign key to Products (ProductID).

*[Figure 3.3: The Three Types of Cardinality. A three-panel diagram showing one-to-one, one-to-many, and many-to-many relationships. Each panel uses simple labeled boxes and connecting lines with crow's foot symbols. The one-to-many panel uses the Northwind Customers-to-Orders example. The many-to-many panel shows the Orders-OrderDetails-Products pattern with the junction table clearly labeled.]*

Understanding cardinality is important for analytics because it affects the results you get when you combine tables. When you join a one-to-many relationship in SQL or in a Power BI data model, the many side of the relationship can multiply rows in your results. If you join the Customers table to the Orders table and a customer has 15 orders, that customer's information will appear 15 times in the output, once for each order. This is correct and expected behavior, but if you are not aware of the cardinality, you might accidentally count the customer 15 times when calculating the number of customers. Many analytical errors in accounting result from misunderstanding the cardinality of a relationship, and the ER diagrams described in the next section help you avoid those errors by making cardinality visible.

> **[WATCH OUT]**
> The most common mistake students make when working with related tables is double-counting. If you join a customer table to an orders table to an order details table, a single customer with 5 orders and 20 line items across those orders will appear 20 times in the result set. Summing revenue at the line-item level is correct. Counting the customer at the line-item level overstates the customer count by a factor of 20. Always consider the cardinality of each join before performing aggregations.


## Entity-Relationship Diagrams

An Entity-Relationship diagram, commonly called an ER diagram, is a visual representation of the tables in a database and the relationships between them. ER diagrams are the maps that database designers, analysts, and auditors use to understand the structure of a data environment. Reading an ER diagram is a skill you will use repeatedly in this textbook and in professional practice.

### How to Read an ER Diagram

In the notation used throughout this textbook, each table appears as a rectangle. The rectangle has a header bar containing the table name and a body listing the column names. Primary key columns are marked with "PK" and foreign key columns are marked with "FK." Relationships between tables are shown as lines connecting the foreign key in one table to the primary key it references in another table.

The endpoints of each relationship line use crow's foot notation to indicate cardinality. A single line ending in a perpendicular bar indicates "one." A line ending in a three-pronged fork (resembling a crow's foot) indicates "many." A relationship line with a bar on one end and a crow's foot on the other represents a one-to-many relationship. The bar end points to the "one" table, and the crow's foot end points to the "many" table.

*[Figure 3.4: Reading Crow's Foot Notation. A reference diagram showing the four common endpoint symbols used in crow's foot ER diagrams: "one and only one" (bar with bar), "one or many" (bar with crow's foot), "zero or one" (circle with bar), and "zero or many" (circle with crow's foot). Each symbol includes a brief label and an accounting example of when it applies.]*

Consider a concrete example. The Northwind ER diagram shows a line between the Customers table and the Orders table. The Customers end of the line has a single bar, meaning "one." The Orders end has a crow's foot, meaning "many." Reading the relationship aloud, you would say "one customer can have many orders." Looking at the columns, you can see that CustomerID is the primary key of the Customers table and a foreign key in the Orders table. This tells you that the connection between the two tables is made through the CustomerID column, and that to retrieve a customer's name alongside their orders, you would match these two columns.

ER diagrams serve the same purpose for a database that a chart of accounts serves for an accounting system. The chart of accounts tells you how the organization classifies its financial transactions. The ER diagram tells you how the database organizes its data. Just as you would consult the chart of accounts before preparing a journal entry, you should consult the ER diagram before writing a query or building a data model.

> **[IN PRACTICE]**
> Auditors routinely request ER diagrams or data dictionaries from clients during the planning phase of an engagement. Understanding the client's database structure helps the audit team identify which tables contain the data needed for analytical procedures, which relationships need to be traversed to connect transactions to their supporting details, and where potential data integrity risks exist. The AICPA's Guide to Audit Data Analytics recommends that auditors document their understanding of the client's data structure before performing data extraction (AICPA, 2017).


## The Accounting Data Model

The relational concepts described so far apply to databases in any domain. What makes an accounting database distinctive is the specific set of entities it stores and the relationships between them. This section shows how the familiar structures of accounting map to tables and relationships in a database. Seeing these connections will help you move between accounting concepts and database structures without difficulty.

### The Chart of Accounts as a Table

The chart of accounts is the organizational backbone of any accounting system. It defines every account the organization uses to classify its financial transactions, typically organized into five major categories: assets, liabilities, equity, revenues, and expenses. In a database, the chart of accounts is stored as a table where each row represents one account. Columns typically include an account code or number, an account name, an account type (asset, liability, equity, revenue, or expense), and a parent account reference that defines the hierarchical structure.

In the ERPNext dataset, the chart of accounts is stored in the Account table. Each row contains an account name, an account type classification, and a parent account reference that places the account within the hierarchy. The parent account reference is a foreign key that points to another row in the same table, creating what database designers call a self-referencing relationship or recursive relationship. The "Cash and Cash Equivalents" account, for example, might have "Current Assets" as its parent account, and "Current Assets" might have "Assets" as its parent. This hierarchical structure allows the database to represent the multi-level account groupings that appear on financial statements.

*[Figure 3.5: The Chart of Accounts as a Database Table. An annotated diagram showing a portion of the ERPNext Account table with columns for AccountName, AccountType, and ParentAccount. Arrows illustrate the self-referencing relationship where child accounts point to their parent accounts. The annotation explains how this structure represents the account hierarchy.]*

### The General Ledger as a Related Table

The general ledger records every financial transaction as a series of debit and credit entries. In a database, the general ledger is typically stored as a table where each row represents one side of a journal entry: a single debit or a single credit. Columns include the posting date, the account reference, the debit amount, the credit amount, a voucher type identifying the source document, and a voucher number linking the entry to the originating transaction.

The relationship between the general ledger table and the chart of accounts table is one-to-many. One account can appear in many general ledger entries, but each general ledger entry is posted to one account. The account reference in the general ledger table is a foreign key that points to the primary key of the chart of accounts table. This relationship is the database equivalent of posting a journal entry to a T-account. When you sum the debits and credits for a given account across all general ledger entries, you calculate that account's balance, which is precisely what a trial balance reports.

In the ERPNext dataset, the GLEntry table stores the general ledger. Each row has a field that references the Account table, establishing the connection between individual entries and the chart of accounts. This relationship is what makes it possible to produce a trial balance from the database: you group the GLEntry rows by account and sum the debit and credit columns for each group.

### Sub-Ledgers and Their Relationship to the General Ledger

Sub-ledgers provide transaction-level detail for specific account categories. The accounts receivable sub-ledger, for example, records individual customer invoices and payments. The accounts payable sub-ledger records individual vendor invoices and payments. In a manual system, the sub-ledger detail rolls up to a control account in the general ledger, and the control account balance should equal the sum of all sub-ledger balances.

In a database, sub-ledgers are represented as tables that connect to the general ledger through shared identifiers. In the ERPNext dataset, the SalesInvoice table functions as part of the accounts receivable sub-ledger. Each sales invoice generates general ledger entries in the GLEntry table, and the voucher number recorded in both tables links the summary posting to its source document. This link allows an analyst or auditor to start with a general ledger balance, identify the journal entries that compose it, and trace each entry back to the original invoice.

The Northwind dataset demonstrates a simpler version of this pattern. The Orders and OrderDetails tables function as a sales sub-ledger, recording the details of each sales transaction. Northwind does not have a general ledger table, so the sub-ledger is the most detailed record available. In practice, a company like Northwind would have a general ledger in its accounting system, and the order data in Northwind would feed summary entries into that ledger. Understanding that the three datasets represent different levels of accounting completeness, as discussed in Chapter 1, helps you select the right dataset for a given analytical task.

*[Figure 3.6: The Relationship Between the General Ledger and Sub-Ledgers. A diagram showing the ERPNext Account table at the top, connected to the GLEntry table in the middle, which is connected to the SalesInvoice and PurchaseInvoice tables at the bottom. Arrows and cardinality symbols show that one account has many GL entries, and each GL entry can be traced to a source document in a sub-ledger table. Annotations label the general ledger layer and the sub-ledger layer.]*

> **[CONNECTING THE DOTS]**
> In Chapter 12, you will write SQL queries that trace transactions from the ERPNext general ledger back to their source documents in the sub-ledger tables. This trace is one of the most important procedures in audit analytics because it tests whether the amounts reported in the financial statements are supported by underlying transactions. The database structure you are learning here makes that trace possible.


## The Northwind Database Design

Now that you understand the components of a relational database, it is time to examine the designs of the three textbook datasets in detail. Each database reflects the complexity of the business it represents. Studying all three together will show you how the same relational principles apply at different scales and in different business contexts.

Northwind Traders is a small wholesale food distribution company, and its database reflects that simplicity. The database contains eight core tables organized around two main business activities: selling products to customers and purchasing products from suppliers.

The sales side of the database centers on three tables. The Orders table records each sales order with columns for the order date, required date, shipped date, and freight amount. The OrderDetails table records the individual line items on each order, with columns for the product, quantity, unit price, and discount. The Customers table stores information about each customer, including company name, contact name, and address. The relationship between Customers and Orders is one-to-many (one customer, many orders), and the relationship between Orders and OrderDetails is also one-to-many (one order, many line items). As discussed earlier, OrderDetails also connects to the Products table through the ProductID foreign key, resolving the many-to-many relationship between orders and products.

The product side of the database includes the Products table, which records each product's name, unit price, units in stock, and units on order, and the Categories table, which classifies products into groups such as "Beverages," "Condiments," and "Seafood." Each product belongs to one category, and one category contains many products.

The supply side includes the Suppliers table, which stores information about the companies that provide products to Northwind. Each product has one supplier, recorded through the SupplierID foreign key in the Products table.

Two additional tables support operations. The Employees table records the sales representatives who handle orders. The Shippers table records the shipping companies that deliver orders. Both connect to the Orders table through foreign keys.

*[Figure 3.7: Full Entity-Relationship Diagram for Northwind Traders. A complete ER diagram showing all eight tables (Customers, Orders, OrderDetails, Products, Categories, Suppliers, Employees, Shippers) with their columns, primary keys, foreign keys, and relationships displayed in crow's foot notation. Tables use teal header bars per the visual design specification.]*

The Northwind design is clean and compact. With only eight tables and straightforward one-to-many relationships, it is easy to understand and navigate. This simplicity is why Northwind serves as the primary dataset for the foundational chapters of this textbook. When you learn new tools and techniques, working with a database you can hold in your head lets you focus on the technique itself rather than struggling with data complexity.


## The AdventureWorks Database Design

Adventure Works Cycles is a mid-size multinational bicycle manufacturer, and its database reflects the complexity of a manufacturing operation. The database contains approximately 70 tables organized across five functional areas, or schemas: Sales, Production, Purchasing, Human Resources, and Person.

A schema is a logical grouping of related tables within a database. Schemas serve the same organizational purpose that departments serve in a company: they group related activities together and make it easier to find what you need. In AdventureWorks, the Sales schema contains tables related to customer orders, territories, and sales representatives. The Production schema contains tables related to products, work orders, bills of materials, and scrap tracking. The Purchasing schema contains tables for vendor management and purchase orders. The Human Resources schema stores employee and department information. The Person schema stores personal details shared across functional areas.

The Sales schema follows a pattern similar to Northwind but with additional complexity. The SalesOrderHeader table records order-level information such as the order date, customer, territory, and total amount due. The SalesOrderDetail table records individual line items. The Customer table stores customer information, and the SalesTerritory table defines the geographic regions where sales occur. These tables are connected through foreign keys in the same way as their Northwind counterparts, but with additional attributes and relationships that support multi-territory, multi-currency operations.

The Production schema introduces tables that have no equivalent in Northwind. The Product table stores product information including standard cost and list price. The WorkOrder table records manufacturing jobs, including the quantity ordered, quantity produced, quantity scrapped, and dates. The BillOfMaterials table defines the components required to manufacture each product. The ScrapReason table classifies why production units were rejected. These tables allow the database to track not just what was sold but how it was made, at what cost, and with what level of waste.

The Purchasing schema includes the PurchaseOrderHeader and PurchaseOrderDetail tables, which record orders placed with vendors, and the Vendor table, which stores vendor information. These tables support exercises in purchasing cycle analysis, vendor evaluation, and procurement testing.

*[Figure 3.8: Focused Entity-Relationship Diagram for AdventureWorks Sales and Production Schemas. A diagram showing a selected subset of AdventureWorks tables from the Sales schema (SalesOrderHeader, SalesOrderDetail, Customer, SalesTerritory) and the Production schema (Product, WorkOrder, BillOfMaterials, ProductSubcategory). Tables use primary blue header bars. Relationships use crow's foot notation. The full diagram appears in Appendix B.]*

The AdventureWorks design demonstrates how a relational database scales to accommodate a more complex business. The same principles of primary keys, foreign keys, and one-to-many relationships that you saw in Northwind apply here, but they connect a much larger network of tables. Navigating this network requires an ER diagram, which is why the ability to read such diagrams is an essential skill for accounting analytics.

> **[IN PRACTICE]**
> Manufacturing companies typically have the most complex database structures among the organizations that accountants serve. Production data introduces tables for bills of materials, work centers, routing steps, scrap tracking, and quality control, all of which connect to the financial data through cost records. Cost accountants and auditors working in manufacturing frequently need to traverse relationships that span multiple schemas to answer questions such as "What was the actual cost of producing this product, and how does it compare to the standard cost?" The AdventureWorks dataset prepares you for exactly this type of analysis.


## The ERPNext Database Design

The ERPNext Demo Company operates within a full enterprise resource planning environment, and its database design reflects the integrated nature of an ERP system. Unlike Northwind, which captures order-level transactions, and AdventureWorks, which adds manufacturing data, ERPNext includes a complete accounting module. This makes ERPNext the most relevant dataset for financial reporting, audit analytics, and any exercise that requires working directly with the general ledger.

The core of the ERPNext accounting module is the relationship between three tables. The Account table stores the chart of accounts with its hierarchical structure. The GLEntry table stores every debit and credit entry that makes up the general ledger. The JournalEntry table stores the header information for manually created journal entries, including the posting date, the entry type, and any descriptive notes. The GLEntry table connects to the Account table through an account reference foreign key, and it connects to source documents such as journal entries, sales invoices, and purchase invoices through a voucher type and voucher number pair.

Beyond the accounting core, ERPNext includes tables for sales invoices (SalesInvoice), purchase invoices (PurchaseInvoice), payment entries (PaymentEntry), cost centers (CostCenter), and budgets (Budget). The SalesInvoice table records revenue transactions and connects to the GLEntry table through the voucher reference, allowing analysts to trace a revenue balance in the general ledger back to the individual invoices that compose it. The CostCenter table defines the organizational units used for management reporting, and general ledger entries are tagged with cost center references that enable departmental analysis.

*[Figure 3.9: Focused Entity-Relationship Diagram for ERPNext Accounting Module. A diagram showing the Account table, GLEntry table, JournalEntry table, SalesInvoice table, PurchaseInvoice table, and PaymentEntry table with their key columns and relationships. Tables use amber header bars. The voucher type and voucher number linkage between GLEntry and the source document tables is highlighted with an annotation. The full diagram appears in Appendix B.]*

The ERPNext design illustrates a key feature of ERP databases: every transaction, regardless of its origin, ultimately flows into the general ledger. A sales invoice creates GL entries that debit accounts receivable and credit revenue. A purchase invoice creates GL entries that debit an expense or inventory account and credit accounts payable. A payment entry creates GL entries that debit or credit cash and the corresponding receivable or payable. This design means that the GLEntry table is the single source of truth for the organization's financial position, and every balance reported on the financial statements can be verified by querying that table.

The ERPNext database also illustrates the concept of a polymorphic relationship, though you do not need to know that term for this course. The GLEntry table uses two columns, voucher type and voucher number, to link entries to their source documents. The voucher type column identifies which source table to look in (SalesInvoice, PurchaseInvoice, JournalEntry, PaymentEntry), and the voucher number identifies the specific record within that table. This design is common in ERP systems and is more flexible than having a separate foreign key column for each possible source table, but it requires you to filter by voucher type before following the reference.

> **[WATCH OUT]**
> The voucher type and voucher number pattern in ERPNext is different from a standard foreign key because the database cannot enforce referential integrity across multiple target tables. This means that a GLEntry could theoretically reference a voucher number that does not exist in the corresponding source table. In Chapter 12, you will write SQL queries to test for exactly this kind of referential integrity problem as part of an audit analytics exercise.


## Comparing the Three Database Designs

Looking at all three databases together reveals how the relational model adapts to businesses of different sizes and complexities. Several patterns emerge from the comparison.

The first pattern is that database complexity increases with business complexity. Northwind has 8 tables and represents a straightforward buy-and-sell operation. AdventureWorks has approximately 70 tables and represents a manufacturing company with multiple departments. ERPNext has dozens of tables spanning a full ERP environment. The number of tables is not the important metric. What matters is the range of business activities captured and the depth of relationships between them. Each additional business process, whether it is manufacturing, multi-territory sales, or integrated budgeting, adds tables and relationships to the database.

The second pattern is that the accounting depth of the database varies. Northwind has no general ledger or chart of accounts. Its data supports sales and purchasing analysis but not financial statement preparation. AdventureWorks adds cost and production data but still lacks a complete accounting module. ERPNext provides the full accounting cycle from chart of accounts through general ledger to financial statements. This progression is deliberate. The textbook introduces Northwind first for its simplicity, adds AdventureWorks when cost and production analysis become relevant, and brings in ERPNext when the exercises require working with the general ledger and financial statements.

The third pattern is that the same relational principles apply at every scale. A foreign key in Northwind works exactly the same way as a foreign key in ERPNext. A one-to-many relationship between customers and orders in a small database follows the same rules as a one-to-many relationship between accounts and GL entries in a large one. The SQL syntax, the Power BI modeling techniques, and the Excel lookup functions you will learn all operate on these same relational foundations regardless of database size.

*[Table 3.2: Comparison of the Three Textbook Database Designs. A table with rows for Number of Core Tables, Schema or Functional Organization, Accounting Module Presence, Key Relationship Examples, Junction Table Examples, and Self-Referencing Relationships. Columns are Northwind Traders, Adventure Works Cycles, and ERPNext Demo Company.]*


## Guided Tutorial 3.1: Reading the Northwind ER Diagram

**Context and objective.** In this tutorial, you will study the full Northwind ER diagram and practice identifying tables, keys, relationships, and cardinality. The goal is to develop fluency in reading ER diagrams so that you can navigate any database structure you encounter in later chapters or in professional practice.

**Prerequisites.** You need access to the Northwind ER diagram provided with this textbook (printed in this chapter as Figure 3.7 and also available as a separate file in the companion materials).

**Step-by-step instructions.**

**Step 1.** Locate Figure 3.7, the full Northwind ER diagram. Begin by counting the tables. You should identify eight tables: Customers, Orders, OrderDetails, Products, Categories, Suppliers, Employees, and Shippers. Each table is represented as a rectangle with a header bar and a list of columns.

**Step 2.** Identify the primary key of each table. Look for the column marked "PK" in each table. The primary keys are CustomerID (Customers), OrderID (Orders), ProductID (Products), CategoryID (Categories), SupplierID (Suppliers), EmployeeID (Employees), and ShipperID (Shippers). The OrderDetails table has a composite primary key consisting of both OrderID and ProductID together, because a single order can include a given product only once, and the combination of order and product uniquely identifies each line item.

**Step 3.** Identify the foreign keys in the Orders table. The Orders table contains three foreign keys: CustomerID (referencing Customers), EmployeeID (referencing Employees), and ShipVia (referencing Shippers). Each foreign key links the order to a related entity. Trace each foreign key to the table it references and confirm that the referenced column is the primary key of that table.

**Step 4.** Read the cardinality of the relationship between Customers and Orders. Find the line connecting the two tables. The Customers end should show a single bar (meaning "one"), and the Orders end should show a crow's foot (meaning "many"). Read the relationship aloud: "One customer can have many orders. Each order belongs to one customer."

**Step 5.** Find the OrderDetails table. Notice that it sits between Orders and Products. Trace its two foreign keys: OrderID connects to the Orders table, and ProductID connects to the Products table. Both relationships are one-to-many (one order has many line items, one product appears on many line items). The OrderDetails table is the junction table that resolves the many-to-many relationship between orders and products.

**Step 6.** Trace a complete path through the diagram. Start at the Categories table. Follow the relationship to the Products table (one category has many products). From Products, follow the relationship to OrderDetails (one product appears on many order line items). From OrderDetails, follow the relationship to Orders (many line items belong to one order). From Orders, follow the relationship to Customers (many orders belong to one customer). You have now traced a path from product category to customer, crossing four tables and three relationships. This is the kind of path you will traverse in SQL queries when you want to answer questions such as "Which customers purchased products in the Seafood category?"

*[Figure 3.10: Annotated Northwind ER Diagram with Traced Path. The same ER diagram as Figure 3.7, with a highlighted path from Categories through Products, OrderDetails, Orders, and Customers. Numbered callout markers identify each step in the path, and annotations explain the cardinality at each connection.]*

**Checkpoint.** You should now be able to answer the following questions by reading the Northwind ER diagram. How many foreign keys does the Orders table contain? (Three: CustomerID, EmployeeID, and ShipVia.) Which table serves as the junction table between Orders and Products? (OrderDetails.) What is the cardinality of the relationship between Categories and Products? (One-to-many: one category, many products.) If you can answer all three questions correctly, you have the ER diagram reading skills you will need for the chapters ahead.


## Guided Tutorial 3.2: Comparing Database Designs Across All Three Datasets

**Context and objective.** In this tutorial, you will compare the ER diagrams of all three textbook databases to understand how different business environments produce different data structures. The goal is to build your ability to assess a database design and determine what analytical questions it can support.

**Prerequisites.** You need access to the ER diagrams for all three datasets (Figures 3.7, 3.8, and 3.9 in this chapter, with full versions in Appendix B).

**Step-by-step instructions.**

**Step 1.** Examine the Northwind ER diagram (Figure 3.7) and identify the tables that store revenue-related data. The relevant tables are Orders and OrderDetails, which together record what was sold, to whom, in what quantity, at what price, and with what discount. Note that calculating total revenue requires joining these two tables because the Orders table has the order-level information while the OrderDetails table has the line-item amounts.

**Step 2.** Examine the AdventureWorks focused ER diagram (Figure 3.8) and identify the tables that store revenue-related data. The relevant tables are SalesOrderHeader and SalesOrderDetail, which follow the same header-detail pattern as Northwind. Additionally, the SalesTerritory table adds geographic context, and the Product table adds cost data (StandardCost and ListPrice) that Northwind does not provide. Note that AdventureWorks enables profitability analysis (revenue minus cost) while Northwind provides only the revenue side.

**Step 3.** Examine the ERPNext focused ER diagram (Figure 3.9) and identify the tables that store revenue-related data. In ERPNext, revenue appears in two places. The SalesInvoice table records individual revenue transactions at the invoice level. The GLEntry table records the corresponding general ledger entries, including the revenue account credits. The Account table classifies the revenue accounts within the chart of accounts hierarchy. Note that ERPNext enables financial statement preparation because it has the full accounting chain from source document (SalesInvoice) through general ledger (GLEntry) to account classification (Account).

**Step 4.** For each dataset, determine whether you could prepare a trial balance from the available data. A trial balance requires a list of all accounts and their balances, calculated by summing debits and credits from the general ledger. Northwind does not have a general ledger or chart of accounts, so a trial balance is not possible. AdventureWorks has product cost data but no general ledger, so a trial balance is not possible. ERPNext has both a chart of accounts (Account table) and a general ledger (GLEntry table), so a trial balance can be prepared by grouping GL entries by account and summing debits and credits.

**Step 5.** For each dataset, identify one analytical question that the database can answer and one that it cannot. Write these down in a brief comparison. For example, Northwind can answer "What is the total revenue by product category?" but cannot answer "What is the company's net income?" because it lacks expense and equity data. AdventureWorks can answer "What is the scrap rate by product line?" but cannot answer "What is the balance in the accounts payable control account?" because it lacks a general ledger. ERPNext can answer "What is the balance of every account on the trial balance?" but may have limited product-level manufacturing detail compared to AdventureWorks.

**Checkpoint.** You should now have a written comparison that identifies the analytical strengths and limitations of each database design. You should be able to explain why a database with more tables is not necessarily better than one with fewer tables. The right database for a given task is the one whose tables and relationships contain the specific data that the task requires.


## Looking Ahead

This chapter has introduced the relational database model and shown you how accounting data is organized within it. You have learned how tables, rows, columns, and data types store information, how primary keys and foreign keys create relationships between tables, and how Entity-Relationship diagrams make these structures visible. You have examined the database designs of all three textbook datasets and compared their ability to support different accounting tasks.

In the next chapter, you will begin working with data directly. Chapter 4 introduces Excel as an analytical tool and teaches you to organize accounting data in Excel Tables, apply sorting and filtering, and use conditional formatting to identify patterns. The relational concepts from this chapter will remain in the background as you work, because the data you import into Excel comes from the same tables and relationships you have just studied.

---

## Chapter Summary

Accounting data in modern organizations is stored in relational databases, which organize information into tables connected by defined relationships. Understanding this structure is a prerequisite for writing SQL queries, building Power BI data models, and preparing data for analysis in Excel. The relational model, first proposed by Codd (1970), has become the standard approach to data storage in business information systems and underlies virtually every ERP system and accounting software package in use today.

A relational database consists of tables, each storing information about one type of entity or event. Tables are organized into rows (one per instance) and columns (one per attribute), and every column has a defined data type that determines what values it can hold and what operations are possible. Primary keys uniquely identify each row in a table, and foreign keys create connections between tables by referencing the primary key of a related table. These keys formalize the cross-references that have always existed in accounting records: an invoice references a customer, a journal entry references an account, and a line item references a product.

Relationships between tables have a cardinality that specifies how many rows on each side of the relationship can be associated. One-to-many relationships are the most common in accounting data: one customer has many orders, one account has many GL entries, one category contains many products. Many-to-many relationships are resolved through junction tables, such as Northwind's OrderDetails table that connects orders to products. Understanding cardinality is essential for avoiding analytical errors such as double-counting when combining data from multiple tables.

Entity-Relationship diagrams provide a visual map of a database's structure. They show tables as labeled rectangles, relationships as connecting lines, and cardinality through crow's foot notation. Reading an ER diagram is a practical skill that auditors, analysts, and accountants use when planning data extractions, designing queries, and building data models. The three ER diagrams studied in this chapter, for Northwind, AdventureWorks, and ERPNext, illustrate how database complexity scales with business complexity while the underlying relational principles remain constant.

The familiar structures of accounting, including the chart of accounts, the general ledger, and the sub-ledgers, map directly to tables and relationships in a database. The chart of accounts is a table with a self-referencing hierarchy. The general ledger is a table of debit and credit entries linked to the chart of accounts through a foreign key. Sub-ledgers are tables of detailed transaction records that connect to the general ledger through voucher references. These mappings make it possible to perform financial reporting, audit testing, and managerial analysis directly from the database, which is exactly what you will do in the chapters ahead.

---

## Key Terms

**Cardinality.** The specification of how many rows on each side of a relationship can be associated with one another. The three types are one-to-one, one-to-many, and many-to-many. In accounting databases, one-to-many is the most common cardinality.

**Column.** A single attribute within a database table, representing one piece of information recorded for every row. Examples include OrderDate, AccountName, and UnitPrice.

**Composite primary key.** A primary key consisting of two or more columns together, where no single column alone is sufficient to uniquely identify a row. The Northwind OrderDetails table uses a composite primary key of OrderID and ProductID.

**Crow's foot notation.** A visual notation system used in Entity-Relationship diagrams to indicate cardinality. A single bar represents "one" and a three-pronged fork represents "many."

**Data type.** The defined category of values that a column can hold, such as integer, decimal, text, date, or Boolean. Data types determine which operations can be performed on a column's values.

**Entity-Relationship (ER) diagram.** A visual representation of the tables in a database and the relationships between them, showing table names, column names, keys, and cardinality using standardized notation.

**Foreign key.** A column in one table that references the primary key of another table, creating a defined relationship between the two tables. For example, CustomerID in the Northwind Orders table is a foreign key referencing the Customers table.

**Junction table.** A table that resolves a many-to-many relationship between two other tables by converting it into two one-to-many relationships. The Northwind OrderDetails table is a junction table between Orders and Products.

**Many-to-many relationship.** A relationship in which each row in either table can be associated with multiple rows in the other table. Relational databases represent many-to-many relationships through junction tables.

**One-to-many relationship.** A relationship in which one row in the first table can be associated with many rows in the second table, but each row in the second table is associated with only one row in the first table. This is the most common relationship type in accounting databases.

**Primary key.** A column or combination of columns that uniquely identifies each row in a table. No two rows can share the same primary key value, and the value cannot be blank.

**Referential integrity.** The property of a database in which every foreign key value corresponds to an existing primary key value in the referenced table. Referential integrity prevents orphaned records that reference nonexistent related entries.

**Relational database.** A data storage system that organizes information into tables connected by defined relationships through primary and foreign keys. The three textbook datasets are all relational databases provided in SQLite format.

**Row.** A single record within a database table, representing one instance of the entity or event the table describes. Each row in the Northwind Orders table represents one customer order.

**Schema.** A logical grouping of related tables within a database. AdventureWorks uses schemas such as Sales, Production, Purchasing, and Human Resources to organize its approximately 70 tables.

**Self-referencing relationship.** A relationship in which a foreign key in a table references the primary key of the same table, creating a hierarchy within a single table. The ERPNext Account table uses this pattern to define the parent-child structure of the chart of accounts.

**Table.** The fundamental storage unit in a relational database, organized into rows and columns. Each table stores information about one type of entity or event, such as customers, orders, or general ledger entries.

---

## Multiple Choice Questions

**1.** In a relational database, which of the following best describes the role of a primary key?

A. It stores the most important data value in the table.
B. It uniquely identifies each row in a table and cannot be duplicated or left blank.
C. It connects one table to another by referencing a column in a different table.
D. It defines the data type for all columns in the table.

**2.** The CustomerID column appears in both the Northwind Customers table and the Northwind Orders table. In the Orders table, this column functions as a:

A. Primary key
B. Foreign key
C. Composite key
D. Data type

**3.** An ER diagram shows a line between two tables. The line has a single bar on one end and a crow's foot on the other end. This notation represents which type of relationship?

A. One-to-one
B. One-to-many
C. Many-to-many
D. The notation does not indicate cardinality

**4.** The Northwind OrderDetails table contains the columns OrderID and ProductID, both of which are foreign keys. This table exists because:

A. It stores the primary key of the Orders table.
B. It resolves a many-to-many relationship between orders and products.
C. It is required for every database to have at least one table with two foreign keys.
D. It stores customer contact information for each order.

**5.** A cost accountant wants to compare standard product costs to actual production costs. Which textbook database is best suited for this analysis?

A. Northwind, because it contains product pricing data
B. AdventureWorks, because it contains both standard cost data in the Product table and production data in the WorkOrder table
C. ERPNext, because it contains a complete general ledger
D. Any of the three databases would work equally well for this analysis

**6.** In the ERPNext database, the Account table contains a column called ParentAccount that references another row in the same Account table. This is an example of a:

A. Foreign key referencing a different table
B. Composite primary key
C. Self-referencing relationship
D. Many-to-many relationship

**7.** An auditor wants to prepare a trial balance directly from database tables. Which textbook dataset provides the necessary data?

A. Northwind, using the Orders and OrderDetails tables
B. AdventureWorks, using the SalesOrderHeader and Product tables
C. ERPNext, using the Account table and the GLEntry table
D. None of the three datasets supports trial balance preparation

**8.** In the AdventureWorks database, tables are organized into schemas such as Sales, Production, and Purchasing. The primary purpose of schemas is to:

A. Restrict access to certain tables based on user roles
B. Group related tables together for logical organization and easier navigation
C. Increase the speed of database queries
D. Store backup copies of tables in case of data loss

**9.** A relational database enforces referential integrity. This means that:

A. Every table must contain at least one foreign key.
B. Primary key values can be duplicated as long as the duplicates are in different tables.
C. Every foreign key value must correspond to an existing primary key value in the referenced table.
D. Tables without relationships are automatically deleted from the database.

**10.** An analyst joins the Northwind Customers table to the Orders table and then to the OrderDetails table. One customer has 10 orders, and those 10 orders contain a total of 45 line items. How many rows will this customer contribute to the joined result?

A. 1 row
B. 10 rows
C. 45 rows
D. 55 rows

**11.** Which of the following accounting structures is represented in a database as a self-referencing table where child rows point to parent rows within the same table?

A. The general ledger
B. The trial balance
C. The chart of accounts hierarchy
D. The accounts receivable sub-ledger

**12.** The ERPNext GLEntry table uses a voucher type and voucher number to link general ledger entries to their source documents. This design differs from a standard foreign key because:

A. It uses two columns instead of one.
B. It can reference multiple different tables depending on the voucher type, which prevents the database from enforcing referential integrity automatically.
C. It does not require the referenced record to exist.
D. It is only used for journal entries and not for other transaction types.

**13.** Which of the following is the best definition of a relational database?

A. A database that stores all data in a single large table
B. A data storage system that organizes information into tables connected through defined relationships using primary and foreign keys
C. A spreadsheet with multiple worksheets
D. A database that requires SQL to access its data

**14.** A database table has a column defined as the INTEGER data type. Which of the following values could this column store?

A. "Accounts Receivable"
B. 2024-03-15
C. 4500
D. 99.73

**15.** The Northwind database has 8 tables and the AdventureWorks database has approximately 70 tables. Which of the following best explains this difference?

A. AdventureWorks is a newer database and uses more modern design principles.
B. Northwind contains errors that should have been stored in additional tables.
C. AdventureWorks captures more business processes, including manufacturing, multi-territory sales, and human resources, each of which requires its own set of tables.
D. The number of tables is arbitrary and has no relationship to the complexity of the business.

---

## Applied Exercises

### Financial Accounting Exercises

**Exercise 3.1 (Financial Accounting): Tracing a Revenue Transaction Through the ERPNext Database**

**Dataset:** ERPNext (Account, GLEntry, SalesInvoice)

**Scenario.** You are a financial reporting analyst preparing to verify that revenue transactions recorded in the ERPNext system are properly reflected in the general ledger. Before writing any queries or performing any calculations, you need to understand the path a revenue transaction follows through the database, from the source document to the account balance.

**Requirements.** (1) Open the ERPNext dataset in Excel and examine the SalesInvoice, GLEntry, and Account tables. For a revenue transaction, identify the specific columns in each table that would allow you to trace the transaction from the invoice, through the general ledger entry, to the account in the chart of accounts. Write down the column names that serve as the connecting links between these three tables. (2) Select one sales invoice from the SalesInvoice table. Record its voucher number. Then search the GLEntry table for all entries that reference this voucher number. Identify the accounts that were debited and credited. Verify that the debit and credit amounts for this transaction are equal. (3) For each account referenced in the general ledger entries you found, locate the account in the Account table and note its account type (asset, liability, equity, revenue, or expense). Confirm that the account classifications make sense for a revenue transaction (for example, the credit should be to a revenue account and the debit should be to a receivable or cash account). (4) Prepare a brief written trace (one page) that documents the path of the transaction through the three tables, identifying each table, the relevant columns, the connecting keys, and the amounts involved. This trace represents the type of vouching procedure that auditors perform to verify financial statement assertions.

**Deliverable.** A one-page written transaction trace documenting the path of a revenue transaction through the ERPNext database.


**Exercise 3.2 (Financial Accounting): Mapping the Northwind Database to the Revenue Cycle**

**Dataset:** Northwind (Customers, Orders, OrderDetails, Products)

**Scenario.** You are a financial reporting analyst who has been asked to document how the Northwind database captures the revenue cycle. Your documentation will be used by the team as a reference when preparing revenue analyses in later chapters.

**Requirements.** (1) Using the Northwind ER diagram (Figure 3.7), identify all tables involved in recording a sale from the initial order through the line-item details to the product and customer information. List each table and describe its role in the revenue cycle in one to two sentences. (2) For each pair of connected tables in the revenue cycle path, identify the foreign key that creates the connection and state the cardinality of the relationship. (3) Identify what revenue cycle information is missing from the Northwind database. Consider whether the database records cash receipts, tracks accounts receivable balances, or includes a general ledger. For each gap you identify, explain what additional table or tables would be needed and what columns they would contain. (4) Prepare a brief written summary (one page) that could serve as a data dictionary excerpt for the revenue-related tables in Northwind.

**Deliverable.** A one-page data dictionary excerpt covering the Northwind revenue cycle tables, their relationships, and their limitations.


### Managerial Accounting Exercises

**Exercise 3.3 (Managerial Accounting): Mapping the AdventureWorks Production Database**

**Dataset:** AdventureWorks (Product, WorkOrder, BillOfMaterials, ProductSubcategory)

**Scenario.** You are a cost analyst at Adventure Works Cycles. Your manager has asked you to document the database tables that support manufacturing cost analysis so that the team can plan a product costing project for the upcoming quarter.

**Requirements.** (1) Using the AdventureWorks ER diagram and the Excel workbook, identify all tables that store production-related data. For each table, write one to two sentences describing what it contains and how it relates to manufacturing cost analysis. (2) Trace the path through the database that connects a finished product to its component materials. Start at the Product table and follow the relationships through the BillOfMaterials table. Explain how a cost analyst would use this path to calculate the material cost of a product. (3) Identify the table that records actual production activity (WorkOrder). Examine its columns and determine what information is available for comparing planned production to actual production, including quantities ordered, quantities produced, and quantities scrapped. (4) Determine whether the AdventureWorks database allows you to calculate the variance between standard cost and actual cost for a specific product. Identify which tables and columns would be involved and note any gaps where the data may be insufficient. (5) Write a brief memorandum (one page) summarizing the production-related data available in AdventureWorks and assessing its suitability for a product cost analysis project.

**Deliverable.** A one-page memorandum documenting the AdventureWorks production data and its suitability for cost analysis.


**Exercise 3.4 (Managerial Accounting): Evaluating Cost Center Data in ERPNext**

**Dataset:** ERPNext (CostCenter, GLEntry, Budget)

**Scenario.** You are a management accountant preparing to build a departmental performance report that compares budgeted expenses to actual expenses by cost center. Before starting the analysis, you need to understand how cost center data is structured in the ERPNext database.

**Requirements.** (1) Open the ERPNext dataset and examine the CostCenter table. Identify the columns available and describe the hierarchical structure if one exists. (2) Examine the GLEntry table and determine how general ledger entries are associated with cost centers. Identify the column that links GL entries to the CostCenter table and state the cardinality of the relationship. (3) Examine the Budget table, if available, and determine how budgeted amounts are associated with cost centers and accounts. Identify the columns that connect budget records to cost centers and to the chart of accounts. (4) Assess whether the ERPNext database provides sufficient data to compare budgeted versus actual spending for each cost center. Identify any gaps, such as missing cost center assignments on GL entries or budget records that do not correspond to actual GL account codes. Write a brief assessment (one half to one page) documenting your findings.

**Deliverable.** A written assessment of the ERPNext cost center data structure and its readiness for budget-versus-actual analysis.


### Auditing Exercises

**Exercise 3.5 (Auditing): Planning a Data Extraction Strategy**

**Dataset:** All three (Northwind, AdventureWorks, ERPNext)

**Scenario.** You are an IT auditor responsible for planning the data extraction needed to support three audit procedures: a revenue completeness test, a purchasing cycle test, and a journal entry analysis for management override of controls. For each procedure, you need to identify which database to use, which tables to extract, and which relationships you will need to traverse.

**Requirements.** (1) For the revenue completeness test, identify the database and tables you would use. Explain which table contains the population of revenue transactions and which related tables you would need to join in order to verify that each transaction includes a valid customer, a valid product, and an amount. State the keys that connect the tables. (2) For the purchasing cycle test, identify the database and tables you would use. The test requires you to verify that every purchase order was placed with an approved vendor and that the quantities and prices on the purchase order match the quantities and prices recorded in the receiving records. Identify which tables are relevant and note any gaps in the available data. (3) For the journal entry analysis, identify the database and tables you would use. The analysis requires access to every manually created journal entry, including the posting date, the amounts, the accounts debited and credited, and the person who created the entry. Identify which tables contain this information and which columns would be useful for risk-based filtering (such as entries posted on weekends or entries with round-dollar amounts). (4) Prepare a data extraction plan (one to two pages) that documents your selections for all three procedures, including the database, tables, key columns, and relationships for each.

**Deliverable.** A one-to-two page data extraction plan for three audit procedures, identifying specific tables and relationships in the textbook databases.


**Exercise 3.6 (Auditing): Assessing Referential Integrity Across the Northwind Database**

**Dataset:** Northwind (all tables)

**Scenario.** Your audit senior has asked you to perform a preliminary check on the referential integrity of the Northwind database. Referential integrity problems, where a foreign key references a primary key value that does not exist, can indicate data migration errors, deletion of master records without updating related transactions, or system configuration problems. Any integrity violations you find will be flagged for further investigation.

**Requirements.** (1) Using the Northwind ER diagram, identify all foreign key relationships in the database. List each relationship by specifying the child table, the foreign key column, the parent table, and the primary key column. (2) For each relationship you identified, use Excel lookup or counting functions to test whether every foreign key value in the child table exists as a primary key value in the parent table. Record the number of orphaned references (if any) for each relationship. (3) Pay particular attention to the relationship between Orders and Customers, between OrderDetails and Products, and between Products and Suppliers. For any orphaned references you find, record the specific foreign key values that have no match and the number of records affected. (4) Prepare a brief memorandum (one page) documenting your referential integrity testing results. For each relationship tested, state whether integrity was maintained or violated, and for any violations, describe the potential impact on financial analyses that depend on those relationships.

**Deliverable.** A one-page referential integrity testing memorandum documenting the results for all foreign key relationships in the Northwind database.

---

## Further Reading

Codd, E. F. (1970). A relational model of data for large shared data banks. *Communications of the ACM*, 13(6), 377-387. This paper introduced the relational database model that underlies virtually every modern business information system. Although the paper is technical, the core ideas of organizing data into tables with defined relationships are accessible, and understanding their origin helps explain why relational databases work the way they do. This is one of the most influential papers in the history of computing.

Dunn, C. L., Cherrington, J. O., and Hollander, A. S. (2005). *Enterprise information systems: A pattern-based approach* (3rd ed.). McGraw-Hill/Irwin. This textbook provides a comprehensive treatment of how accounting information systems are designed using relational database concepts. The chapters on REA (Resources, Events, Agents) modeling are particularly useful for understanding how accounting transactions map to database tables and relationships.

Gelinas, U. J., Dull, R. B., and Wheeler, P. R. (2018). *Accounting information systems* (11th ed.). Cengage Learning. This widely used accounting information systems textbook includes detailed coverage of relational databases, ER diagrams, and their application to accounting data. The chapters on database design and data modeling provide additional depth on the concepts introduced in this chapter.

Sledgianowski, D., Gomaa, M., and Tan, C. (2017). Toward integration of Big Data, technology, and information systems competencies into the accounting curriculum. *Journal of Accounting Education*, 38, 81-93. This paper reports on a survey of accounting professionals about the technology competencies needed by entry-level accountants. The findings support the claim that understanding database concepts is valued by employers and that accounting curricula should include instruction on relational data structures.

AICPA (American Institute of Certified Public Accountants). (2017). *Guide to audit data analytics.* AICPA. This professional guidance document includes recommendations for auditors on understanding client data structures before performing data analytics procedures. The guide's discussion of data extraction planning and relationship mapping aligns with the ER diagram reading skills taught in this chapter.

McCarthy, W. E. (1982). The REA accounting model: A generalized framework for accounting systems in a shared data environment. *The Accounting Review*, 57(3), 554-578. This paper introduced the REA model, which applies entity-relationship concepts specifically to accounting system design. The framework describes accounting data in terms of resources, events, and agents rather than debits and credits, providing an alternative perspective on how accounting transactions are represented in databases. Understanding the REA model deepens the connection between the database concepts in this chapter and the accounting concepts students already know.

Romney, M. B., and Steinbart, P. J. (2018). *Accounting information systems* (14th ed.). Pearson. This textbook provides thorough coverage of relational databases and ER modeling in the context of accounting information systems. The chapters on database design, data modeling, and REA diagrams offer additional practice with the concepts introduced in this chapter, and the book includes numerous exercises using accounting scenarios.
