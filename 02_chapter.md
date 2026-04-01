---
title: "Understanding Data in Accounting"
---

::: {.chapter-meta}
[Conceptual Chapter]{.chapter-pill}
[Northwind]{.dataset-badge .dataset-nw}
[ERPNext]{.dataset-badge .dataset-erp}
:::

---


## Learning Objectives

After completing this chapter, you will be able to:

1. Distinguish between quantitative and qualitative data and between structured and unstructured data, and identify examples of each in accounting contexts.
2. Describe the primary sources of accounting data, including general ledgers, sub-ledgers, trial balances, enterprise resource planning systems, and external data feeds.
3. Evaluate accounting data against four quality dimensions: accuracy, completeness, consistency, and timeliness.
4. Explain the concept of tidy data and why it matters for accounting analytics.
5. Identify common data quality problems in the Northwind and ERPNext datasets, including missing values, duplicates, inconsistent formatting, and outliers.

---

## Opening Scenario

You are a newly hired internal auditor at a mid-size wholesale distribution company that recently migrated its accounting records from a legacy system to a new enterprise resource planning platform. Your supervisor has asked you to verify that the migrated data is reliable enough to support the upcoming year-end audit. When you begin examining the general ledger entries, you notice that some account names use abbreviations while others are spelled out in full. Several transactions are missing posting dates. A handful of customer records appear more than once under slightly different names. Before the audit team can use this data to test account balances, perform analytical procedures, or identify anomalies, someone needs to assess the quality of the data itself. Your supervisor has asked you to prepare that assessment. This chapter will give you the vocabulary, the framework, and the practical skills to evaluate whether accounting data is fit for analysis.

---

## Why Data Quality Comes First

Chapter 1 introduced the six-stage accounting analytics workflow, beginning with defining the question and ending with communicating findings. This chapter focuses on a concern that cuts across every stage of that workflow: the quality of the underlying data. No analytical technique, no matter how sophisticated, can produce reliable results if the data it operates on contains errors, gaps, or inconsistencies. A PivotTable built on revenue data with missing transaction dates will produce period totals that understate actual performance. A SQL query designed to detect duplicate payments will miss duplicates if vendor names are recorded inconsistently across tables. A Power BI dashboard showing budget-versus-actual comparisons will mislead managers if the budget data and the actual data use different account classifications.

The principle is straightforward. The quality of every analytical output is constrained by the quality of the data that feeds it. Researchers in information systems have formalized this idea by studying data quality as a measurable property of datasets, with dimensions that can be assessed, monitored, and improved (Wang and Strong, 1996). For accountants, data quality is not an abstract concern. It is a professional responsibility. Auditing standards require auditors to evaluate the reliability of data used in analytical procedures. Management accountants who present cost analyses to executives are implicitly vouching for the integrity of the numbers. Financial reporting analysts who prepare disclosures from database extracts must ensure that the underlying data supports the figures reported. Understanding what data quality means, how to assess it, and what problems to look for is therefore a prerequisite for everything else in this textbook.


## Data Types in Accounting

Before you can evaluate the quality of a dataset, you need to understand the types of data it contains. Accounting data takes many forms, and the appropriate way to store, analyze, and interpret a piece of data depends on what type it is. Two classification schemes are particularly useful for accounting analytics: the distinction between quantitative and qualitative data, and the distinction between structured and unstructured data.

### Quantitative and Qualitative Data

Quantitative data consists of values that represent measurements or counts and that can be meaningfully subjected to arithmetic operations. In accounting, the most familiar quantitative data includes transaction amounts (debits, credits, invoice totals, payment amounts), quantities (units produced, units sold, units in inventory), and calculated values (ratios, percentages, variances). Quantitative data can be further divided into continuous data, which can take any value within a range (such as a transaction amount of $1,247.83), and discrete data, which takes only specific values (such as the number of journal entries posted in a given month).

Qualitative data consists of values that represent categories, labels, or descriptions rather than measurements. In accounting, qualitative data includes account names, customer names, vendor classifications, transaction descriptions, product categories, and status codes such as "paid" or "outstanding." Qualitative data can be nominal, meaning the categories have no natural order (such as the names of cost centers), or ordinal, meaning the categories have a meaningful sequence (such as a credit rating scale from AAA to D).

The distinction matters because it determines which analytical techniques are appropriate. You can calculate an average transaction amount, but you cannot calculate an average account name. You can count the number of transactions in each product category, but the category labels themselves are not quantities. Many data quality problems arise when qualitative data is treated as quantitative or when quantitative data is stored in a format that prevents arithmetic operations. A common example is a transaction amount stored as text rather than as a number because the original data source included a currency symbol or a comma in the value. The number looks correct to a human reader, but Excel and SQL cannot perform calculations on it until the formatting is corrected.

*[Table 2.1: Examples of Quantitative and Qualitative Data in Accounting. A table with three columns (Data Type, Accounting Example, Typical Source) and six rows showing examples such as transaction amounts from the general ledger (continuous quantitative), unit quantities from inventory records (discrete quantitative), account names from the chart of accounts (nominal qualitative), and aging categories from receivables schedules (ordinal qualitative).]*

### Structured and Unstructured Data

A second important distinction is between structured and unstructured data. Structured data is organized into a predefined format, typically rows and columns in a table, where each column has a defined data type and each row represents a single observation or transaction. All three datasets used in this textbook contain structured data. The Northwind Orders table, for example, has columns for OrderID, CustomerID, OrderDate, and Freight, and each row represents one customer order. Structured data is the primary input for the analytical techniques covered in this book, including PivotTables in Excel, SQL queries, and Power BI data models.

Unstructured data lacks a predefined tabular format. In accounting, unstructured data includes the text of contracts, the narrative sections of annual reports, email correspondence between auditors and clients, scanned images of invoices, and the notes that accountants attach to journal entries. Unstructured data often contains valuable information, but extracting that information requires different tools and techniques than those used for structured data. Natural language processing, a branch of artificial intelligence, is increasingly used to analyze unstructured accounting documents such as lease agreements and regulatory filings (Fisher, Garnsey, and Hughes, 2016). Chapter 20 discusses these emerging technologies in more detail.

Between these two extremes lies semi-structured data, which has some organizational elements but does not fit neatly into rows and columns. An example relevant to accounting is an XBRL (eXtensible Business Reporting Language) filing, which contains financial data tagged with standardized labels but organized in a hierarchical rather than tabular structure. Another example is a bank statement in PDF format that contains tabular transaction data embedded within an unstructured document layout.

*[Figure 2.1: The Spectrum of Data Structure. A horizontal diagram showing three zones from left to right: Structured Data (example: a general ledger table with defined columns), Semi-Structured Data (example: an XBRL filing with tagged financial elements), and Unstructured Data (example: a contract document in plain text). Each zone includes a brief description and an accounting example.]*

> **[IN PRACTICE]**
> Most of the data that accountants work with in practice is structured. General ledgers, trial balances, accounts receivable aging schedules, and payroll registers are all structured datasets stored in rows and columns within ERP systems or accounting software. However, the proportion of unstructured data in accounting work is growing as firms adopt tools for contract analysis, disclosure review, and automated document processing. Developing strong skills with structured data, as this textbook teaches, provides the foundation for working with less structured data as your career progresses.

This textbook focuses almost entirely on structured data because it represents the majority of what accountants analyze and because the tools covered here (Excel, SQL, and Power BI) are designed for structured datasets. The datasets you will work with throughout the book are all structured, with clearly defined tables, columns, and data types. Understanding this foundation is essential before you can evaluate whether a dataset is ready for analysis.


## Sources of Accounting Data

Accounting data originates from many places within and outside an organization. Understanding where data comes from helps you anticipate its strengths and limitations, which in turn helps you assess its quality and suitability for a given analytical task. This section describes the most common sources of accounting data that you will encounter in practice.

### The General Ledger and Sub-Ledgers

The general ledger is the central repository of an organization's financial transactions. Every debit and credit entry that affects the financial statements passes through the general ledger. In a database environment, the general ledger is typically stored as a table where each row represents one side of a journal entry (a single debit or credit), and columns record the posting date, the account number, the amount, a description, and a reference to the source document or voucher. The ERPNext dataset used in this textbook stores its general ledger in the GLEntry table, which follows exactly this structure.

Sub-ledgers provide detailed records for specific account categories. The accounts receivable sub-ledger, for example, contains individual customer balances and the invoices and payments that make up each balance. The accounts payable sub-ledger contains individual vendor balances. The inventory sub-ledger contains records of individual stock items, their quantities, and their costs. Sub-ledgers feed summary totals to the general ledger, and the balances in the two should agree. When they do not, the discrepancy becomes an audit finding. In the Northwind dataset, the Orders and OrderDetails tables function as a sales sub-ledger, recording individual transactions at a level of detail that a general ledger summary would not capture.

### Trial Balances

A trial balance is a listing of all general ledger account balances at a specific point in time. It serves as a control to verify that total debits equal total credits and as the starting point for preparing financial statements. In an analytics context, the trial balance is useful as a summary dataset that provides a high-level view of the organization's financial position. Auditors frequently use the trial balance as the population from which they select accounts for testing. The trial balance is not a separate table in most databases but rather a report generated by summing the general ledger entries for each account.

### Enterprise Resource Planning Systems

An enterprise resource planning system integrates data from across an organization's functional areas into a single database. A typical ERP system captures not only financial transactions but also sales orders, purchase orders, production schedules, inventory movements, human resources records, and customer relationship management data. This integration means that an accountant with access to the ERP database can trace a sales transaction from the customer order through the shipment, the invoice, the revenue recognition entry in the general ledger, and the cash receipt. The ERPNext dataset in this textbook simulates this integrated environment, with tables spanning the full cycle from sales invoices through general ledger entries and payment records.

ERP systems are the dominant data source in large and mid-size organizations. They produce structured data with defined fields, data types, and validation rules. However, ERP data is not immune to quality problems. Data entry errors, system configuration mistakes, and gaps in validation rules can all introduce inaccuracies that propagate through the system. One of the advantages of the analytical skills taught in this textbook is the ability to identify these problems by examining the data directly rather than relying solely on the reports the ERP system generates (Grabski, Leech, and Schmidt, 2011).

*[Figure 2.2: Common Sources of Accounting Data. A diagram showing five data sources (General Ledger, Sub-Ledgers, Trial Balance, ERP System, and External Feeds) connected by arrows to a central box labeled "Accounting Analytics." Each source box includes a one-sentence description of the type of data it provides.]*

### External Data Sources

Accountants also work with data that originates outside the organization. External data sources include bank statements used for cash reconciliation, market price feeds used for fair value measurements, credit rating data used for impairment assessments, tax rate tables used for compliance calculations, and industry benchmarking data used for comparative analysis. External data introduces additional quality concerns because the accountant has less control over how the data was collected, formatted, and maintained. When external data is combined with internal data for analysis, differences in formatting, time periods, or classification schemes can create inconsistencies that must be resolved before the analysis can proceed.

> **[CONNECTING THE DOTS]**
> In Chapter 5, you will use Excel lookup functions and Power Query to merge data from different sources, such as combining Northwind order data with customer details from a separate table. The challenges you encounter in that chapter, including mismatched identifiers and inconsistent formatting, are practical examples of the data quality issues discussed here. Understanding the sources of accounting data now will help you anticipate those challenges when you begin working with the tools.


## Data Quality Dimensions

Data quality is not a single characteristic that data either has or lacks. Researchers have identified multiple dimensions of data quality, each describing a different aspect of what makes data fit for its intended use. The framework developed by Wang and Strong (1996) identified more than a dozen dimensions, but four are particularly important for accounting analytics: accuracy, completeness, consistency, and timeliness. These four dimensions provide a practical vocabulary for describing data problems and assessing whether a dataset is suitable for a given analytical task.

### Accuracy

Accuracy means that the recorded values correspond to the true values they are intended to represent. A transaction amount of $5,000 is accurate if the actual transaction was indeed $5,000. An account classification of "current asset" is accurate if the account genuinely meets the definition of a current asset under the applicable accounting standards. Accuracy is the most fundamental quality dimension because inaccurate data leads directly to incorrect analytical results.

In accounting datasets, accuracy problems arise from data entry errors (typing $50,000 instead of $5,000), calculation errors (applying the wrong exchange rate to a foreign currency transaction), classification errors (posting an expense to the wrong account), and measurement errors (using an incorrect cost allocation formula). Some accuracy problems are obvious when you inspect the data, such as a negative value in a field that should always be positive. Others are subtle and can only be detected by comparing the data to an independent source or by applying analytical tests such as reasonableness checks.

### Completeness

Completeness means that all expected data values are present. A dataset is complete if it contains all the records that should be there and if every field within each record has a value where one is expected. Completeness problems take two forms. The first is missing records, where entire transactions or entities are absent from the dataset. The second is missing values, where individual fields within existing records are blank or null.

In accounting, completeness is a significant concern for both preparers and auditors. A revenue dataset that is missing the last three days of the fiscal period will understate total revenue. An accounts payable listing that omits recently recorded invoices will understate total liabilities. Auditors specifically test for completeness because management has an incentive to understate liabilities and overstate assets, and missing data can serve that purpose either intentionally or accidentally. In the Northwind dataset, you will discover that some orders have missing shipped dates, which raises the question of whether those orders were ever fulfilled.

### Consistency

Consistency means that the same fact is represented in the same way wherever it appears. A customer named "Acme Corporation" in the accounts receivable table should not appear as "ACME Corp." in the sales order table and "Acme Corp" in the payment records table. An account coded as "4100" in the chart of accounts should be coded as "4100" everywhere it is referenced in the general ledger, not as "4100.0" in some entries and "41-00" in others.

Consistency problems are among the most common data quality issues in accounting datasets, and they are particularly troublesome because they can cause analytical results to be silently wrong rather than obviously wrong. If a SQL query groups revenue by customer name and the same customer appears under three different name variations, the query will produce three separate line items instead of one. The total revenue figure will be correct, but the per-customer breakdown will be misleading. Consistency problems are especially prevalent when data comes from multiple sources or when an organization has undergone a system migration (Redman, 2001).

### Timeliness

Timeliness means that the data reflects the current state of the business as of the relevant reporting date. A balance sheet analysis performed on general ledger data that has not been updated to include the final adjusting entries of the period will produce inaccurate results. A receivables aging analysis based on data that is two weeks old may overstate the number of delinquent accounts if payments have been received in the interim.

Timeliness is a quality dimension that depends on context. Data that is perfectly timely for a monthly management report may be inadequate for a daily cash position analysis. The analytical question determines what level of timeliness is required. Accountants must assess whether the data they are working with is current enough for the purpose at hand and, if it is not, either obtain more current data or disclose the limitation in their analysis.

*[Table 2.2: The Four Data Quality Dimensions with Accounting Examples. A table with four rows (Accuracy, Completeness, Consistency, Timeliness) and three columns (Dimension, Definition, Accounting Example). Each row includes a concrete example of a quality problem drawn from common accounting scenarios.]*

> **[WATCH OUT]**
> A dataset can score well on one quality dimension while failing on another. The general ledger may be perfectly accurate (every amount matches the source document) and perfectly consistent (every account code follows the same format) but incomplete because transactions from a subsidiary were not yet consolidated. Evaluating data quality requires examining all four dimensions, not just the one that is easiest to check.


## Common Data Quality Problems in Accounting Datasets

The four quality dimensions provide a framework for thinking about data quality, but in practice, accountants encounter specific types of problems that recur across organizations and systems. Learning to recognize these problems is the first step toward resolving them. This section describes the most common data quality problems you will encounter when working with accounting data.

### Missing Values

Missing values occur when a field that should contain data is blank, null, or contains a placeholder such as "N/A" or "TBD." In accounting datasets, missing values often appear in date fields (a payment date that was never recorded), in descriptive fields (a journal entry with no memo), and in classification fields (a transaction that was never assigned to a cost center). Missing values can affect analysis in several ways. Some analytical tools exclude records with missing values from calculations, which can distort totals and averages. Other tools treat missing values as zeros, which produces a different type of distortion.

### Duplicate Records

Duplicate records occur when the same transaction, entity, or event appears more than once in a dataset. In accounts payable, a duplicate payment means the organization paid the same invoice twice. In a customer master file, a duplicate customer record means the same customer has two identities in the system, which splits their transaction history and makes it difficult to assess total purchasing volume or outstanding receivables. Duplicates can result from data entry errors, system integration problems, or the failure of validation controls. Detecting duplicates is an important audit analytics procedure, and you will perform duplicate detection exercises in several chapters of this textbook.

### Inconsistent Formatting

Inconsistent formatting occurs when the same type of data is recorded in different formats across records or across tables. Date formatting is a frequent source of inconsistency. One table may store dates as "2024-03-15" while another stores them as "03/15/2024" or "15-Mar-2024." Name formatting is another common issue. Vendor names may appear with or without legal suffixes ("Inc.", "LLC"), with different capitalization, or with abbreviated words. Currency amounts may include or exclude currency symbols, and numeric values may use commas or periods as decimal separators depending on regional settings.

Inconsistent formatting is more than a cosmetic problem. When data from two tables must be matched or merged, formatting differences can prevent correct joins and lookups. An XLOOKUP formula in Excel or a JOIN clause in SQL that matches on customer name will fail to connect records if the name is spelled differently in the two tables. Chapters 5 and 10 of this textbook teach specific techniques for standardizing formatted data before analysis.

### Outliers

Outliers are values that fall far outside the expected range for a given field. A single invoice for $2,000,000 in a dataset where the average invoice is $5,000 may be a legitimate large transaction, or it may be a data entry error where extra zeros were added accidentally. A journal entry posted at 3:00 AM may be a legitimate automated posting, or it may indicate unauthorized activity. Outliers require investigation rather than automatic removal. The appropriate response depends on the context and on the accountant's professional judgment.

In audit analytics, outliers are often the transactions of greatest interest. Auditors look for unusual transactions because they may indicate errors, fraud, or control failures. The statistical and analytical techniques covered in later chapters, including stratification in Chapter 6, Benford's Law analysis in Chapter 8, and anomaly detection queries in Chapter 12, are all designed to help you identify and evaluate outliers systematically.

*[Figure 2.3: Common Data Quality Problems Illustrated. A four-panel diagram with one panel for each problem type (Missing Values, Duplicates, Inconsistent Formatting, Outliers). Each panel shows a small sample of data with the problem highlighted and a brief annotation explaining what is wrong. The examples use Northwind-style data to maintain continuity with the textbook datasets.]*

> **[IN PRACTICE]**
> In professional practice, data quality assessment is often the first task in any analytics engagement. Audit teams perform data quality checks before running analytical procedures to ensure that the results will be reliable. Management accountants validate the data behind cost reports before presenting them to executives. The AICPA's Guide to Audit Data Analytics recommends that auditors evaluate the completeness and accuracy of data obtained from client systems before using it in substantive procedures (AICPA, 2017). The data quality skills you develop in this chapter apply directly to that professional requirement.


## The Concept of Tidy Data

In 2014, the statistician Hadley Wickham published a paper that formalized a set of principles for organizing datasets in a way that makes them easy to analyze. He called datasets that follow these principles "tidy" and those that violate them "messy" (Wickham, 2014). The concept of tidy data has since become widely adopted in data analysis across many fields, and it is directly relevant to accounting analytics.

A tidy dataset has three properties. First, each variable occupies its own column. A variable is any attribute that is measured or recorded, such as transaction date, account number, or debit amount. Second, each observation occupies its own row. An observation is a single instance of what is being measured, such as one line item in a journal entry or one sales transaction. Third, each type of observational unit forms its own table. Customer information belongs in a customer table, order information belongs in an order table, and product information belongs in a product table.

These principles may seem obvious, but violations are surprisingly common in accounting data. A frequent violation is storing multiple variables in a single column. For example, a spreadsheet might have a column called "Account" that contains entries like "4100-Sales-Domestic" where the account number, account name, and geographic segment are all packed into one field. Analyzing sales by geographic segment requires splitting this column into three separate columns before any aggregation can be performed.

Another common violation is storing observations in column headers rather than in rows. A budget spreadsheet might have columns labeled "January," "February," "March," and so on, with each row representing a department and the values representing that department's budgeted amount for each month. This layout is easy for humans to read but difficult for analytical tools to process. A tidy version of the same data would have three columns (Department, Month, and Budget Amount) with one row for each department-month combination. This format, sometimes called "long" format as opposed to the "wide" format of the original, is what PivotTables, SQL GROUP BY queries, and Power BI data models require.

*[Figure 2.4: Messy Versus Tidy Data. A side-by-side comparison showing the same budget data in two layouts. The left panel shows the "wide" format with months as column headers (messy). The right panel shows the "long" format with Department, Month, and Budget Amount as columns (tidy). Annotations explain why the tidy format is preferred for analysis.]*

> **[WATCH OUT]**
> Students sometimes confuse "tidy" with "clean." A tidy dataset is one that follows the structural principles described above: each variable in its own column, each observation in its own row, each type of observational unit in its own table. A clean dataset is one that is free of quality problems such as missing values, duplicates, and inconsistencies. A dataset can be tidy but dirty (properly structured but containing errors) or clean but messy (free of errors but organized in a way that makes analysis difficult). Both structure and quality must be addressed before analysis can proceed.

The three textbook datasets are, for the most part, already tidy. They are stored as relational database tables where each column represents a single variable and each row represents a single observation. This is by design: relational databases enforce the structural principles of tidy data because their table definitions require each column to have a name, a data type, and a single purpose. When you import these datasets into Excel, however, you may encounter situations where the data needs to be restructured, particularly when working with summary reports that were designed for human readers rather than analytical tools. Chapter 5 introduces Power Query, which provides a systematic way to reshape data from messy to tidy formats.

> **[CONNECTING THE DOTS]**
> The tidy data principles described here are closely related to the concept of database normalization, which you will study in Chapter 3. Both tidy data and normalization seek to organize data so that each fact is stored once, in a single defined location, with no redundancy or ambiguity. Understanding tidy data now will make the transition to relational database concepts in the next chapter feel natural.


## Mapping the Textbook Datasets to Real-World Data Sources

The three datasets used in this textbook represent different types of accounting data environments, and understanding how they map to real-world sources will help you apply the concepts from this chapter in practice.

The Northwind Traders dataset represents the type of data you would find in a small company's order management system. It records sales transactions, customer information, product details, and supplier records. In a real company of similar size, this data might reside in a standalone accounting package or a small-business ERP system. The data is relatively simple: a few hundred customers, a few thousand orders, and straightforward relationships between tables. Northwind does not include a general ledger or a chart of accounts, which means it cannot support financial statement preparation on its own. It functions as a sub-ledger system focused on the revenue and purchasing cycles.

The AdventureWorks Cycles dataset represents the type of data you would find in a mid-size manufacturing company's departmental databases. It includes tables for sales, production, purchasing, and human resources, each organized within its own schema (a logical grouping of related tables within a database). In a real company, these data might come from separate modules within an ERP system or from several integrated applications. The AdventureWorks data is more complex than Northwind because it captures manufacturing processes, including work orders, bills of materials, production routing, and scrap records. This complexity introduces additional data quality challenges, such as ensuring that cost records are consistent across the production and accounting modules.

The ERPNext Demo Company dataset represents the type of data you would find in a full enterprise resource planning system with an integrated accounting module. It includes a chart of accounts, general ledger entries, journal entries, sales and purchase invoices, cost centers, and budget records. In a real company, this data would serve as the authoritative source for financial reporting. The ERPNext dataset is the most accounting-rich of the three, and it mirrors the data structures that auditors and financial analysts encounter when working with production ERP systems. The general ledger entries in ERPNext record every debit and credit that affects the financial statements, and the chart of accounts provides the classification structure that organizes those entries into meaningful categories.

*[Table 2.3: Mapping Textbook Datasets to Real-World Data Sources. A table with four columns (Feature, Northwind Traders, AdventureWorks Cycles, ERPNext Demo Company) and five rows (Real-World Equivalent, Accounting Module Depth, Primary Data Quality Challenges, Most Relevant For, Chapters Where Quality Issues Are Explored). Each cell contains a brief description.]*

Understanding these mappings helps you connect the exercises in this textbook to the data environments you will encounter after graduation. When you clean and validate Northwind order data in the tutorials that follow, you are practicing the same skills you would use when working with transaction exports from a client's accounting system. When you assess the completeness and consistency of ERPNext general ledger data, you are performing the same type of evaluation that an audit team performs at the start of every engagement.


## Guided Tutorial 2.1: Inspecting the Northwind Dataset for Data Quality Problems

**Context and objective.** In this tutorial, you will examine the Northwind dataset in Excel and identify specific data quality problems across several tables. The goal is to practice applying the four quality dimensions (accuracy, completeness, consistency, and timeliness) to a real dataset and to document what you find. This tutorial connects to the opening scenario by showing you how a data quality assessment works in practice.

**Prerequisites.** You need Microsoft Excel installed on your computer and access to the Northwind.xlsx file provided with this textbook.

**Step-by-step instructions.**

**Step 1.** Open Northwind.xlsx in Excel and click on the Orders worksheet. Scroll across the columns to familiarize yourself with the available fields. You should see columns including OrderID, CustomerID, EmployeeID, OrderDate, RequiredDate, ShippedDate, ShipVia, Freight, ShipName, ShipAddress, ShipCity, ShipRegion, ShipPostalCode, and ShipCountry.

**Step 2.** Click on the ShippedDate column header to select the entire column. Use Excel's Find and Select feature (Ctrl+F on Windows, Cmd+F on Mac) to search for blank cells, or use the filter dropdown to look for blanks. Count the number of orders that have no ShippedDate value. These missing values represent a completeness problem: orders that were placed but for which no shipment date was recorded. Record the count.

*[Figure 2.5: Screenshot of the Northwind Orders table in Excel with the ShippedDate column filtered to show blank cells. An annotation highlights the missing values and identifies this as a completeness problem.]*

**Step 3.** With the Orders worksheet still active, examine the ShipRegion column using the same approach. Filter for blank values. You will find that many orders have no value in the ShipRegion field. Consider whether this represents a true completeness problem (the data should exist but was not entered) or whether some countries do not use region designations. This distinction matters because the appropriate response differs. If the data should exist, it needs to be obtained. If the field is not applicable for certain records, the blank is acceptable.

**Step 4.** Click on the Customers worksheet. Examine the CompanyName column. Look for potential consistency problems by scanning for variations in how company names are formatted. Check whether any company names appear to be near-duplicates (similar names with slight differences in punctuation, abbreviation, or spacing). You can sort the column alphabetically to make near-duplicates easier to spot.

**Step 5.** Return to the Orders worksheet. Create a simple check for potential accuracy problems by examining the Freight column. Sort the Freight column from largest to smallest. Examine the highest values. Are any freight amounts unusually large relative to the others? Make a note of any values that appear to be outliers. In a real engagement, you would investigate these further to determine whether they are legitimate transactions or data entry errors.

**Step 6.** Examine the relationship between OrderDate, RequiredDate, and ShippedDate. For records that have all three dates populated, check whether the dates are in a logical sequence: OrderDate should come first, followed by ShippedDate, and RequiredDate should not precede OrderDate. You can create a simple formula in a new column to test this. In cell P2, enter a formula that returns "Check" if ShippedDate is earlier than OrderDate, and "OK" otherwise. Copy the formula down the column and filter for any "Check" results. These would indicate a potential accuracy problem in the date fields.

*[Figure 2.6: Screenshot showing a helper column added to the Northwind Orders table that flags records where ShippedDate precedes OrderDate. The formula is visible in the formula bar, and the annotation identifies this as an accuracy check.]*

**Step 7.** Click on the Products worksheet. Examine the UnitPrice column. Sort by UnitPrice from smallest to largest. Check whether any products have a unit price of zero, which could indicate a missing value recorded as zero rather than left blank. Also check the UnitsInStock column for any negative values, which would be physically impossible and would represent an accuracy problem.

**Checkpoint.** At this point, you should have identified at least three specific data quality problems in the Northwind dataset: missing ShippedDate values (completeness), potential inconsistencies in company names or regional data (consistency), and at least one instance worth investigating further in the date sequence or freight amounts (accuracy). You should have a written list of findings, noting the table, the column, the type of problem, and the number of affected records. This list is a simple version of the data quality assessment that auditors perform at the start of every analytics engagement.


## Guided Tutorial 2.2: Examining ERPNext General Ledger Data for Completeness and Consistency

**Context and objective.** In this tutorial, you will examine the ERPNext dataset to assess whether the general ledger entries and chart of accounts are complete and consistent. This is a more accounting-specific data quality assessment than the Northwind tutorial, because it involves checking whether the accounting records themselves are internally coherent. The skills practiced here connect directly to the audit procedures you will learn in Chapter 8 and Chapter 12.

**Prerequisites.** You need Microsoft Excel installed on your computer, access to the ERPNext.xlsx file, and completion of Tutorial 2.1.

**Step-by-step instructions.**

**Step 1.** Open ERPNext.xlsx in Excel and click on the Account worksheet (the chart of accounts). Examine the columns available. You should see fields including account name, account number or code, account type (such as Asset, Liability, Equity, Income, or Expense), and a parent account field that defines the account hierarchy. Scroll through the list to get a sense of how many accounts exist and how they are organized.

**Step 2.** Check the chart of accounts for completeness. Every account type should be represented. Sort or filter the account type column and verify that the chart includes accounts classified as assets, liabilities, equity, income, and expenses. If any major category is missing, that is a completeness problem. Record your findings.

**Step 3.** Click on the GLEntry worksheet (the general ledger). Examine the columns available. You should see fields including a posting date, an account reference, debit and credit amounts, a voucher type (indicating the source document, such as "Journal Entry" or "Sales Invoice"), and a voucher number. Scroll down to get a sense of the volume of data.

**Step 4.** Check the general ledger for a fundamental accounting consistency requirement: for every transaction, total debits should equal total credits. To test this at the aggregate level, use the SUM function to calculate the total of the Debit column and the total of the Credit column. The two totals should be equal, or very nearly so (small differences may arise from rounding). If there is a significant difference, that indicates a serious consistency problem in the ledger.

*[Figure 2.7: Screenshot of the ERPNext GLEntry worksheet with SUM formulas calculating total debits and total credits at the bottom of the respective columns. An annotation highlights the comparison and explains that equal totals confirm the basic debit-equals-credit consistency of the ledger.]*

**Step 5.** Check for accounts referenced in the general ledger that do not exist in the chart of accounts. This is a consistency check between two related tables. To perform this check manually, use the COUNTIFS function. In a new column adjacent to the GLEntry data, enter a formula that counts how many times the account value in the current GL row appears in the Account worksheet's account column. If any GLEntry row returns a count of zero, that means the entry references an account that does not exist in the chart of accounts, which is a consistency problem. Scan for any zeros and record the affected entries.

**Step 6.** Examine the PostingDate column in the GLEntry worksheet. Sort by posting date and check the date range. Note the earliest and latest dates. Check whether there are any gaps in the sequence of months, which could indicate missing periods. Also check whether any entries have dates that fall outside the expected fiscal year, which would be an accuracy concern.

**Step 7.** Examine the Debit and Credit columns for missing or unusual values. Filter for rows where both the Debit and Credit fields are zero or blank. An entry with no debit and no credit amount serves no accounting purpose and may indicate a data entry error or a system artifact. Record the count of such entries if any exist.

**Checkpoint.** At this point, you should have assessed the ERPNext data against three quality dimensions: completeness (all account types present in the chart of accounts, no gaps in the posting date range), consistency (debits equal credits in the aggregate, all GL accounts exist in the chart of accounts), and accuracy (no entries outside the expected date range, no zero-amount entries without explanation). Your findings should be documented in a brief written list that identifies each test performed, the result, and any issues discovered. This exercise previews the audit analytics work you will perform in Chapters 8 and 12, where you will use SQL to automate these same tests across the entire population.


## Looking Ahead

This chapter has provided the vocabulary and the framework you need to think critically about accounting data before you begin analyzing it. You can now distinguish between quantitative and qualitative data, between structured and unstructured data, and between data that is tidy and data that needs restructuring. You know the primary sources of accounting data and the four dimensions against which data quality is measured. You have practiced inspecting two of the textbook datasets for specific quality problems and documenting your findings.

In the next chapter, you will build on this foundation by studying how accounting data is organized within relational databases. Chapter 3 introduces the concepts of tables, keys, and relationships that make it possible to connect data across different parts of an accounting system. Understanding these structures will prepare you for the SQL chapters in Part III and for the data modeling work you will do in Power BI in Part IV.

---

## Chapter Summary

Every accounting analytics project depends on the quality of the data that feeds it. Before applying any analytical technique, accountants must understand what types of data they are working with, where the data came from, and whether it is fit for the intended purpose. This chapter established the conceptual foundation for that assessment.

Accounting data can be classified along two dimensions. The quantitative versus qualitative distinction determines whether arithmetic operations are appropriate. The structured versus unstructured distinction determines which analytical tools can be applied. The datasets used in this textbook contain structured data organized in rows and columns, which is the format required by Excel, SQL, and Power BI. Accounting data originates from general ledgers, sub-ledgers, trial balances, enterprise resource planning systems, and external sources. Each source has characteristic strengths and limitations that affect data quality.

Data quality is assessed along four dimensions: accuracy, completeness, consistency, and timeliness. Accuracy means that recorded values correspond to true values. Completeness means that all expected records and fields are present. Consistency means that the same fact is represented the same way wherever it appears. Timeliness means that the data reflects the relevant reporting period. Common data quality problems include missing values, duplicate records, inconsistent formatting, and outliers. Each of these problems can distort analytical results if not identified and addressed before analysis begins.

The concept of tidy data provides a structural standard for how datasets should be organized: each variable in its own column, each observation in its own row, and each type of observational unit in its own table. Tidy data is easier to analyze than messy data because it aligns with the input requirements of PivotTables, SQL queries, and Power BI data models. The three textbook datasets follow tidy principles because they are stored as relational database tables, but real-world data often requires restructuring before it reaches this standard.

The practical skills introduced in the two guided tutorials, inspecting the Northwind dataset for missing values, date inconsistencies, and outliers, and examining the ERPNext general ledger for completeness and consistency, represent the first steps in a data quality assessment process that you will apply throughout this textbook and throughout your career.

---

## Key Terms

**Accuracy.** A data quality dimension indicating that recorded values correspond to the true values they are intended to represent. In accounting, accuracy problems include data entry errors, misclassifications, and incorrect calculations.

**Completeness.** A data quality dimension indicating that all expected records and field values are present in the dataset. Missing transactions, blank fields, and omitted time periods are examples of completeness problems.

**Consistency.** A data quality dimension indicating that the same fact is represented in the same way wherever it appears in a dataset or across related datasets. Inconsistent customer names, account codes, or date formats are common consistency problems.

**Data quality.** The degree to which a dataset is fit for its intended use, assessed across multiple dimensions including accuracy, completeness, consistency, and timeliness.

**Duplicate record.** A record that appears more than once in a dataset, representing the same underlying transaction, entity, or event. Duplicate payments and duplicate customer entries are common examples in accounting data.

**External data.** Data originating from outside the organization, such as bank statements, market price feeds, credit ratings, and industry benchmarks. External data introduces additional quality concerns because the accountant has less control over how it was collected and formatted.

**General ledger.** The central repository of an organization's financial transactions, containing debit and credit entries organized by account. In the ERPNext dataset, the general ledger is stored in the GLEntry table.

**Missing value.** A field within a record that is blank, null, or contains a placeholder rather than a substantive value. Missing values represent a completeness problem and can distort calculations if not handled properly.

**Outlier.** A data value that falls far outside the expected range for its field. Outliers may represent legitimate unusual transactions or data entry errors and require investigation to determine the appropriate treatment.

**Qualitative data.** Data consisting of categories, labels, or descriptions rather than numerical measurements. Account names, transaction descriptions, and vendor classifications are examples of qualitative data in accounting.

**Quantitative data.** Data consisting of numerical values that represent measurements or counts and that can be subjected to arithmetic operations. Transaction amounts, unit quantities, and financial ratios are examples of quantitative data in accounting.

**Semi-structured data.** Data that has some organizational elements but does not fit neatly into rows and columns. XBRL filings and PDF bank statements are examples relevant to accounting.

**Structured data.** Data organized into a predefined format of rows and columns, where each column has a defined data type. All three textbook datasets contain structured data.

**Sub-ledger.** A detailed record for a specific category of accounts that feeds summary totals to the general ledger. The accounts receivable sub-ledger and accounts payable sub-ledger are common examples.

**Tidy data.** A dataset organized so that each variable occupies its own column, each observation occupies its own row, and each type of observational unit forms its own table. Tidy data aligns with the input requirements of analytical tools such as PivotTables, SQL, and Power BI.

**Timeliness.** A data quality dimension indicating that the data reflects the current state of the business as of the relevant reporting date. Data that is not current enough for the intended analysis has a timeliness problem.

**Unstructured data.** Data that lacks a predefined tabular format, such as the text of contracts, email correspondence, or scanned invoice images.

---

## Multiple Choice Questions

**1.** A transaction amount of $15,000 is recorded in the general ledger as $1,500 due to a data entry error. This is an example of a problem with which data quality dimension?

A. Completeness
B. Timeliness
C. Accuracy
D. Consistency

**2.** An auditor discovers that 47 orders in a sales database have no value in the ShippedDate field. This situation represents a problem with which data quality dimension?

A. Accuracy
B. Completeness
C. Consistency
D. Timeliness

**3.** A company's accounts receivable sub-ledger records a customer as "Johnson & Johnson Inc." while the payment records list the same customer as "Johnson and Johnson." An analyst attempting to match payments to receivables will encounter errors because of this difference. This is an example of a problem with which data quality dimension?

A. Accuracy
B. Completeness
C. Consistency
D. Timeliness

**4.** Which of the following is an example of qualitative data in an accounting context?

A. The total amount of a sales invoice
B. The number of units of inventory on hand
C. The name of the cost center to which an expense is assigned
D. The gross profit margin expressed as a percentage

**5.** According to the concept of tidy data, a budget spreadsheet with months as column headers (January, February, March) and departments as rows is considered "messy" because it violates which tidy data principle?

A. Each variable should occupy its own column
B. Each observation should occupy its own row
C. Each type of observational unit should form its own table
D. Both A and B

**6.** An auditor is performing analytical procedures using general ledger data extracted from the client's ERP system on March 15 for a fiscal year ending December 31. The data includes all adjusting entries through March 10 but not the final three adjusting entries posted on March 12. This situation represents a concern about which data quality dimension?

A. Accuracy
B. Completeness
C. Consistency
D. Timeliness

**7.** Which of the following best describes the relationship between structured and unstructured data in accounting practice?

A. Accountants work exclusively with structured data and never encounter unstructured data.
B. Most accounting analytical work uses structured data, but the proportion of unstructured data in accounting is growing.
C. Unstructured data has replaced structured data as the primary input for accounting analytics.
D. Structured and unstructured data require the same analytical tools and techniques.

**8.** A management accountant discovers that the same product appears in the inventory database under two different product codes because it was entered separately by two warehouse locations. This is an example of which data quality problem?

A. Missing value
B. Outlier
C. Duplicate record
D. Timeliness problem

**9.** Which of the following sources of accounting data provides the most complete picture of an organization's financial transactions?

A. The accounts receivable sub-ledger
B. The general ledger
C. An external bank statement
D. A product inventory listing

**10.** The ERPNext dataset is described as the most "accounting-rich" of the three textbook datasets. Which feature primarily distinguishes it from Northwind and AdventureWorks?

A. It contains sales transaction data.
B. It includes a chart of accounts, general ledger entries, journal entries, and a complete accounting module.
C. It contains more tables than the other two datasets combined.
D. It records data in an unstructured format.

**11.** A dataset is organized so that each variable occupies its own column and each observation occupies its own row, but several records contain data entry errors in the amount field. This dataset is best described as:

A. Tidy and clean
B. Tidy but not clean
C. Clean but not tidy
D. Neither tidy nor clean

**12.** A financial analyst creates a revenue summary using a SQL query that groups sales by customer name. The query returns 150 distinct customers, but the company's customer master file contains only 142 customers. The most likely explanation for the discrepancy is:

A. The SQL query contains a syntax error.
B. Some customers made purchases but were never entered into the customer master file.
C. Inconsistent formatting of customer names caused the same customer to appear under multiple name variations.
D. The customer master file is more current than the sales data.

**13.** An enterprise resource planning system is distinct from a standalone accounting package primarily because an ERP system:

A. Uses a relational database to store data
B. Integrates data from multiple functional areas such as sales, production, purchasing, and human resources into a single database
C. Produces financial statements automatically
D. Eliminates all data quality problems through built-in validation rules

**14.** Which of the following best explains why data quality assessment should be performed before any analysis begins?

A. Software tools cannot process data that contains quality problems.
B. Data quality problems can cause analytical results to be unreliable or misleading, and identifying problems in advance allows the accountant to address them.
C. Professional standards prohibit accountants from using any data that contains missing values.
D. Data quality assessment is only required for auditing engagements and not for managerial accounting or financial reporting.

**15.** An auditor finds that a general ledger entry references account code "5200" but this code does not appear anywhere in the company's chart of accounts. This finding represents a problem with:

A. Accuracy only
B. Completeness only
C. Consistency between the general ledger and the chart of accounts
D. Timeliness of the chart of accounts

---

## Applied Exercises

### Financial Accounting Exercises

**Exercise 2.1 (Financial Accounting): Assessing Revenue Data Quality in Northwind**

**Dataset:** Northwind (Orders, OrderDetails, Products, Customers)

**Scenario.** You are a financial reporting analyst preparing to analyze Northwind Traders' revenue for the most recent fiscal year. Before building any reports, you need to verify that the underlying sales data is reliable enough to support accurate revenue figures.

**Requirements.** (1) Open the Northwind dataset in Excel and examine the Orders, OrderDetails, Products, and Customers tables. For each table, identify and document any data quality problems you observe, classifying each problem by quality dimension (accuracy, completeness, consistency, or timeliness). (2) Assess whether the OrderDetails table contains the information needed to calculate revenue for each order. Identify the columns involved and note any values that appear problematic (such as zero or negative quantities, missing prices, or discount values outside the expected zero-to-one range). (3) Examine whether every CustomerID in the Orders table corresponds to a customer in the Customers table. Use COUNTIFS or VLOOKUP to test this relationship. Document any orphaned records where an order references a customer that does not exist. (4) Prepare a brief written data quality assessment memorandum (one page) that summarizes your findings and recommends whether the data is suitable for revenue reporting or whether specific problems must be resolved first.

**Deliverable.** A one-page data quality assessment memorandum with specific findings organized by quality dimension.


**Exercise 2.2 (Financial Accounting): Evaluating General Ledger Completeness in ERPNext**

**Dataset:** ERPNext (GLEntry, Account)

**Scenario.** You are a financial reporting analyst who has been asked to verify that the ERPNext general ledger is complete before the team begins preparing the year-end financial statements. Your supervisor is concerned that some transactions may not have been posted.

**Requirements.** (1) Open the ERPNext dataset and examine the GLEntry table. Calculate the total debits and total credits across all entries. Determine whether the ledger is in balance. (2) Identify the date range covered by the general ledger entries. Check whether entries are present for every month within the fiscal year. Note any months that appear to have an unusually low number of entries compared to other months, which could indicate missing transactions. (3) Examine the voucher type column to understand what types of transactions are recorded. Determine whether the ledger includes entries from all expected source types (such as journal entries, sales invoices, purchase invoices, and payment entries). If any expected source type is absent, document this as a potential completeness concern. (4) Write a brief assessment (one page) of the general ledger's completeness, suitable for review by the financial reporting manager.

**Deliverable.** A one-page completeness assessment memorandum with quantitative evidence supporting each finding.


### Managerial Accounting Exercises

**Exercise 2.3 (Managerial Accounting): Data Quality Assessment for Cost Analysis**

**Dataset:** AdventureWorks (Product, WorkOrder)

**Scenario.** You are a cost analyst who has been asked to perform a product cost analysis using AdventureWorks manufacturing data. Before starting the analysis, you need to assess whether the data is clean enough to produce reliable cost figures.

**Requirements.** (1) Open the AdventureWorks dataset in Excel and examine the Product table. Identify any products where the StandardCost field is zero, blank, or appears unreasonable. Assess whether these entries represent data quality problems or legitimate situations (such as products that have been discontinued and are no longer costed). (2) Compare the StandardCost and ListPrice columns. Identify any products where the ListPrice is less than the StandardCost, which would imply a negative margin. Determine whether these represent accuracy problems or deliberate pricing decisions. (3) Examine the WorkOrder table if available. Check for missing values in key fields such as quantity ordered, quantity produced, and dates. (4) Write a brief assessment (one half to one page) of the data's suitability for product cost analysis, identifying any problems that would need to be resolved before proceeding.

**Deliverable.** A written data quality assessment focused on cost analysis readiness, with specific product-level findings.


**Exercise 2.4 (Managerial Accounting): Identifying Tidy Data Problems in Budget Reports**

**Dataset:** ERPNext (Budget, CostCenter, or equivalent tables)

**Scenario.** You are a management accountant who needs to compare budgeted amounts to actual spending by cost center. The budget data is available in the ERPNext system, but you suspect it may not be in a format suitable for analysis.

**Requirements.** (1) Open the ERPNext dataset and locate any budget-related tables. Examine the structure. Determine whether the budget data follows tidy data principles (each variable in its own column, each observation in its own row). If not, describe specifically which tidy data principle is violated and how the data would need to be restructured. (2) Examine the cost center references in the budget data and in the GLEntry table. Assess whether the cost center names or codes are consistent between the two sources. Identify any inconsistencies that would prevent a straightforward comparison. (3) Document your findings in a brief memorandum (one half to one page) that recommends specific data preparation steps needed before a budget-versus-actual analysis can be performed.

**Deliverable.** A written memorandum identifying structural and quality issues in the budget data and recommending preparation steps.


### Auditing Exercises

**Exercise 2.5 (Auditing): Data Quality Evaluation for Audit Planning**

**Dataset:** Northwind (Orders, OrderDetails, Customers, Suppliers) and ERPNext (GLEntry, Account, PaymentEntry)

**Scenario.** You are a first-year auditor assigned to evaluate the data that will be used for analytics procedures during the upcoming audit. Your senior has asked you to perform a preliminary data quality assessment of both the Northwind and ERPNext datasets to determine which data sources are reliable enough for audit testing.

**Requirements.** (1) For the Northwind dataset, perform the following data quality checks on the Orders and OrderDetails tables: test for missing values in critical fields (OrderDate, CustomerID, UnitPrice, Quantity), test for records where ShippedDate precedes OrderDate, and check for order line items with quantities of zero or negative values. Document the number of records affected by each problem. (2) For the ERPNext dataset, perform the following checks on the GLEntry and PaymentEntry tables: verify that total debits equal total credits in the general ledger, check for payment entries with missing dates or missing vendor references, and test for duplicate entries by looking for records that match on date, amount, and account. (3) For each problem identified, classify it by quality dimension and assess its potential impact on audit procedures. A missing date, for example, would prevent the auditor from testing the transaction in the correct period. (4) Prepare a one-page audit data quality assessment memorandum that your senior could use to decide which datasets and tables are suitable for audit analytics.

**Deliverable.** A one-page audit data quality assessment memorandum organized by dataset and quality dimension.


**Exercise 2.6 (Auditing): Testing for Duplicate Records**

**Dataset:** ERPNext (PaymentEntry or equivalent payment table)

**Scenario.** Your audit team has identified duplicate payments as a risk area for the current engagement. Before performing a full duplicate payment analysis (which you will learn in Chapter 12 using SQL), you have been asked to perform a preliminary manual check using Excel.

**Requirements.** (1) Open the ERPNext dataset and locate the payment-related table(s). Identify the fields that would be relevant for detecting duplicate payments, such as vendor or payee, amount, and date. (2) Sort the data by payee and then by amount to bring potential duplicates into adjacent rows. Scan for records where the same payee received the same amount on the same date or within a narrow date range. Document any potential duplicates you identify. (3) Assess the reliability of your manual approach. Consider what limitations exist when searching for duplicates by visual inspection versus using automated techniques. Write two to three sentences explaining why a SQL-based approach (which you will learn later in the book) would be more effective for this task. (4) Prepare a brief memorandum (one half page) documenting the potential duplicates identified and your assessment of the method's limitations.

**Deliverable.** A written memorandum documenting potential duplicate payments and the limitations of manual detection methods.

---

## Further Reading

Wang, R. Y., and Strong, D. M. (1996). Beyond accuracy: What data quality means to data consumers. *Journal of Management Information Systems*, 12(4), 5-33. This paper established the foundational framework for understanding data quality as a multidimensional concept defined by the needs of data users. The four quality dimensions discussed in this chapter (accuracy, completeness, consistency, and timeliness) draw on this framework, and the paper remains essential reading for anyone who works with data quality assessment in any professional context.

Wickham, H. (2014). Tidy data. *Journal of Statistical Software*, 59(10), 1-23. This paper formalized the principles of tidy data that are discussed in this chapter. Although the examples use the R programming language, the structural principles apply to any data analysis environment, including Excel, SQL, and Power BI. The paper's clear explanation of why each variable should occupy its own column and each observation its own row is directly relevant to the data preparation challenges students will encounter throughout this textbook.

Grabski, S. V., Leech, S. A., and Schmidt, P. J. (2011). A review of ERP research: A future agenda for accounting information systems. *Journal of Information Systems*, 25(1), 37-78. This review paper examines the research literature on enterprise resource planning systems and their implications for accounting. It provides useful context for understanding the role of ERP systems as data sources in accounting analytics and discusses the data quality challenges that arise within ERP environments.

Redman, T. C. (2001). *Data quality: The field guide.* Digital Press. This practitioner-oriented book provides a comprehensive treatment of data quality concepts, assessment methods, and improvement strategies. Although it addresses data quality broadly rather than in an accounting-specific context, the practical techniques it describes for identifying and resolving data quality problems are directly applicable to the exercises in this chapter and throughout the textbook.

AICPA (American Institute of Certified Public Accountants). (2017). *Guide to audit data analytics.* AICPA. This professional guidance document describes how auditors should use data analytics in audit engagements, including specific recommendations for evaluating the reliability and completeness of data before performing analytical procedures. The guide's discussion of data quality evaluation aligns with the quality dimensions covered in this chapter and supports the audit-oriented exercises throughout the textbook.

Fisher, I. E., Garnsey, M. R., and Hughes, M. E. (2016). Natural language processing in accounting, auditing and finance: A synthesis of the literature with a roadmap for future research. *Intelligent Systems in Accounting, Finance and Management*, 23(3), 157-214. This paper reviews the emerging application of natural language processing to unstructured accounting data such as contracts, disclosures, and regulatory filings. It provides useful context for the brief discussion of unstructured data in this chapter and points toward the emerging technologies covered in Chapter 20.

Bovee, M., Srivastava, R. P., and Mak, B. (2003). A conceptual framework and belief-function approach to assessing overall information quality. *International Journal of Intelligent Systems*, 18(1), 51-74. This paper presents a formal framework for assessing information quality that extends the foundational work of Wang and Strong. The paper's approach to evaluating quality dimensions is relevant to the data quality assessment exercises in this chapter, particularly for students interested in the theoretical underpinnings of data quality measurement.

Dai, J., and Vasarhelyi, M. A. (2017). Toward blockchain-based accounting and assurance. *Journal of Information Systems*, 31(3), 5-21. While this paper focuses primarily on blockchain technology, it includes a useful discussion of how data integrity and quality assurance are handled in current accounting information systems versus emerging distributed ledger approaches. It provides forward-looking context that connects the data quality concepts in this chapter to the emerging technologies discussed in Chapter 20.
