---
title: "The Role of Analytics in Accounting"
---

::: {.chapter-meta}
[Conceptual Chapter]{.chapter-pill}
[Northwind]{.dataset-badge .dataset-nw}
[AdventureWorks]{.dataset-badge .dataset-aw}
[ERPNext]{.dataset-badge .dataset-erp}
:::

---

## Learning Objectives

::: {.learning-objectives}
After completing this chapter, you will be able to:

1. Explain how data analytics has changed the work accountants perform and the skills the profession demands.
2. Define descriptive, predictive, and prescriptive analytics and identify examples of each in financial accounting, managerial accounting, and auditing.
3. Describe the purpose and capabilities of Excel, SQL, and Power BI as complementary tools for accounting analytics.
4. Compare the structure and business context of the three datasets used throughout this textbook.
5. Map the stages of an accounting analytics workflow from question formulation through communication of results.
:::

---

## Opening Scenario

You have just started a position as a staff accountant at a mid-size distribution company. During your first week, the controller asks you to investigate why gross margins declined in the most recent quarter. She hands you login credentials to the company's enterprise resource planning system and tells you the data you need is "in the database." Your accounting coursework prepared you to interpret financial statements, calculate ratios, and apply standards, but you have never pulled data directly from a database, cleaned it for analysis, or built an interactive report that the management team can explore on their own. You realize that answering the controller's question will require more than accounting knowledge. It will require the ability to extract, prepare, analyze, and communicate data. This chapter introduces the analytical mindset and the toolkit you will develop throughout this book to handle exactly this kind of challenge.

---

## The Changing Landscape of Accounting Work

The accounting profession has always been built on data. Accountants record transactions, classify them into accounts, summarize them in financial statements, and interpret the results for stakeholders. For most of the profession's history, the volume of data involved in these tasks was manageable through manual methods and later through basic spreadsheets. A general ledger might contain a few thousand entries per year, and an auditor could review a reasonable portion of those entries by hand. That era has ended.

Modern organizations generate transaction data at a scale that makes manual review impractical. A single retail company may process millions of sales transactions per month, each one recorded with a timestamp, a product identifier, a customer identifier, a store location, a payment method, and a discount code. An enterprise resource planning system at a manufacturing firm captures not only financial transactions but also production orders, material movements, quality inspections, and employee time records. The data that accountants must work with has grown by orders of magnitude, and it continues to grow (Vasarhelyi, Kogan, and Tuttle, 2015).

This growth in data has created both a challenge and an opportunity for the profession. The challenge is that traditional methods of sampling and manual review cannot keep pace with the volume and complexity of modern datasets. An auditor who selects 50 transactions from a population of 500,000 is examining one hundredth of one percent of the available evidence. The opportunity is that the same technology that generates massive datasets also provides tools to analyze entire populations rather than small samples. Accountants who can use these tools effectively bring more evidence to their conclusions, identify patterns that sampling would miss, and deliver insights that go beyond compliance and reporting (Earley, 2015).

Professional bodies have recognized this shift and responded by updating their competency frameworks. The American Institute of Certified Public Accountants has integrated data analytics into its pre-certification curriculum and its continuing education requirements. The Institute of Management Accountants has emphasized technology and analytics in its Certified Management Accountant examination content. The International Federation of Accountants has published guidance on the skills that accounting graduates need in a data-rich environment (IFAC, 2019). These developments signal that analytics is not a niche specialization within accounting. It is a core competency that every practitioner will need.

::: {.callout-tip .in-practice icon=false}
## In Practice
Accounting firms of all sizes now recruit for analytics skills alongside traditional accounting knowledge. Major firms have established dedicated data analytics practices, and even small and mid-size firms use data analysis tools for audit testing, tax planning, and advisory engagements. A 2019 survey by the Institute of Management Accountants found that data analytics ranked among the top five skills employers seek when hiring management accountants (IMA, 2019).
:::

The purpose of this textbook is to help you develop these skills in a structured and practical way. You will learn to work with data using three tools that are widely used in practice: Microsoft Excel, SQL, and Microsoft Power BI. You will apply these tools to realistic accounting data drawn from three carefully designed datasets. And you will practice solving problems from three accounting perspectives: financial accounting, managerial accounting, and auditing. By the end of this book, you will be able to extract data from a database, prepare it for analysis, summarize and model it, visualize the results, and communicate your findings to professional audiences.


## Defining Accounting Analytics

Analytics is the process of examining data to draw conclusions, identify patterns, and support decisions. In accounting, analytics applies this process to financial and operational data for purposes such as reporting, planning, control, and assurance. The term "accounting analytics" as used in this textbook refers to the application of data extraction, preparation, analysis, and visualization techniques to accounting data for the purpose of producing information that supports financial reporting, managerial decision-making, and audit assurance.

It is important to distinguish accounting analytics from related terms that students may encounter. "Data analytics" is a broad term that encompasses analytical work in any domain, from marketing to healthcare to logistics. "Business intelligence" typically refers to the tools and infrastructure that organizations use to collect, store, and present data for operational and strategic decisions. "Big data" refers to datasets that are too large or complex for traditional data processing methods and is often associated with technologies such as Hadoop and cloud computing. Accounting analytics draws on all of these concepts but applies them specifically to the data, questions, and standards that define the accounting profession (Richins, Stapleton, Stratopoulos, and Wong, 2017).

### The Three Types of Analytics

A useful framework for understanding the scope of analytics divides it into three categories: descriptive, predictive, and prescriptive. These categories represent increasing levels of analytical complexity and are not mutually exclusive. Most real-world accounting analytics projects involve more than one type.

![The Analytics Continuum.](visuals/ch01/fig-01-01-analytics-continuum.svg){#fig-01-01 fig-alt="A horizontal diagram showing three stages from left to right: Descriptive Analytics, Predictive Analytics, and Prescriptive Analytics. The stages answer the questions What happened, What might happen, and What should we do. Each stage includes a brief accounting example beneath it."}

**Descriptive analytics** answers the question "what happened?" It involves summarizing historical data to understand past performance, identify trends, and describe the current state of affairs. Descriptive analytics is the foundation of most accounting work. When a financial analyst prepares a comparative income statement showing revenue by product line for the past four quarters, that is descriptive analytics. When an auditor stratifies accounts receivable by aging bucket to assess the adequacy of the allowance for doubtful accounts, that is also descriptive analytics. The tools of descriptive analytics include aggregation, grouping, sorting, filtering, and basic statistical measures such as totals, averages, and counts.

In the context of this textbook, descriptive analytics appears most prominently in the Excel chapters (Part II) and the introductory SQL chapters (Part III). Students will build PivotTables that summarize sales by category and quarter, write SQL queries that calculate average order values by customer, and create Power BI dashboards that display key performance indicators. These are all descriptive tasks, and they form the base on which more advanced analysis is built.

**Predictive analytics** answers the question "what might happen?" It involves using historical data to make forecasts, estimate probabilities, and identify the factors that drive outcomes. Predictive analytics moves beyond describing the past to projecting the future. When a management accountant builds a regression model to forecast next quarter's revenue based on historical trends, that is predictive analytics. When an auditor uses statistical analysis to set an expectation for an account balance and then compares the actual balance to the expectation as a substantive analytical procedure, that too involves prediction. The tools of predictive analytics include regression analysis, trend extrapolation, time series modeling, and classification techniques.

In this textbook, predictive analytics appears in the modeling chapter of the Excel section (Chapter 7), in the intermediate SQL chapters where students use window functions for period-over-period analysis (Chapter 11), and in the Power BI chapters where DAX time intelligence functions enable rolling averages and year-over-year comparisons (Chapter 15). Students will build forecasting models, conduct sensitivity analyses, and set analytical expectations that mirror the procedures used in professional practice.

**Prescriptive analytics** answers the question "what should we do?" It involves using data analysis to recommend a course of action, often by optimizing an objective subject to constraints. Prescriptive analytics is the most advanced of the three types and is less common in current accounting practice than descriptive and predictive analytics, although it is growing. When a cost accountant uses Excel's Solver tool to determine the optimal product mix that maximizes contribution margin given production capacity constraints, that is prescriptive analytics. When a tax advisor uses scenario modeling to recommend a filing strategy that minimizes a client's tax liability across multiple jurisdictions, that also has prescriptive elements.

This textbook introduces prescriptive analytics through optimization exercises in Chapter 7 (using Solver and Scenario Manager in Excel) and through scenario analysis in the integrated chapters of Part V. The emphasis throughout the book, however, is on descriptive and predictive analytics because these represent the analytical work that accounting professionals perform most frequently.

::: {.callout-warning .watch-out icon=false}
## Watch Out
Students sometimes assume that descriptive analytics is "basic" and that the goal is to reach prescriptive analytics as quickly as possible. In practice, most accounting analytics work is descriptive, and doing it well requires substantial skill. A poorly constructed summary can mislead decision makers just as easily as a sophisticated model can. The value of analytics lies not in its complexity but in the quality of the questions it answers and the rigor of the process behind it.
:::


## Why Accountants Need Analytics Skills

The demand for analytics skills in accounting is driven by several developments that have reshaped the profession over the past two decades. Understanding these drivers helps explain why this textbook exists and why the skills it teaches matter for your career.

The first driver is the increasing availability of data. As organizations have adopted enterprise resource planning systems, cloud-based accounting platforms, and automated transaction processing, the volume of financial and operational data available for analysis has expanded dramatically. Accountants who can access and analyze this data directly, rather than waiting for IT departments to produce reports, work more efficiently and can respond to questions in real time (Appelbaum, Kogan, and Vasarhelyi, 2017).

The second driver is the evolution of audit methodology. Auditing standards increasingly encourage or require the use of data analytics. The ability to test an entire population of transactions rather than a sample changes the nature of audit evidence. Auditors who use analytics can identify anomalies that sampling would miss, perform more precise risk assessments, and provide more relevant findings to audit committees. The Public Company Accounting Oversight Board has emphasized the use of technology and data analysis in its inspection findings, and firms have responded by investing in analytics training for their audit staff (PCAOB, 2017).

The third driver is the expansion of the accountant's role from preparer and verifier to advisor and analyst. Organizations expect their accounting and finance teams to provide forward-looking analysis, scenario planning, and strategic insight, not just historical reports. Management accountants, in particular, are asked to explain why results differ from plan, to forecast future performance under different assumptions, and to identify the operational drivers behind financial outcomes. These tasks require analytical skills that go beyond debits and credits (Cokins, 2013).

The fourth driver is competitive pressure in the labor market. Graduates who can combine accounting knowledge with data analysis skills are more attractive to employers than those with accounting knowledge alone. This is true across all areas of the profession, from public accounting to industry to government. The ability to write a SQL query, build a PivotTable, or create an interactive dashboard distinguishes a candidate in a hiring process and opens career paths that were previously reserved for specialists in information systems or data science.

::: {.callout-tip .in-practice icon=false}
## In Practice
A survey of accounting professionals conducted by Kokina and Dagiliene (2017) found that respondents identified data analysis and technology skills as the area of greatest change in the competencies required of accountants. Respondents across audit, tax, and advisory roles reported that they spend more time working with data tools than they did five years earlier and expected that trend to continue.
:::

| Role | Descriptive Example | Predictive Example |
|---|---|---|
| Financial Reporting | Comparative income statement showing revenue by product line for the past four quarters | Revenue forecast for the next fiscal quarter using trend extrapolation of historical sales data |
| Managerial Accounting | Product profitability ranking by category based on unit margins and sales volume | Cost-volume-profit model projecting break-even points under three pricing scenarios |
| External Audit | Stratification of accounts receivable by aging bucket to evaluate the allowance for doubtful accounts | Regression-based expectation for monthly revenue used as a substantive analytical procedure |
| Internal Audit | Frequency distribution of payment amounts to identify concentrations near approval thresholds | Risk scoring of journal entries based on multiple indicators to prioritize selections for testing |

: Examples of Analytics Applications by Accounting Role {#tbl-01-01}


## The Accounting Analytics Workflow

Before learning specific tools, it is helpful to understand the general process that all accounting analytics projects follow. Whether you are building a revenue summary in Excel, writing an audit query in SQL, or designing a dashboard in Power BI, the work progresses through the same sequence of stages. This textbook is organized around these stages, and understanding them now will help you see how the chapters connect.

![The Accounting Analytics Workflow.](visuals/ch01/fig-01-02-analytics-workflow.svg){#fig-01-02 fig-alt="A process flowchart showing six stages in sequence: (1) Define the Question, (2) Identify and Access the Data, (3) Prepare and Clean the Data, (4) Analyze the Data, (5) Visualize and Present the Results, (6) Communicate Findings and Recommendations. Each stage includes a one-sentence description."}

The first stage is defining the question. Every analytics project begins with a clear statement of the problem or question to be addressed. In the opening scenario of this chapter, the controller's question was specific: why did gross margins decline in the most recent quarter? A well-defined question guides every subsequent decision, from which data to collect to which visualizations to create. Vague questions produce vague answers. The ability to translate a business concern into an analytical question is one of the most important skills an accountant can develop.

The second stage is identifying and accessing the data. Once the question is defined, the accountant must determine which data is needed and where it resides. In many organizations, the relevant data is stored in databases that are part of the company's ERP system or accounting software. Accessing this data may require writing SQL queries to extract the relevant tables and columns. In other cases, the data may be available in spreadsheet exports or flat files. Chapter 2 and Chapter 3 of this textbook address this stage by teaching students how accounting data is structured and stored.

The third stage is preparing and cleaning the data. Raw data almost always contains problems that must be resolved before analysis can begin. Missing values, duplicate records, inconsistent formatting, and incorrect data types are common in accounting datasets. Data preparation is often the most time-consuming stage of an analytics project, and it is also the most important. Analysis performed on dirty data produces unreliable results. Chapters 4 and 5 cover data preparation in Excel, and Chapters 9 and 10 cover data extraction and joining in SQL.

The fourth stage is analyzing the data. This is where the accountant applies techniques such as summarization, comparison, trend analysis, regression, and anomaly detection to answer the question defined in the first stage. The choice of technique depends on the question and the type of data available. Chapters 6 through 8 cover analysis in Excel, Chapters 10 through 12 cover analysis in SQL, and Chapters 15 and 16 cover analysis in Power BI.

The fifth stage is visualizing and presenting the results. Data visualization transforms analytical results into visual formats that audiences can interpret quickly and accurately. A well-designed chart, table, or dashboard communicates the answer to the original question more effectively than a spreadsheet full of numbers. Chapter 13 covers visualization principles, and Chapters 14 through 16 teach students to build interactive reports and dashboards in Power BI.

The sixth stage is communicating findings and recommendations. The final product of an analytics project is not a spreadsheet or a dashboard but a communication to decision makers. That communication might take the form of a written memorandum to an audit committee, a presentation to management, or an interactive report that stakeholders can explore. The ability to translate analytical results into clear, professional language is essential. This skill is practiced throughout the textbook in the applied exercises and comprehensive cases, each of which asks students to produce a written interpretation alongside their technical work.

::: {.callout-note .connecting-dots icon=false}
## Connecting the Dots
The six-stage workflow described here is not unique to accounting. It closely parallels the data analysis process described in data science and business intelligence literature (Provost and Fawcett, 2013). What makes accounting analytics distinctive is not the process itself but the data it works with (financial and operational transactions), the questions it addresses (reporting, control, assurance), and the professional standards that govern the work (GAAP, GAAS, IMA ethical standards). Throughout this book, the workflow provides the thread that connects every chapter and every tool.
:::


## The Tools of This Textbook

This textbook uses three tools: Microsoft Excel, SQL (Structured Query Language), and Microsoft Power BI. These tools were selected because they are widely used in accounting practice, they are accessible to students without programming backgrounds, and together they cover the full analytics workflow from data preparation through visualization.

### Microsoft Excel

Excel is the most widely used analytical tool in the accounting profession. Nearly every accountant works with Excel on a daily basis, and most accounting graduates enter the workforce with at least basic spreadsheet skills. This textbook builds on that foundation and extends it into areas that many students have not explored, including structured Excel Tables, PivotTables, statistical functions, Power Query for data preparation, the Data Analysis ToolPak for regression, and Solver for optimization.

Excel is most powerful when working with datasets that fit comfortably in a spreadsheet, typically up to a few hundred thousand rows. It excels at ad hoc analysis, where the accountant needs to explore data interactively, try different approaches, and produce results quickly. Excel is also the primary tool for building financial models, conducting what-if analysis, and preparing workpapers that document analytical procedures.

Part II of this textbook (Chapters 4 through 8) is devoted to Excel. Students will learn to import, clean, summarize, model, and test accounting data using features that go well beyond basic formulas and formatting.

### SQL (Structured Query Language)

SQL is the standard language for accessing data stored in relational databases. It allows accountants to extract exactly the data they need from large, complex databases without relying on pre-built reports or IT intermediaries. SQL is particularly important for accountants who work with ERP systems, because the underlying data in these systems is stored in relational databases that SQL can query directly.

SQL is most powerful when working with large datasets, when the data spans multiple related tables that must be joined together, and when the same analysis needs to be performed repeatedly. An auditor who writes a SQL query to identify duplicate payments can run that same query every quarter with no additional effort. A financial analyst who writes a query to produce a revenue summary by territory and product line can reuse that query whenever the data is updated.

Part III of this textbook (Chapters 9 through 12) is devoted to SQL. Students will learn to write queries that retrieve, filter, join, aggregate, and analyze accounting data stored in SQLite databases.

### Microsoft Power BI

Power BI is a business intelligence platform that enables accountants to build interactive dashboards and reports. It connects to a wide range of data sources (including Excel files and SQL databases), provides a data modeling layer for defining relationships and calculations, and offers a rich set of visualization tools for presenting results.

Power BI is most powerful when the goal is to create a reusable, interactive report that multiple stakeholders can explore. A management accountant who builds a budget-versus-actual dashboard in Power BI gives every department manager the ability to filter the report to their own cost center, drill down into specific line items, and compare results across periods. An audit team that builds an anomaly detection dashboard creates a monitoring tool that can be refreshed with new data each audit cycle.

Part IV of this textbook (Chapters 13 through 16) is devoted to Power BI. Students will learn visualization principles, the Power BI interface, data modeling with DAX, and interactive dashboard design.

![The Three Tools and Their Roles in the Analytics Workflow.](visuals/ch01/fig-01-03-tools-workflow-mapping.svg){#fig-01-03 fig-alt="A diagram showing Excel, SQL, and Power BI mapped to the six stages of the analytics workflow, indicating where each tool is primarily used. SQL maps primarily to stages 2 and 3 (accessing and preparing data). Excel maps primarily to stages 3 and 4 (preparing and analyzing data). Power BI maps primarily to stages 4 and 5 (analyzing and visualizing data). All three tools contribute to stage 6 (communication)."}

::: {.callout-note .connecting-dots icon=false}
## Connecting the Dots
Part V of this textbook (Chapters 17 through 20) integrates all three tools. In those chapters, you will work through scenarios that begin with SQL to extract data from a database, move to Excel for detailed analysis and modeling, and finish in Power BI for visualization and presentation. This integrated approach mirrors how analytics projects work in practice, where no single tool handles every stage of the workflow.
:::


## Introduction to the Three Datasets

This textbook is built around three datasets that you will use throughout the entire book. All three datasets are provided in two formats: Microsoft Excel workbooks and SQLite database files. This means you will work with the same underlying data regardless of whether you are using Excel, SQL, or Power BI in a given chapter. The datasets represent three different types of businesses at three different levels of complexity, and the textbook introduces them in order from simplest to most complex.

### Northwind Traders

Northwind Traders is a fictional small wholesale food distribution company. It buys specialty food products from suppliers around the world and sells them to retail and restaurant customers. The Northwind database is compact and straightforward. It contains eight core tables: Customers, Orders, OrderDetails, Products, Categories, Suppliers, Employees, and Shippers.

The Northwind dataset is the first one you will work with in this book. Its simplicity makes it ideal for learning new tools and techniques without being distracted by data complexity. When you write your first SQL query in Chapter 9 or build your first PivotTable in Chapter 6, you will use Northwind data. The database contains approximately 830 orders, 2,100 order line items, 77 products, and 91 customers. These numbers are small enough that you can inspect the data manually to verify your analytical results, which is a valuable habit to develop.

From a financial accounting perspective, Northwind provides sales revenue data, customer receivables information, and product inventory records that support exercises in revenue analysis, receivables aging, and inventory valuation. From a managerial accounting perspective, Northwind provides data on product pricing, shipping costs, and sales performance by employee and region. From an auditing perspective, Northwind provides transaction-level data that supports exercises in duplicate detection, completeness testing, and anomaly identification.

### Adventure Works Cycles

Adventure Works Cycles is a fictional mid-size multinational bicycle manufacturer. It designs, produces, and sells bicycles, bicycle components, clothing, and accessories through multiple sales territories. The AdventureWorks database is substantially larger and more complex than Northwind. It contains approximately 70 tables organized across five functional areas: Sales, Production, Purchasing, Human Resources, and Person management.

The AdventureWorks dataset enters the textbook in the middle chapters as exercises grow more complex and students have built enough skill to handle a richer data environment. Its manufacturing data is particularly valuable for managerial accounting exercises. The database contains work orders with routing and scrap tracking, bills of materials, standard and actual cost records, vendor purchase orders, and multi-territory sales transactions. These data elements support exercises in variance analysis, product costing, production performance measurement, and purchasing evaluation that are not possible with the simpler Northwind dataset.

From a financial accounting perspective, AdventureWorks provides multi-territory revenue data and product cost data that support exercises in disaggregated revenue disclosure and cost of goods sold analysis. From an auditing perspective, AdventureWorks provides purchasing cycle data that supports exercises in vendor analysis, segregation of duties testing, and purchase price variance evaluation.

### ERPNext Demo Company

ERPNext is a fictional company operating within a full enterprise resource planning environment. Unlike Northwind and AdventureWorks, which focus on specific operational areas, the ERPNext database includes a complete accounting module with a chart of accounts, general ledger entries, journal entries, sales and purchase invoices, cost centers, budgets, payment entries, bank reconciliation records, and asset registers. This makes ERPNext the most accounting-rich dataset of the three.

The ERPNext dataset appears in the textbook once students have developed enough analytical skill to work with a full accounting system. It is the primary dataset for financial statement preparation, general ledger analysis, budgetary control, audit testing, and integrated financial reporting. Because ERPNext mirrors the structure of a production ERP system, working with it gives students familiarity with the kind of data environment they will encounter in professional practice.

From a financial accounting perspective, ERPNext provides everything needed to prepare financial statements from the general ledger, perform ratio analysis, and conduct period-over-period comparisons. From a managerial accounting perspective, ERPNext provides cost center data and budget records that support exercises in budget-versus-actual analysis and departmental performance measurement. From an auditing perspective, ERPNext provides journal entry data that supports exercises in management override testing, Benford's Law analysis, duplicate payment detection, and continuous monitoring.

| Attribute | Northwind Traders | Adventure Works Cycles | ERPNext Demo Company |
|---|---|---|---|
| Company Type | Small wholesale food distributor | Mid-size multinational bicycle manufacturer | Full enterprise resource planning environment |
| Number of Core Tables | 8 tables | Approximately 70 tables across 5 schemas | 20+ accounting and operational tables |
| Key Functional Areas | Sales, customers, products, suppliers | Sales, production, purchasing, human resources, person management | General ledger, journal entries, invoices, payments, budgets, cost centers |
| Accounting Module Depth | Transaction-level sales data only (no general ledger or chart of accounts) | Product cost and manufacturing data (no complete accounting module) | Full chart of accounts, general ledger, journal entries, and financial reporting capability |
| Primary Use in This Book | Introductory chapters for learning new tools and techniques | Mid-level chapters for cost accounting, production analysis, and purchasing evaluation | Financial reporting, audit analytics, budgetary control, and integrated analysis |
| Chapters Where Featured | 1 through 10, 12 through 14, 16, and 19 | 1, 3, 5 through 7, 10 through 13, 15 through 19 | 1 through 3, 8, 11 through 13, 15 through 20 |

: Comparison of the Three Textbook Datasets {#tbl-01-02}


![implified Entity-Relationship Diagram for Northwind Traders.](visuals/ch01/fig-01-04-northwind-er.svg){#fig-01-04 fig-alt="Shows the eight core tables (Customers, Orders, OrderDetails, Products, Categories, Suppliers, Employees, Shippers) and their relationships using crow's foot notation. This is a simplified preview; the full diagram appears in Chapter 3 and Appendix B."}


![Simplified Entity-Relationship Diagram for Adventure Works Cycles.](visuals/ch01/fig-01-05-adventureworks-er.svg){#fig-01-05 fig-alt="Shows a selected subset of tables from the Sales, Production, and Purchasing schemas to illustrate the database's scope without overwhelming the reader. The full diagram appears in Chapter 3 and Appendix B."}


![Simplified Entity-Relationship Diagram for ERPNext Demo Company.](visuals/ch01/fig-01-06-erpnext-er.svg){#fig-01-06 fig-alt="Shows the chart of accounts, general ledger entries, journal entries, sales invoices, and payment entries tables and their relationships. The full diagram appears in Chapter 3 and Appendix B."}


::: {.callout-warning .watch-out icon=false}
## Watch Out
These three datasets are fictional companies created for educational purposes. They are designed to illustrate realistic data structures and analytical challenges, but they do not represent the full complexity or messiness of real-world data. Real ERP systems may contain hundreds of tables, custom fields, and data quality problems that exceed what you will encounter in these datasets. The skills you learn here will transfer to real-world environments, but you should expect that professional practice will require additional adaptation and judgment.
:::


## Guided Tutorial 1.1: Exploring the Three Datasets

**Context and objective.** In this tutorial, you will open each of the three datasets in Excel and examine their structure. The goal is not to perform any analysis but to build familiarity with the tables, columns, and business context of each dataset. By the end of this tutorial, you will know what data is available in each database and where to find it.

**Prerequisites.** You need Microsoft Excel installed on your computer and access to the three Excel workbook files provided with this textbook: Northwind.xlsx, AdventureWorks.xlsx, and ERPNext.xlsx.

**Step-by-step instructions.**

**Step 1.** Open the file Northwind.xlsx in Excel. Notice that the workbook contains multiple worksheets, each representing one table in the Northwind database. Click through each worksheet tab at the bottom of the screen and note the table name. You should see worksheets labeled Customers, Employees, Categories, Suppliers, Shippers, Products, Orders, and OrderDetails.

**Step 2.** Click on the Orders worksheet. Examine the column headers in row 1. You should see columns including OrderID, CustomerID, EmployeeID, OrderDate, RequiredDate, ShippedDate, ShipVia, and Freight, among others. Scroll down to get a sense of the number of records. The Orders table contains approximately 830 rows of data.

**Step 3.** Click on the OrderDetails worksheet. Examine the columns, which include OrderID, ProductID, UnitPrice, Quantity, and Discount. Notice that OrderID appears in both the Orders and OrderDetails worksheets. This column links the two tables together, a concept you will study in depth in Chapter 3 and use extensively when writing SQL joins in Chapters 10 and 11.

::: {#fig-01-07 .figure-placeholder}
**Figure 1.7.** Screenshot of the Northwind Orders worksheet in Excel, showing column headers and the first several rows of data. Annotated callouts identify the OrderID, CustomerID, OrderDate, and Freight columns.
:::

**Step 4.** Close Northwind.xlsx and open AdventureWorks.xlsx. This workbook contains significantly more worksheets than Northwind. Click through several worksheet tabs and note the variety of data available. Look for worksheets related to sales (such as SalesOrderHeader and SalesOrderDetail), production (such as WorkOrder and Product), purchasing (such as PurchaseOrderHeader and Vendor), and human resources (such as Employee and Department).

**Step 5.** Click on the Product worksheet in AdventureWorks.xlsx. Examine the columns, which include ProductID, Name, ProductNumber, StandardCost, ListPrice, ProductSubcategoryID, and several others. Notice that the Product table includes both cost and pricing information, which will be essential for profitability analysis in later chapters.

**Step 6.** Close AdventureWorks.xlsx and open ERPNext.xlsx. Look for worksheets that represent core accounting tables. You should find worksheets such as Account (the chart of accounts), GLEntry (general ledger entries), JournalEntry, SalesInvoice, PurchaseInvoice, PaymentEntry, and CostCenter. Click on the Account worksheet and examine the account names, account types, and parent account relationships. This is the chart of accounts for the ERPNext company, and it forms the backbone of the accounting module.

**Step 7.** Click on the GLEntry worksheet. Examine the columns, which should include fields such as PostingDate, Account, Debit, Credit, Voucher Type, and Voucher Number. This table contains the individual debit and credit entries that make up the general ledger. Every financial transaction in the ERPNext system is recorded here, and you will use this table extensively in the audit and financial reporting chapters.

**Checkpoint.** At this point, you should have opened all three workbooks and examined at least two worksheets in each one. You should be able to answer the following questions: Which dataset has the fewest tables? (Northwind.) Which dataset has tables related to manufacturing and production? (AdventureWorks.) Which dataset contains a chart of accounts and general ledger entries? (ERPNext.) If you can answer these three questions, you are ready to proceed.


## How This Book Is Organized

This textbook is organized into five parts that follow the progression of the analytics workflow and introduce tools in a sequence designed for students with no prior analytics or programming experience.

**Part I, Foundations of Accounting Analytics** (Chapters 1 through 3), establishes the conceptual groundwork. You are in Part I now. Chapter 2 will teach you to think critically about accounting data, including its types, sources, and quality dimensions. Chapter 3 will introduce the relational database model and show you how accounting data is organized within the three textbook databases.

**Part II, Accounting Analytics with Excel** (Chapters 4 through 8), teaches you to use Excel as an analytical tool. These chapters move from data organization and cleaning through summarization, modeling, and audit-specific analytics. By the end of Part II, you will be able to build PivotTables, run regressions, perform Benford's Law analysis, and prepare professional analytical workpapers.

**Part III, Accounting Analytics with SQL** (Chapters 9 through 12), teaches you to query relational databases using SQL. These chapters start with the basic SELECT statement and progress through joins, aggregation, window functions, and audit analytics queries. By the end of Part III, you will be able to write SQL queries that extract, join, summarize, and test accounting data directly from a database.

**Part IV, Data Visualization and Power BI** (Chapters 13 through 16), teaches you to build interactive reports and dashboards. These chapters begin with visualization principles and progress through Power BI basics, data modeling with DAX, and full dashboard design. By the end of Part IV, you will be able to build professional dashboards for financial reporting, operational management, and audit monitoring.

**Part V, Integrated and Applied Topics** (Chapters 17 through 20), brings everything together. These chapters apply the full toolkit to financial reporting analytics, cost and management accounting analytics, forensic accounting and fraud detection, and emerging technologies. The chapters in Part V require you to move between Excel, SQL, and Power BI within a single project, just as you would in professional practice.


![Book Organization Map.](visuals/ch01/fig-01-08-book-organization-map.svg){#fig-01-08 fig-alt="A visual roadmap showing the five parts of the book as a progression from left to right. Part I (Foundations) leads to Part II (Excel), Part III (SQL), and Part IV (Power BI), which converge into Part V (Integrated Topics). Each part shows its chapter numbers and the tools and datasets used."}


Each chapter follows a consistent structure. It opens with learning objectives and a motivating scenario, presents concepts through narrative explanation and guided tutorials, and closes with a summary, key terms, review questions, and applied exercises organized by three accounting perspectives: Financial Accounting, Managerial Accounting, and Auditing. Five comprehensive cases, one at the end of each part, provide extended multi-tool investigations that integrate the material from all chapters in that part.

::: {.callout-tip .in-practice icon=false}
## In Practice
The three-perspective exercise structure in this book reflects how analytics is used across the accounting profession. The same technique, such as aging analysis, serves different purposes depending on the role. A financial accountant uses aging analysis to estimate the allowance for doubtful accounts. A managerial accountant uses it to assess collection efficiency and cash flow timing. An auditor uses it to evaluate management's estimates and to identify balances for confirmation testing. Seeing these connections will help you understand why a single analytical skill has broad professional value.
:::


## Looking Ahead

This chapter has introduced the concept of accounting analytics, defined the three types of analytics, described the tools and datasets you will use throughout the book, and outlined the analytical workflow that connects every chapter. In the next chapter, you will take a closer look at accounting data itself. You will learn to distinguish different data types, identify common data quality problems, and understand why the quality of your data determines the quality of your analysis. The practical skills begin in Chapter 2, and they build steadily from that point forward.

---

## Chapter Summary

The accounting profession is undergoing a fundamental shift in the skills it demands from practitioners. The growth of transaction data, the evolution of audit methodology, and the expansion of the accountant's role from preparer to analyst have created strong demand for data analytics competencies. Professional bodies including the AICPA, IMA, and IFAC have responded by integrating analytics into their competency frameworks, signaling that these skills are essential rather than optional.

Analytics in accounting takes three forms. Descriptive analytics summarizes historical data to explain what happened. Predictive analytics uses historical patterns to forecast future outcomes. Prescriptive analytics recommends actions by optimizing objectives subject to constraints. Most accounting analytics work is descriptive or predictive, and doing this work well requires both technical skill and professional judgment.

This textbook teaches accounting analytics using three tools (Excel, SQL, and Power BI) applied to three datasets (Northwind Traders, Adventure Works Cycles, and ERPNext Demo Company). The tools cover the full analytics workflow from data access through visualization and communication. The datasets represent three levels of complexity and three types of business environments, giving students a range of experience that prepares them for the variety they will encounter in practice.

Every analytical project follows a consistent workflow: define the question, access the data, prepare and clean the data, analyze it, visualize the results, and communicate findings. This workflow provides the organizing thread for the entire book. The chapters are arranged so that students develop foundational skills in Parts I through IV and then apply them in integrated, multi-tool projects in Part V.

---

## Key Terms

**Accounting analytics.** The application of data extraction, preparation, analysis, and visualization techniques to financial and operational data for the purpose of supporting financial reporting, managerial decision-making, and audit assurance.

**Analytics workflow.** The sequence of stages that an accounting analytics project follows, from defining the question through communicating findings. The six stages are question definition, data identification, data preparation, analysis, visualization, and communication.

**Chart of accounts.** A structured list of all accounts used by an organization to record financial transactions, organized by account type (assets, liabilities, equity, revenue, expenses). In the ERPNext dataset, the chart of accounts is stored in the Account table.

**Data analytics.** A broad term for the process of examining data to draw conclusions, identify patterns, and support decisions. Accounting analytics is a specific application of data analytics to accounting data and questions.

**Descriptive analytics.** The type of analytics that summarizes and describes historical data to answer the question "what happened?" Examples in accounting include financial statement preparation, variance reports, and aging analyses.

**Enterprise resource planning (ERP) system.** An integrated software platform that organizations use to manage business processes across departments, including accounting, sales, purchasing, production, and human resources. ERPNext is the ERP-based dataset used in this textbook.

**Entity-Relationship (ER) diagram.** A visual representation of the tables in a database and the relationships between them. ER diagrams show how tables are connected through primary and foreign keys.

**Foreign key.** A column in a database table that references the primary key of another table, establishing a relationship between the two tables. For example, the CustomerID column in the Northwind Orders table is a foreign key that references the CustomerID column in the Customers table.

**General ledger.** The complete record of all financial transactions for an organization, organized by account. In the ERPNext dataset, the general ledger is represented by the GLEntry table.

**Power BI.** A business intelligence platform developed by Microsoft that enables users to connect to data sources, build data models, and create interactive visualizations and dashboards.

**Predictive analytics.** The type of analytics that uses historical data to forecast future outcomes and estimate probabilities. Examples in accounting include revenue forecasting, regression-based analytical procedures, and credit risk assessment.

**Prescriptive analytics.** The type of analytics that recommends actions by optimizing an objective subject to constraints. Examples in accounting include product mix optimization, tax strategy planning, and resource allocation modeling.

**Primary key.** A column (or combination of columns) in a database table that uniquely identifies each row. For example, OrderID is the primary key of the Northwind Orders table.

**Relational database.** A system for storing data in tables that are connected to one another through defined relationships. The three datasets in this textbook are provided as relational databases in SQLite format.

**SQL (Structured Query Language).** The standard language for accessing, querying, and manipulating data stored in relational databases. Part III of this textbook teaches SQL using SQLite databases.

**SQLite.** A lightweight relational database system that stores the entire database in a single file. This textbook uses SQLite because it requires no server installation and runs on any operating system.

---

## Multiple Choice Questions

**1.** Which of the following best describes the primary reason that analytics skills have become essential for accounting professionals?

A. Accounting standards now require the use of data visualization tools in all financial reports.
B. The volume and complexity of financial and operational data have grown beyond what traditional manual methods can effectively analyze.
C. Analytics skills have replaced the need for accountants to understand generally accepted accounting principles.
D. Employers prefer to hire data scientists rather than accountants for financial reporting roles.

**2.** A management accountant prepares a report showing total manufacturing costs by product line for the past four quarters and calculates the percentage change from quarter to quarter. This activity is best classified as which type of analytics?

A. Prescriptive analytics
B. Predictive analytics
C. Descriptive analytics
D. Diagnostic analytics

**3.** An auditor builds a regression model using monthly revenue data from the prior year to establish an expected range for current-year monthly revenue. The auditor then compares actual monthly revenue to the expected range and investigates months where the difference exceeds the threshold. This procedure involves which type of analytics?

A. Descriptive analytics only
B. Predictive analytics
C. Prescriptive analytics
D. None of the above, because regression is a statistical technique rather than an analytics type

**4.** A cost accountant uses Excel's Solver tool to determine the combination of products that maximizes total contribution margin given constraints on machine hours and raw material availability. This activity is best classified as which type of analytics?

A. Descriptive analytics
B. Predictive analytics
C. Prescriptive analytics
D. Exploratory analytics

**5.** Which of the following is the correct sequence of stages in the accounting analytics workflow as described in this chapter?

A. Access data, define the question, analyze, clean, visualize, communicate
B. Define the question, access data, clean and prepare data, analyze, visualize, communicate
C. Analyze data, define the question, visualize, clean, communicate, access data
D. Define the question, visualize, access data, analyze, clean, communicate

**6.** Which of the three textbook datasets contains a chart of accounts and general ledger entries?

A. Northwind Traders
B. Adventure Works Cycles
C. ERPNext Demo Company
D. All three datasets contain a chart of accounts

**7.** Which tool covered in this textbook is most appropriate for extracting data directly from a relational database?

A. Microsoft Excel
B. SQL
C. Microsoft Power BI
D. The Data Analysis ToolPak

**8.** The Northwind dataset is introduced first in this textbook primarily because it:

A. Contains the most realistic accounting data of the three datasets
B. Is the only dataset that includes both Excel and SQLite formats
C. Is compact and simple enough for students to learn new tools without being overwhelmed by data complexity
D. Includes manufacturing and production data needed for early exercises

**9.** Which professional organization's competency framework has been updated to include data analytics as a core skill for management accountants?

A. The Financial Accounting Standards Board (FASB)
B. The Institute of Management Accountants (IMA)
C. The Securities and Exchange Commission (SEC)
D. The International Accounting Standards Board (IASB)

**10.** An accountant needs to create an interactive dashboard that allows multiple department managers to filter financial results to their own cost center and drill down into individual line items. Which tool is best suited for this purpose?

A. A SQL query
B. A static Excel spreadsheet
C. Microsoft Power BI
D. The Excel Data Analysis ToolPak

**11.** In the context of a relational database, a foreign key is best described as:

A. A column that uniquely identifies each row in its own table
B. A column in one table that references the primary key of another table, establishing a relationship between them
C. A password or security credential used to access the database
D. A column that stores encrypted financial data for confidentiality purposes

**12.** According to this chapter, which stage of the analytics workflow is typically the most time-consuming?

A. Defining the question
B. Data preparation and cleaning
C. Visualization
D. Communication of findings

**13.** The Adventure Works Cycles dataset is most valuable for managerial accounting exercises because it includes:

A. A complete chart of accounts and general ledger
B. Manufacturing cost data including work orders, bills of materials, and scrap tracking
C. Only sales and customer data
D. Budget records and cost center allocations

**14.** Which of the following best describes why this textbook provides datasets in both Excel and SQLite formats?

A. Excel files are used only for financial accounting exercises and SQLite files are used only for auditing exercises
B. Students can work with the same underlying data regardless of whether a given chapter uses Excel, SQL, or Power BI
C. SQLite databases are smaller than Excel files and require less storage space
D. Excel format is for undergraduate students and SQLite format is for graduate students

**15.** A financial analyst uses PivotTables to summarize total revenue by product category and fiscal quarter. The analyst notices that revenue in one category declined sharply in the third quarter and investigates the underlying transactions to determine the cause. The summarization step is an example of descriptive analytics. What type of analytics would applying a regression model to forecast fourth-quarter revenue in that category represent?

A. Descriptive analytics
B. Predictive analytics
C. Prescriptive analytics
D. The regression would not be considered analytics because it involves statistics

---

## Applied Exercises

### Financial Accounting Exercises {.exercise-perspective .financial-accounting .unnumbered}

**Exercise 1.1 (Financial Accounting): Mapping Datasets to the Financial Reporting Cycle**

**Dataset:** All three (Northwind, AdventureWorks, ERPNext)

**Scenario.** You are a financial reporting analyst preparing a memorandum for your supervisor that assesses the analytical capabilities of three data sources your company has available. Your supervisor wants to understand which data source is best suited for specific financial reporting tasks.

**Requirements.** (1) Open each of the three textbook datasets in Excel and examine the available tables. For each dataset, identify which tables contain data that relates to revenue recognition, accounts receivable, inventory, and cost of goods sold. (2) For each of the four financial reporting areas listed above, determine which dataset provides the most complete data for analysis. Write a brief explanation (two to three sentences) for each area, identifying the specific tables you would use. (3) Identify one financial reporting task that can be performed with ERPNext data but cannot be performed with either Northwind or AdventureWorks data, and explain why. (4) Prepare a one-page summary memorandum presenting your findings in a format suitable for your supervisor.

**Deliverable.** A one-page written memorandum that compares the three datasets from a financial reporting perspective, identifying specific tables and explaining your reasoning.


**Exercise 1.2 (Financial Accounting): Identifying Revenue Data Across Datasets**

**Dataset:** Northwind and AdventureWorks

**Scenario.** You are a staff accountant asked to determine what revenue-related information is available in two of your company's data systems so that the team can plan a revenue trend analysis for the upcoming quarterly review.

**Requirements.** (1) Open both the Northwind and AdventureWorks datasets in Excel. Identify all tables that contain revenue or sales-related data. Record the table names and the column names that are most relevant to revenue measurement (such as amounts, dates, and product identifiers). (2) For each dataset, determine the total number of sales transactions recorded. Note the date range covered by the sales data. (3) Compare the two datasets in terms of the level of detail available for revenue analysis. Which dataset provides geographic (territory) information about sales? Which dataset provides product cost information alongside revenue? (4) Write a brief comparison (three to five sentences) explaining which dataset you would recommend for a detailed revenue trend analysis and why.

**Deliverable.** A written comparison of the revenue data available in each dataset, with specific table and column references.


### Managerial Accounting Exercises {.exercise-perspective .managerial-accounting .unnumbered}

**Exercise 1.3 (Managerial Accounting): Evaluating Datasets for Cost Analysis**

**Dataset:** AdventureWorks and ERPNext

**Scenario.** You are a management accountant at a manufacturing company. Your controller has asked you to assess which of the company's data systems contains the information needed for a product cost analysis and a departmental budget review.

**Requirements.** (1) Open the AdventureWorks dataset in Excel and identify all tables that contain cost-related information. Look for tables related to product costs, work orders, production, and purchasing. List the table names and the columns most relevant to cost analysis. (2) Open the ERPNext dataset and identify all tables that contain budget and cost center information. List the table names and columns. (3) Determine which dataset is better suited for product-level cost analysis (comparing standard cost to actual cost for specific products) and which is better suited for departmental budget analysis (comparing budgeted amounts to actual spending by department). Explain your reasoning in three to five sentences. (4) Identify one managerial accounting question that requires data from both datasets to answer fully, and explain what tables from each dataset you would combine.

**Deliverable.** A written assessment that compares the managerial accounting capabilities of the two datasets, with specific references to tables and columns.


**Exercise 1.4 (Managerial Accounting): Understanding Operational Data Structures**

**Dataset:** AdventureWorks

**Scenario.** You have been asked to prepare a brief overview of the operational data available in the AdventureWorks database for a new manager who will be using this data to evaluate production performance.

**Requirements.** (1) Open AdventureWorks.xlsx and examine the worksheets related to production and manufacturing. Identify at least four tables that a production manager would find relevant. (2) For each table you identified, write one sentence describing what information it contains and how it might be used to evaluate production performance. (3) Identify the columns that appear in more than one table (these are the keys that connect the tables). Write two to three sentences explaining how these shared columns would allow you to combine information across tables for a more complete analysis. (4) Prepare a brief written overview (one half to one page) that the new manager could use as a reference when requesting reports.

**Deliverable.** A written overview of the production-related data in AdventureWorks, suitable for a non-technical manager audience.


### Auditing Exercises {.exercise-perspective .auditing .unnumbered} 

**Exercise 1.5 (Auditing): Assessing Data Availability for Audit Testing**

**Dataset:** All three (Northwind, AdventureWorks, ERPNext)

**Scenario.** You are a first-year auditor who has been assigned to plan the data analytics procedures for an upcoming engagement. Your senior has asked you to assess what data is available for three common audit tests: aging of receivables, testing for duplicate transactions, and journal entry testing for management override of controls.

**Requirements.** (1) For each of the three audit tests listed above, identify which of the three textbook datasets contains the data needed to perform the test. Be specific about which tables and columns you would use. (2) Determine which of the three datasets supports all three audit tests using a single data source. Explain your answer by identifying the specific tables. (3) Identify one limitation of the Northwind dataset for audit analytics purposes. What type of audit test cannot be performed with Northwind data, and why? (4) Write a planning memorandum (one page) that documents the data available for each test and recommends which dataset should be used for each purpose.

**Deliverable.** A one-page audit planning memorandum documenting data availability for three specified audit procedures.


**Exercise 1.6 (Auditing): Evaluating Journal Entry Data for Audit Purposes**

**Dataset:** ERPNext

**Scenario.** You are preparing for journal entry testing as part of an audit engagement. Before writing any queries or performing any analysis, you need to understand the structure of the journal entry data in the company's system.

**Requirements.** (1) Open ERPNext.xlsx and examine the JournalEntry and GLEntry worksheets. Identify all columns available in each table. (2) Determine which columns would be most useful for identifying journal entries that warrant audit attention. Consider columns related to the person who posted the entry, the date and time of posting, the amount, and any descriptions or references. (3) Write a brief assessment (three to five sentences) of whether the ERPNext data provides sufficient information to test for three common fraud risk indicators: entries posted outside of normal business hours, entries with round-dollar amounts, and entries posted just below an approval threshold. For any indicator where the data may be insufficient, explain what additional information would be needed. (4) Prepare a one-paragraph summary of your assessment for discussion with your audit senior.

**Deliverable.** A written assessment of the journal entry data structure in ERPNext, evaluating its suitability for audit testing of management override of controls.

---

## Further Reading

Appelbaum, D., Kogan, A., and Vasarhelyi, M. A. (2017). Big data and analytics in the modern audit engagement: Research needs. *Auditing: A Journal of Practice and Theory*, 36(4), 1-27. This paper outlines a research agenda for data analytics in auditing and provides a framework for understanding how the analytical techniques taught in this textbook relate to the evolving audit process. The paper's discussion of population-based testing versus sampling is particularly relevant to the arguments presented in this chapter.

Earley, C. E. (2015). Data analytics in auditing: Opportunities and challenges. *Business Horizons*, 58(5), 493-500. This article provides an accessible overview of how audit practice is changing due to data analytics and identifies specific opportunities for auditors who develop analytical skills. It is useful reading for students interested in the audit perspective.

Kokina, J., and Dagiliene, L. (2017). The digitization of the accounting profession: Perceived threats and opportunities. *Journal of Emerging Technologies in Accounting*, 14(1), 1-13. This survey-based study examines how accounting professionals perceive the impact of digitization and analytics on their work. The findings support the claim made in this chapter that analytics skills are increasingly demanded across all areas of the profession.

Provost, F., and Fawcett, T. (2013). Data science and its relationship to big data and data-driven decision making. *Big Data*, 1(1), 51-59. This paper defines data science as a discipline and describes the analytical workflow that underlies data-driven decision making. Although it addresses data science broadly rather than accounting specifically, the workflow it describes closely parallels the accounting analytics workflow presented in this chapter.

Richins, G., Stapleton, A., Stratopoulos, T. C., and Wong, C. (2017). Big data analytics: Opportunity or threat for the accounting profession? *Journal of Information Systems*, 31(3), 63-79. This paper examines the implications of big data for the accounting profession and discusses both the opportunities for accountants who develop analytics skills and the threats for those who do not. It provides evidence supporting the labor market arguments presented in this chapter.

Vasarhelyi, M. A., Kogan, A., and Tuttle, B. M. (2015). Big data in accounting: An overview. *Accounting Horizons*, 29(2), 381-396. This paper provides a comprehensive overview of how big data and analytics are affecting accounting practice, research, and education. It is one of the most cited papers on accounting analytics and offers valuable context for understanding why this textbook exists.

IFAC (International Federation of Accountants). (2019). *Technology and the profession: A guide for professional accountancy organizations.* IFAC. This guidance document describes the technology-related competencies that accounting graduates need and how professional bodies can integrate these competencies into their qualification frameworks. It supports the claim that analytics is recognized as a core competency by international standard-setting bodies.
