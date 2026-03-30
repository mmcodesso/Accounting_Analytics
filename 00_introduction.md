---
number-sections: false
format:
  html:
    number-sections: false
---

# Introduction {.unnumbered}

## About This Book

This textbook is designed for undergraduate and graduate accounting and business students who need a practical introduction to analytics without assuming prior programming experience. The goal is not simply to teach software features. The goal is to help students ask better questions, work effectively with accounting data, and communicate findings in forms that support financial reporting, managerial decision-making, and audit assurance.

The book is built around a single integrated toolkit. Students learn to move from spreadsheet-based analysis in Excel, to direct database access in SQL, to interactive reporting in Power BI. That sequence mirrors how analytics work often unfolds in practice: data is extracted, prepared, analyzed, and then presented to decision makers in a format they can actually use.

---

## About the Datasets

This textbook is built around three real-world-style databases that students will use throughout the entire book. All three datasets are provided in both Excel workbook format and SQLite database format, allowing students to work with the same data across all three tools (Excel, SQL, and Power BI).

**Northwind Traders** is a small wholesale food distribution company. Its database contains tables for customers, orders, order details, products, product categories, suppliers, employees, and shippers. Northwind is compact and easy to understand, making it the primary dataset for foundational chapters. Students will use it to learn basic sales analysis, customer analytics, purchasing evaluation, and inventory review. Because it represents a simple trading company, it is well suited for introducing core concepts without overwhelming students with complexity.

**Adventure Works Cycles** is a mid-size multinational bicycle manufacturer. Its database contains approximately 70 tables organized across five functional areas: Sales, Production, Purchasing, Human Resources, and Person. Adventure Works includes manufacturing cost data (bills of materials, work orders, routing, scrap tracking), multi-territory sales operations, vendor management, and employee department histories. This dataset introduces the complexity students will encounter in manufacturing and multi-division organizations. It supports exercises in cost accounting, production analysis, sales performance evaluation, and organizational analytics.

**ERPNext Demo Company** is a full enterprise resource planning environment with a complete accounting module. Its database includes a chart of accounts, general ledger entries, journal entries, sales and purchase invoices, cost centers, budgets, payment entries, bank reconciliation records, stock ledger entries, and asset registers. ERPNext provides the most accounting-rich environment of the three datasets. Students will use it for financial statement preparation, general ledger analysis, budgetary control, audit testing, and integrated reporting. Because ERPNext mirrors the structure of a production ERP system, students also gain familiarity with the kind of data environment they will encounter in professional practice.

**Dataset Progression Strategy:** The book introduces Northwind first because it is the simplest. AdventureWorks enters in the middle chapters as exercises grow more complex. ERPNext appears once students have enough analytical skill to work with a full accounting system. By the final chapters, students move fluently across all three datasets in integrated exercises.

**Pedagogical Structure of Each Chapter:** Every chapter follows a consistent structure. Each one opens with a set of learning objectives and a brief motivating scenario drawn from one of the three datasets. The body of the chapter presents concepts through narrative explanation, worked examples, and step-by-step guided exercises. Each chapter closes with a summary, key terms, review questions, and three sets of applied exercises organized by accounting perspective: Financial Accounting, Managerial Accounting, and Auditing. Not every chapter will have equal weight across all three perspectives, but the consistent structure ensures students see how the same analytical techniques serve different purposes depending on the role.

---

## PART I: FOUNDATIONS OF ACCOUNTING ANALYTICS

### Chapter 1: The Role of Analytics in Accounting

This chapter establishes why analytics matters in the accounting profession. It traces the evolution from manual bookkeeping to data-driven decision making and positions analytics as a core competency rather than an optional skill. The chapter introduces the three types of analytics (descriptive, predictive, and prescriptive) and illustrates each one with examples drawn from the three datasets used in this book. Students also learn how professional bodies such as the AICPA and IMA have integrated data analytics into their competency frameworks.

**Topics covered:** The changing landscape of accounting work. Descriptive, predictive, and prescriptive analytics defined and applied. The demand for analytics skills in audit, tax, managerial, and advisory roles. Overview of tools used in this textbook (Excel, SQL, Power BI). Introduction to the three companion datasets (Northwind, AdventureWorks, ERPNext). How this book is organized and how to use it effectively.

**Dataset:** Students receive all three datasets and explore each one at a high level, examining the number of tables, the types of transactions recorded, and the business context behind each company. No analysis is performed yet; the goal is orientation and familiarity.

---

### Chapter 2: Understanding Data in Accounting

This chapter teaches students to think critically about accounting data before they begin any analysis. It covers data types (quantitative and qualitative, structured and unstructured), common data sources in accounting (general ledgers, sub-ledgers, trial balances, ERP systems, external feeds), and the concept of data quality. Students use the Northwind and ERPNext datasets to identify common data problems such as missing values, duplicates, inconsistent formatting, and outliers. The chapter emphasizes that every analytical result depends on the quality and appropriateness of the underlying data.

**Topics covered:** Data types and structures relevant to accounting. Sources of accounting data including ERP systems, spreadsheets, and external databases. Data quality dimensions (accuracy, completeness, consistency, timeliness). The concept of tidy data and why it matters. Mapping the three textbook datasets to real-world accounting data sources.

**Dataset focus:** Northwind (inspecting the orders, products, and customers tables for data quality) and ERPNext (examining the general ledger entries and chart of accounts for completeness and consistency).

---

### Chapter 3: The Accounting Data Environment

This chapter provides a conceptual foundation for understanding how accounting data is stored, organized, and accessed within organizations. It introduces the relational database model, explains how tables relate to one another through keys, and connects these concepts to the chart of accounts, journal entries, and sub-ledger structures that students already know from their accounting courses. Students examine Entity-Relationship diagrams for all three databases and compare their designs. They do not write code in this chapter but instead build the mental model they will need for the SQL chapters that follow.

**Topics covered:** Relational databases and their structure. Tables, rows, columns, and data types. Primary keys and foreign keys. Entity-Relationship diagrams. How a chart of accounts maps to a database schema. The general ledger and sub-ledgers as related tables. Comparing database designs across Northwind (simple), AdventureWorks (departmental schemas), and ERPNext (ERP-integrated).

**Dataset focus:** All three. Students study the ER diagram of each database and map relationships. They compare how Northwind stores order data, how AdventureWorks organizes sales and production, and how ERPNext links its general ledger to transactional modules.

---

## PART II: ACCOUNTING ANALYTICS WITH EXCEL

### Chapter 4: Excel Essentials for Accounting Analytics

This chapter builds on whatever Excel experience students may have and establishes a consistent foundation. Rather than teaching basic spreadsheet operations, it focuses on the features that matter most for analytics work. Students learn to organize data in proper tabular form, use structured references with Excel Tables, apply sorting and filtering, and use conditional formatting to highlight patterns. All examples use the Northwind dataset, which students import from the provided Excel workbook.

**Topics covered:** Organizing data as Excel Tables. Sorting, filtering, and using slicers. Conditional formatting for pattern detection. Absolute, relative, and mixed cell references. Naming ranges for clarity. Data validation and drop-down lists. Workbook organization and documentation practices.

**Dataset focus:** Northwind (Orders, OrderDetails, Products, Customers).

**Financial Accounting exercises:** Students import the Northwind orders data into an Excel Table, filter for a specific fiscal period, and use conditional formatting to highlight orders above a revenue threshold. They prepare a schedule of sales by customer that could support a revenue disclosure note.

**Managerial Accounting exercises:** Students sort products by unit price and quantity sold, then use conditional formatting to identify the highest-revenue and lowest-revenue product categories. They prepare a product profitability ranking.

**Auditing exercises:** Students apply filters to identify orders with missing ship dates or unusually long fulfillment times. They use conditional formatting to flag transactions where the quantity ordered falls outside the normal range for a given product.

---

### Chapter 5: Data Preparation and Cleaning in Excel

This chapter addresses the practical reality that most accounting data requires preparation before analysis. Students learn to use text functions (LEFT, RIGHT, MID, TRIM, CLEAN, SUBSTITUTE) to standardize entries, date functions to extract and manipulate time periods, and lookup functions (VLOOKUP, XLOOKUP, INDEX/MATCH) to merge data from different sources. The chapter also introduces Power Query as a repeatable and documented approach to data transformation.

**Topics covered:** Text functions for cleaning account descriptions and transaction narratives. Date functions for fiscal period analysis. Lookup functions for matching data across tables. Removing duplicates and handling missing values. Introduction to Power Query for repeatable data preparation. Recording and documenting transformation steps.

**Dataset focus:** Northwind (merging Orders with Customers and Products using lookups) and AdventureWorks (cleaning Product and Vendor tables).

**Financial Accounting exercises:** Students use XLOOKUP to merge customer details into the Northwind orders table and create a receivables schedule grouped by customer and aging period. They use date functions to assign each order to its fiscal quarter.

**Managerial Accounting exercises:** Students merge AdventureWorks product cost data (standard cost, list price) with sales order details to calculate unit margins. They use Power Query to combine and clean multiple product-related tables into a single analysis-ready table.

**Auditing exercises:** Students use text functions to standardize supplier names in the Northwind suppliers table and identify potential duplicate suppliers. They use Power Query to document and automate the cleaning steps so the process is repeatable and traceable for workpaper documentation.

---

### Chapter 6: Descriptive Analytics and Summarization in Excel

This chapter teaches students to summarize and describe accounting data using the tools Excel provides. It covers statistical functions (AVERAGE, MEDIAN, STDEV, COUNT, COUNTIFS, SUMIFS), PivotTables for multidimensional summarization, and grouped calculations. Students apply these tools to answer questions across all three accounting perspectives using the Northwind and AdventureWorks datasets.

**Topics covered:** Statistical functions applied to accounting data. Building and formatting PivotTables. Grouping by date, account, and category. Calculated fields within PivotTables. Cross-tabulation for comparative analysis. Using SUMIFS, COUNTIFS, and AVERAGEIFS for conditional aggregation.

**Dataset focus:** Northwind (sales summarization) and AdventureWorks (production and purchasing summarization).

**Financial Accounting exercises:** Students build PivotTables from Northwind order data to produce revenue summaries by product category and quarter. They compare revenue across periods and calculate growth rates. They also summarize AdventureWorks sales by territory to prepare a geographic revenue disclosure.

**Managerial Accounting exercises:** Students analyze AdventureWorks production data by summarizing work order quantities, scrap rates, and production times by product. They build a PivotTable showing manufacturing costs by product subcategory and identify products with the highest scrap percentages.

**Auditing exercises:** Students use COUNTIFS and SUMIFS on Northwind order data to stratify transactions by size and identify the distribution of order values. They apply descriptive statistics to assess whether any product categories have unusual concentration of large transactions that would warrant additional testing.

---

### Chapter 7: Data Analysis and Modeling in Excel

This chapter moves beyond description into analysis and simple modeling. Students learn to use regression through the Data Analysis ToolPak, build scenario analyses using data tables and Scenario Manager, and apply basic forecasting techniques. Each technique is grounded in an accounting application using the Northwind and AdventureWorks datasets.

**Topics covered:** Correlation and regression analysis applied to accounting. Trend analysis and basic forecasting. Scenario Manager and data tables for what-if analysis. Goal Seek and Solver for optimization problems. Cost-volume-profit modeling. Sensitivity analysis and assumption documentation.

**Dataset focus:** Northwind (revenue forecasting, customer analysis) and AdventureWorks (cost-volume-profit, production modeling).

**Financial Accounting exercises:** Students build a regression model using Northwind historical sales data to forecast next-quarter revenue. They create a trend analysis chart and document the assumptions supporting the forecast, as would be required for a going-concern or revenue projection analysis.

**Managerial Accounting exercises:** Students use AdventureWorks product cost and pricing data to build a cost-volume-profit model for a bicycle product line. They use Scenario Manager to evaluate three pricing strategies and perform sensitivity analysis on material cost assumptions. They also use Solver to determine the optimal product mix given capacity constraints.

**Auditing exercises:** Students build a regression model on Northwind monthly sales data and use it to set expectations for analytical procedures. They compare the predicted values to actual values and identify months where the difference exceeds the tolerable threshold, simulating substantive analytical procedures.

---

### Chapter 8: Excel for Audit and Internal Controls

This chapter demonstrates how auditors and internal control professionals use Excel as an analytics tool. Students learn to apply techniques such as stratification of account balances, Benford's Law analysis for anomaly detection, aging analysis, and duplicate testing. The chapter uses the Northwind dataset for introductory exercises and the ERPNext dataset for more realistic audit scenarios involving journal entries and general ledger data.

**Topics covered:** Stratification and sampling using Excel. Benford's Law analysis of leading digits. Aging analysis for receivables and payables. Duplicate detection and gap analysis. Ratio analysis and trend comparison for analytical procedures. Documenting Excel-based audit analytics as workpapers.

**Dataset focus:** Northwind (order and supplier data for introductory testing) and ERPNext (journal entries, general ledger, payment entries for realistic audit analytics).

**Financial Accounting exercises:** Students perform an aging analysis on Northwind orders to estimate an allowance for doubtful accounts. Using ERPNext data, they reconcile the general ledger balances for selected accounts to the trial balance and investigate any discrepancies.

**Managerial Accounting exercises:** Students stratify ERPNext cost center expenses to identify departments with spending patterns that differ from budget expectations. They calculate variance percentages and prepare a summary report highlighting areas for management attention.

**Auditing exercises:** Students perform a Benford's Law analysis on ERPNext payment entry amounts to identify potential anomalies. They test for duplicate payments by matching on vendor, amount, and date. They also identify journal entries posted on weekends, entries with round-dollar amounts, and entries just below approval thresholds in the ERPNext data.

---

## PART III: ACCOUNTING ANALYTICS WITH SQL

### Chapter 9: Introduction to SQL for Accountants

This chapter provides a gentle and practical introduction to SQL, written specifically for students who have never programmed before. It begins by explaining why accountants need SQL (to access data directly from databases rather than relying on exported reports), then walks through the basic SELECT statement with hands-on examples using the Northwind SQLite database. Students install a lightweight SQLite tool and immediately begin writing queries.

**Topics covered:** Why SQL matters for accounting professionals. Setting up the SQLite practice environment. The SELECT statement and its components. Filtering with WHERE clauses. Sorting with ORDER BY. Using aliases for readability. Limiting results. Comparison operators, BETWEEN, IN, and LIKE. Running and saving queries.

**Dataset focus:** Northwind (SQLite).

**Financial Accounting exercises:** Students write queries to retrieve all sales orders within a specific fiscal year. They filter by customer country to prepare data for a geographic revenue analysis. They retrieve product information sorted by unit price to support inventory valuation work.

**Managerial Accounting exercises:** Students query the Northwind products table to identify products with low stock levels. They filter orders by employee (salesperson) to begin evaluating individual sales performance. They retrieve supplier data sorted by country to analyze supply chain concentration.

**Auditing exercises:** Students write queries to find orders where the shipped date is before the order date (a potential data integrity error). They filter for orders with freight charges that exceed a threshold to identify items for testing. They retrieve all products that have been discontinued to verify proper accounting treatment.

---

### Chapter 10: Querying and Joining Accounting Data

This chapter expands students' SQL skills to include joining multiple tables and performing grouped calculations. Since accounting data is inherently relational, joins are essential. Students learn INNER JOIN, LEFT JOIN, and the practical differences between them using the Northwind and AdventureWorks datasets. The chapter also introduces GROUP BY with aggregate functions, enabling students to produce summary reports directly from the database.

**Topics covered:** Joining tables with INNER JOIN and LEFT JOIN. Joining orders to customers, products to categories, invoices to line items. Aggregate functions (SUM, COUNT, AVG, MIN, MAX) with GROUP BY. Filtering grouped results with HAVING. Subqueries for multi-step questions. Writing queries that produce summary reports.

**Dataset focus:** Northwind (SQLite) and AdventureWorks (SQLite).

**Financial Accounting exercises:** Students join Northwind orders to order details and products to calculate total revenue by product category for a given year. Using AdventureWorks, they join SalesOrderHeader to SalesOrderDetail and Product to produce a revenue report by product subcategory and territory, simulating a disaggregated revenue disclosure.

**Managerial Accounting exercises:** Students join AdventureWorks work orders to products to calculate total production quantity and scrap quantity by product. They use GROUP BY and HAVING to identify products with scrap rates above a target threshold. Using Northwind, they calculate average order value by customer and rank customers by total spending.

**Auditing exercises:** Students use a LEFT JOIN on Northwind customers to orders to identify customers who appear in the customer master but have no orders (testing for completeness and validity of the customer list). Using AdventureWorks, they join purchase orders to vendors and use GROUP BY to identify vendors with unusually high transaction counts or values relative to others.

---

### Chapter 11: Intermediate SQL for Accounting Analysis

This chapter introduces more powerful SQL features that enable deeper analysis. Students learn to use CASE expressions for conditional logic, window functions for running totals and rankings, Common Table Expressions (CTEs) for organizing complex queries, and date functions for fiscal period analysis. Every concept is presented through an accounting problem using AdventureWorks and ERPNext.

**Topics covered:** CASE expressions for transaction classification and aging. Window functions (ROW_NUMBER, RANK, SUM OVER, LAG, LEAD) for running balances and period-over-period comparison. Common Table Expressions for readable multi-step analysis. Date functions for fiscal period grouping. Creating views to save useful queries.

**Dataset focus:** AdventureWorks (SQLite) and ERPNext (SQLite).

**Financial Accounting exercises:** Students write a CASE-based query on ERPNext general ledger entries to classify accounts into current assets, non-current assets, liabilities, equity, revenue, and expense groups, then aggregate to produce a trial balance. They use LAG to calculate month-over-month revenue changes from AdventureWorks sales data.

**Managerial Accounting exercises:** Students use window functions to rank AdventureWorks products by contribution margin within each product category. They build a CTE that calculates cumulative production costs by month and compares each month to the prior year. Using ERPNext cost center data, they write a query that calculates each department's share of total overhead.

**Auditing exercises:** Students use a CASE expression to age ERPNext accounts receivable into 30, 60, 90, and 120-plus day buckets. They use ROW_NUMBER to identify the largest journal entries per period for audit selection. They build a CTE that flags ERPNext journal entries meeting multiple risk criteria (posted on weekends, round amounts, near approval limits).

---

### Chapter 12: SQL for Audit Analytics and Anomaly Detection

This chapter applies SQL to audit and forensic accounting scenarios at depth. Students learn to write queries that test for specific control violations, identify duplicate payments, detect unusual journal entries, and perform completeness tests. The chapter uses all three datasets to provide a range of scenarios from simple to complex.

**Topics covered:** Testing entire populations versus sampling. Identifying duplicate payments and invoices. Detecting journal entries that bypass controls. Gap and sequence analysis for completeness testing. Benford's Law analysis in SQL. Matching transactions across systems for reconciliation. Building a library of reusable audit queries.

**Dataset focus:** Northwind (SQLite) for introductory tests, AdventureWorks (SQLite) for purchasing cycle tests, and ERPNext (SQLite) for full journal entry and GL testing.

**Financial Accounting exercises:** Students write a reconciliation query that compares ERPNext sales invoice totals to the corresponding general ledger revenue account balances. They identify invoices that exist in the sub-ledger but have no corresponding GL entry (or vice versa), simulating a subledger-to-ledger reconciliation.

**Managerial Accounting exercises:** Students query AdventureWorks purchase order data to identify purchases from vendors not on the approved vendor list. They calculate actual versus standard cost variances for production work orders and flag items where the variance exceeds a materiality threshold.

**Auditing exercises:** Students write a Benford's Law analysis on ERPNext payment entry amounts using SQL. They build a duplicate payment detection query matching on vendor, amount, and date across the ERPNext payment entries table. They perform a sequence test on Northwind order numbers to check for gaps. Using AdventureWorks, they identify purchase orders approved by the same person who created them (a segregation of duties test).

---

## PART IV: DATA VISUALIZATION AND POWER BI

### Chapter 13: Principles of Data Visualization for Accounting

This chapter establishes the conceptual foundation for effective data visualization before students learn Power BI. It covers the principles of choosing the right chart type, designing for clarity, avoiding common mistakes, and telling a story with data. Each principle is illustrated with accounting examples from all three datasets, showing how the same data can inform or mislead depending on how it is presented.

**Topics covered:** Why visualization matters in accounting communication. Choosing chart types for different analytical purposes (comparison, composition, distribution, relationship, change over time). Design principles including simplicity, appropriate scales, color use, and labeling. Common visualization errors and how to avoid them. The concept of a data story and how to structure one for financial and managerial reporting audiences.

**Dataset focus:** All three. Examples show good and poor visualizations of Northwind sales trends, AdventureWorks production metrics, and ERPNext financial statement data.

**Financial Accounting exercises:** Students evaluate a set of poorly designed charts showing ERPNext income statement trends and redesign them following the principles discussed. They plan a visual approach for presenting a multi-period balance sheet comparison.

**Managerial Accounting exercises:** Students select appropriate chart types for presenting AdventureWorks manufacturing metrics (scrap rate over time, cost per unit by product line, production volume by quarter). They sketch dashboard layouts for a plant manager audience versus an executive audience.

**Auditing exercises:** Students design a visualization plan for communicating audit findings, considering how to present the results of a Benford's Law analysis, an aging distribution, and a trend in detected anomalies to an audit committee.

---

### Chapter 14: Getting Started with Power BI

This chapter introduces Power BI Desktop as a tool for interactive data visualization and reporting. Students install Power BI, learn to import data from the Excel workbooks and SQLite databases used throughout the book, and build their first reports. The chapter walks through the interface and teaches students to create basic visualizations using the Northwind dataset.

**Topics covered:** Installing and navigating Power BI Desktop. Importing data from Excel and SQLite. The Power BI interface (report view, data view, model view). Creating basic visualizations (bar charts, line charts, tables, cards, KPIs). Formatting and arranging visuals on a report page. Connecting related tables in the model view. Publishing and sharing basics.

**Dataset focus:** Northwind (both Excel and SQLite imports).

**Financial Accounting exercises:** Students import the Northwind dataset into Power BI, connect the tables in the model view, and build a report page showing total revenue by category, revenue by quarter (line chart), and a KPI card for total sales. They create a matrix visual that resembles an income statement format with product categories as rows and quarters as columns.

**Managerial Accounting exercises:** Students build a report page showing order volume and average order value by employee (salesperson), simulating a sales performance dashboard. They add a visual that breaks down freight costs by shipper and destination country.

**Auditing exercises:** Students create a report page that visualizes the distribution of order values using a histogram and highlights transactions above a threshold using conditional formatting in a table visual. They add a slicer for date range to allow filtering to a specific audit period.

---

### Chapter 15: Data Modeling and DAX in Power BI

This chapter deepens students' Power BI skills by teaching data modeling and the DAX formula language. Students learn to build a proper star schema from accounting data, create calculated columns and measures, and use common DAX functions. The chapter uses both AdventureWorks and ERPNext to illustrate data modeling in different business contexts.

**Topics covered:** Star schema design for accounting data (fact tables and dimension tables). Creating relationships and managing cardinality. Introduction to DAX syntax. Calculated columns versus measures. Common DAX functions (SUM, CALCULATE, FILTER, ALL, RELATED). Time intelligence functions (year-to-date, prior year comparison, rolling averages). Creating a date table.

**Dataset focus:** AdventureWorks and ERPNext.

**Financial Accounting exercises:** Students build a data model from the ERPNext general ledger and chart of accounts. They create DAX measures for year-to-date revenue, prior year revenue comparison, and gross profit margin. They build a report page that produces a dynamic income statement responding to date slicers.

**Managerial Accounting exercises:** Students model AdventureWorks production data as a star schema with work orders as the fact table and products, dates, and scrap reasons as dimensions. They create DAX measures for total production cost, scrap rate, and cost per unit. They build a time intelligence measure that shows the three-month rolling average of production costs.

**Auditing exercises:** Students create DAX measures on ERPNext data that calculate the number and total value of journal entries meeting specific risk criteria (posted after hours, round amounts, above a threshold). They build a report page where an auditor can use slicers to interactively filter journal entries by risk indicator.

---

### Chapter 16: Building Accounting Dashboards in Power BI

This chapter brings together everything students have learned to build complete, interactive accounting dashboards. Students design and build three dashboards: one for financial reporting using ERPNext data, one for operational and managerial analysis using AdventureWorks data, and one for audit monitoring using a combination of all three datasets. The chapter covers interactivity features such as slicers, drill-through, bookmarks, and cross-filtering.

**Topics covered:** Dashboard planning and layout design. Slicers and cross-filtering for interactivity. Drill-through pages for detailed analysis. Bookmarks and buttons for navigation. Formatting for professional presentation. Row-level security concepts.

**Dataset focus:** All three.

**Financial Accounting exercises:** Students build a financial performance dashboard from ERPNext data that includes an income statement summary page with KPIs (revenue, net income, gross margin percentage), a balance sheet overview, and a drill-through page that shows the underlying journal entries for any selected account. Date slicers control the reporting period.

**Managerial Accounting exercises:** Students build an operational dashboard from AdventureWorks data that includes a production performance page (output, scrap rate, cost per unit by product line), a purchasing analysis page (spend by vendor, lead time trends), and a sales territory comparison page. They use bookmarks and buttons to create a navigation experience that lets managers move between views.

**Auditing exercises:** Students build an audit analytics dashboard that combines Northwind order data, AdventureWorks purchasing data, and ERPNext journal entry data into a single monitoring view. The dashboard includes a Benford's Law analysis visual, an aging analysis visual, a duplicate detection results table, and a risk-scored journal entry listing with drill-through to transaction detail.

---

## PART V: INTEGRATED AND APPLIED TOPICS

### Chapter 17: Accounting Analytics for Financial Reporting

This chapter applies the full toolkit (Excel, SQL, and Power BI) to financial reporting scenarios using the ERPNext dataset as the primary source, supplemented by AdventureWorks for multi-entity analysis. Students work through integrated cases that require extracting data using SQL, performing analysis in Excel, and presenting results in Power BI.

**Topics covered:** Integrated analytics workflows across tools. Financial ratio analysis and peer benchmarking. Revenue trend analysis and recognition pattern testing. Lease classification and amortization calculations. Intercompany transaction identification and consolidation analytics.

**Dataset focus:** ERPNext (primary) and AdventureWorks (supplementary).

**Financial Accounting exercises:** Students use SQL to extract a full trial balance from ERPNext, export it to Excel for ratio analysis and period-over-period comparison, and then build a Power BI report that presents the financial statements with interactive drill-through. They perform horizontal and vertical analysis of the income statement and balance sheet.

**Managerial Accounting exercises:** Students extract cost center level data from ERPNext using SQL and build an Excel model that allocates shared costs across departments. They create a Power BI dashboard that allows managers to see their department's financial performance with allocated and unallocated views.

**Auditing exercises:** Students use SQL to identify ERPNext journal entries recorded in the last week of the fiscal year that reverse in the first week of the next year (a test for window dressing). They prepare an Excel workpaper documenting the population, the selection criteria, and the findings. They build a Power BI page that visualizes the timing pattern of journal entries around period close.

---

### Chapter 18: Cost and Management Accounting Analytics

This chapter focuses on applying analytics to managerial and cost accounting scenarios. It uses AdventureWorks as the primary dataset because of its rich production, purchasing, and cost data, supplemented by ERPNext for budget analysis and cost center reporting.

**Topics covered:** Standard cost versus actual cost analysis. Variance analysis (material price, material usage, labor rate, labor efficiency). Product profitability analysis. Activity-based costing concepts using available data. Budget versus actual reporting. Cost center performance measurement.

**Dataset focus:** AdventureWorks (primary) and ERPNext (supplementary).

**Financial Accounting exercises:** Students use SQL to extract AdventureWorks product cost data and build an Excel model that calculates cost of goods sold for a specific period. They reconcile the calculated COGS to the revenue and margin data in the sales tables.

**Managerial Accounting exercises:** Students perform a full variance analysis on AdventureWorks work order data, comparing standard costs to actual costs and decomposing the total variance into price and efficiency components. They extract ERPNext budget data using SQL, join it to actual GL entries by cost center, and build a Power BI dashboard showing budget versus actual performance by department with drill-through to line-item detail. They also conduct a product profitability analysis across the AdventureWorks bicycle product lines.

**Auditing exercises:** Students test the reasonableness of AdventureWorks standard costs by comparing them to recent actual purchase prices and flag products where the standard cost has not been updated despite significant price changes. They evaluate ERPNext budget entries for proper authorization by checking whether budget amounts align with approved levels.

---

### Chapter 19: Forensic Accounting and Fraud Analytics

This chapter focuses on using analytics to detect fraud and support forensic investigations. It brings together techniques introduced in earlier chapters and adds new approaches such as network analysis for related-party detection and text matching for suspicious vendor identification. Students work through realistic scenarios using all three datasets.

**Topics covered:** The fraud triangle and how analytics supports detection. Digital analysis including Benford's Law extended to second and first-two digits. Network and relationship analysis for related-party detection. Vendor fraud detection patterns. Journal entry testing for management override. Expense pattern analytics. Building a continuous monitoring framework.

**Dataset focus:** All three.

**Financial Accounting exercises:** Students use ERPNext GL data to test for revenue manipulation by analyzing the timing and pattern of revenue entries relative to period close. They use SQL to identify unusual concentrations of revenue in the last days of each month and evaluate whether the pattern suggests channel stuffing or legitimate business cycles.

**Managerial Accounting exercises:** Students analyze AdventureWorks purchasing patterns to identify potential kickback arrangements. They use SQL to flag vendors where the same employee consistently approves orders, where prices exceed the average for similar products, or where purchase frequency spikes without corresponding production needs. They build an Excel model that estimates the financial impact of the identified anomalies.

**Auditing exercises:** Students investigate a simulated fraud scenario involving fictitious vendors across the three datasets. They use SQL to identify Northwind suppliers sharing addresses or phone numbers with employees. They perform a second-digit and first-two-digit Benford's Law analysis on ERPNext payment amounts. They build a Power BI dashboard that serves as a continuous monitoring tool, displaying Benford's conformity scores, duplicate detection results, and risk-scored transactions that update when new data is loaded.

---

### Chapter 20: Emerging Technologies and the Future of Accounting Analytics

This final chapter surveys the technologies that are reshaping accounting analytics, giving students a forward-looking perspective on their careers. It covers robotic process automation (RPA), artificial intelligence and machine learning, blockchain and distributed ledgers, and continuous auditing and monitoring. Rather than teaching students to build these systems, the chapter explains what each technology does, how it connects to the analytics skills learned in this book, and what accountants need to understand to work effectively alongside these technologies.

**Topics covered:** Robotic process automation in accounting workflows. Machine learning applications in accounting (classification, prediction, anomaly detection). Natural language processing for contract analysis and disclosure review. Blockchain and its implications for audit and assurance. Continuous auditing and real-time monitoring systems. The evolving role of the accounting professional. Building a personal analytics skill development plan.

**Dataset focus:** All three, used in discussion exercises and case analyses rather than technical exercises.

**Financial Accounting exercises:** Students read a case study about a company that implemented machine learning for revenue forecasting and evaluate the approach using the analytical framework from this textbook. They prepare a brief analysis explaining how the techniques in this book (regression, time intelligence, trend visualization) provide the foundation for understanding what the machine learning model does.

**Managerial Accounting exercises:** Students evaluate a case study of an organization that deployed RPA for month-end close processes. Using their knowledge of the ERPNext data model, they identify three specific tasks in the close process that could be automated and describe what the data inputs and outputs would look like.

**Auditing exercises:** Students evaluate a case study about continuous auditing implementation. They design a continuous monitoring framework for one of the three textbook datasets, specifying what tests would run, what thresholds would trigger alerts, and how the results would be presented in a Power BI dashboard. They connect their framework to the audit analytics dashboard they built in Chapter 16.

---

## APPENDICES

### Appendix A: Software Installation and Setup Guide

This appendix provides step-by-step instructions for installing and configuring Excel (with the Data Analysis ToolPak and Power Query), a SQLite browser (such as DB Browser for SQLite), and Power BI Desktop. It includes troubleshooting tips for common installation issues and instructions for accessing the companion datasets in both Excel and SQLite formats.

### Appendix B: Dataset Documentation

This appendix documents every table in all three datasets. For each database (Northwind, AdventureWorks, ERPNext), it provides the table name, a description of its purpose, all column names with data types and descriptions, primary and foreign key relationships, and the fictional business context. Entity-Relationship diagrams for all three databases are included. Students and instructors can reference this appendix when working through any chapter.

### Appendix C: Excel Function Reference

This appendix provides a concise reference of all Excel functions used in the textbook, organized by category (text, date, lookup, statistical, logical, financial), with syntax, parameters, and a brief example drawn from the textbook datasets for each.

### Appendix D: SQL Quick Reference

This appendix provides a concise reference of SQL syntax covered in the textbook, including SELECT, FROM, WHERE, JOIN, GROUP BY, HAVING, ORDER BY, CASE, window functions, CTEs, and common date functions, with short examples using the textbook datasets for each.

### Appendix E: DAX Quick Reference

This appendix provides a concise reference of all DAX functions used in the textbook, organized by category, with syntax and brief examples drawn from the textbook datasets.

### Appendix F: Mapping Exercises to Accounting Competency Frameworks

This appendix maps each exercise in the textbook to the relevant competency areas in the AICPA, IMA, and IFAC frameworks, helping instructors design their courses around specific learning outcomes and accreditation requirements.

---

## Dataset-to-Chapter Mapping Summary

**Northwind Traders** appears in Chapters 1 through 10, 12, 13, 14, 16, and 19. It serves as the primary introductory dataset for Excel and early SQL chapters due to its simplicity and accessibility.

**AdventureWorks Cycles** appears in Chapters 1, 3, 5 through 7, 10 through 13, 15 through 19. It enters fully in the mid-chapters and serves as the primary dataset for cost and managerial accounting exercises due to its manufacturing and multi-department structure.

**ERPNext Demo Company** appears in Chapters 1 through 3, 8, 11 through 13, 15 through 20. It enters for audit and GL-focused work in the Excel section and becomes the primary dataset for financial reporting, budgeting, and audit analytics in the later chapters due to its full accounting module.

---

## Suggested Course Schedules

### Undergraduate Course (4 Credits, 15 Weeks)

Week 1 covers Chapter 1 and Chapter 2, introducing analytics in accounting and understanding data through the Northwind dataset. Week 2 covers Chapter 3, the accounting data environment, where students explore ER diagrams for all three databases. Weeks 3 through 4 cover Chapters 4 and 5, Excel essentials and data preparation using Northwind. Weeks 5 through 6 cover Chapters 6 and 7, descriptive analytics and modeling using Northwind and AdventureWorks. Week 7 covers Chapter 8, Excel for audit analytics, introducing the ERPNext dataset. Weeks 8 through 9 cover Chapters 9 and 10, introduction to SQL and joining data using Northwind and AdventureWorks. Week 10 covers Chapters 11 and 12, intermediate SQL and audit analytics using AdventureWorks and ERPNext. Week 11 covers Chapter 13, visualization principles. Weeks 12 through 13 cover Chapters 14 and 15, Power BI fundamentals and data modeling. Week 14 covers Chapter 16, building accounting dashboards. Week 15 covers selected topics from Chapters 17 through 20 based on instructor preference, along with a capstone project presentation.

### Graduate Course (4 Credits, 15 Weeks)

Week 1 covers Chapters 1 through 3 together as a combined foundational session, with all three datasets introduced. Week 2 covers Chapters 4 and 5 at an accelerated pace. Week 3 covers Chapters 6 and 7 with emphasis on the modeling and analytical judgment aspects. Week 4 covers Chapter 8 with deeper discussion of audit standards and professional skepticism in analytics. Weeks 5 through 6 cover Chapters 9 through 11 with emphasis on CTEs and window functions. Week 7 covers Chapter 12 with extended case analysis requiring multi-step SQL-based investigation. Week 8 covers Chapters 13 and 14. Week 9 covers Chapter 15 with advanced DAX and complex data models. Week 10 covers Chapter 16 with emphasis on dashboard design for different stakeholder audiences. Week 11 covers Chapter 17, financial reporting analytics, as a full integrated case. Week 12 covers Chapter 18, cost and management accounting analytics. Week 13 covers Chapter 19, forensic accounting and fraud analytics. Week 14 covers Chapter 20, emerging technologies, supplemented by assigned readings from the academic literature. Week 15 involves the capstone project presentation and discussion.
