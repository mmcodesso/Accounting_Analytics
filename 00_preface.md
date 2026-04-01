---
number-sections: false
format:
  html:
    number-sections: false
---

# Preface {.unnumbered}


This book exists because the accounting profession has changed faster than most accounting curricula have adapted. Organizations now generate financial and operational data at a scale that makes traditional manual methods of analysis insufficient. Enterprise resource planning systems capture every transaction, every journal entry, every payment, and every production order in relational databases that contain millions of records. Auditors are expected to test entire populations rather than small samples. Management accountants are asked to explain variances, forecast performance, and identify operational drivers using data that lives in systems they were never trained to access. Financial reporting teams must reconcile, validate, and analyze data that flows from dozens of interconnected tables before it reaches the financial statements. The profession needs practitioners who can work directly with data, and accounting education needs textbooks that teach them how.

This textbook teaches accounting students to extract, prepare, analyze, and visualize data using three tools that are widely used in professional practice. Microsoft Excel serves as the foundation for data preparation, descriptive analytics, statistical modeling, and audit testing. SQL provides the ability to query relational databases directly, joining tables, aggregating results, and performing population-level analysis without relying on pre-built reports. Microsoft Power BI enables the creation of interactive dashboards and reports that communicate analytical findings to diverse audiences. These three tools cover the full analytics workflow from data access through communication of results, and they represent the toolkit that employers consistently identify as most relevant for entry-level accounting professionals (Sledgianowski, Gomaa, and Tan, 2017).

The book is built around three realistic datasets that students use throughout all twenty chapters, progressing from a simple wholesale distributor (Northwind Traders) through a mid-size manufacturer (Adventure Works Cycles) to a full enterprise resource planning environment with a complete accounting module (ERPNext Demo Company). All three are provided in both Excel workbook and SQLite database formats, so students work with the same underlying data regardless of which tool a given chapter uses. The About the Datasets section that follows this preface provides full descriptions of each database, including table counts, functional coverage, and a chapter-by-chapter appearance map.


## Why This Book

Several features distinguish this textbook from other analytics resources available to accounting instructors.

The first is its focus on accounting. General-purpose data analytics textbooks teach techniques using data from marketing, healthcare, sports, or other domains. Those examples are interesting but do not help accounting students see how analytics connects to the work they will actually do. Every example, exercise, and case in this book uses accounting data and addresses accounting questions. Students analyze revenue trends, prepare trial balances, test for duplicate payments, calculate cost variances, perform Benford's Law analysis, and build financial reporting dashboards. The analytical techniques are the same ones taught in general analytics courses, but the context is always accounting, which helps students transfer what they learn to professional practice.

The second is its three-perspective exercise structure. Every chapter includes applied exercises organized into three sections by accounting perspective. Financial Accounting exercises address reporting, disclosure, and compliance questions. Managerial Accounting exercises address costing, budgeting, performance measurement, and decision support questions. Auditing exercises address assurance, control testing, anomaly detection, and risk assessment questions. This structure ensures that students see how the same analytical technique serves different purposes depending on the professional role. An aging analysis, for example, appears as a financial reporting exercise (estimating the allowance for doubtful accounts), a managerial accounting exercise (assessing collection efficiency), and an auditing exercise (evaluating management estimates and selecting balances for confirmation). Students who encounter all three perspectives develop a broader understanding of how analytics creates value across the profession.

The third is its integrated tool progression. Many textbooks teach Excel, SQL, and visualization tools in isolation. This book teaches them as complementary stages of a single workflow. Part II covers Excel. Part III covers SQL. Part IV covers Power BI. Part V brings all three tools together in integrated projects where students extract data using SQL, analyze it in Excel, and present results in Power BI within a single engagement. This progression mirrors how analytics projects work in practice, where no single tool handles every stage.

The fourth is its design as an open educational resource. The book and all companion datasets are freely available, and every tool used in the exercises is either free or included with standard institutional licenses. The Open Access section on the book's landing page describes the licensing terms in detail.


## Pedagogical Design

The book follows a consistent pedagogical structure that reflects research on how students learn technical skills most effectively. Worked examples, immediate practice opportunities, and progressive complexity have been shown to support skill acquisition in technology-intensive courses (Borthick and Jones, 2000). Every chapter in this book applies these principles through a structured sequence.

Each chapter opens with four to six learning objectives written in measurable terms using action verbs drawn from Bloom's taxonomy. The objectives span multiple cognitive levels, from foundational understanding through application and analysis, so that both undergraduate and graduate students find appropriate challenges. Following the objectives, an opening scenario places the student in a realistic professional situation drawn from one of the three datasets. The scenario names a role, describes a concrete task, and motivates the material that follows by showing students why it matters before they learn how to do it.

The body of each chapter presents concepts in narrative paragraph form, supported by figures, tables, and diagrams. One to three guided tutorials are embedded within the conceptual content at the point where the relevant technique is introduced, so students read about a concept and immediately practice it before moving to the next topic. Each tutorial includes numbered steps, expected outputs, and a checkpoint that allows students to verify their work. Three types of callout boxes appear throughout the narrative. "In Practice" notes describe how the technique is used in professional settings. "Watch Out" notes warn about common errors and pitfalls. "Connecting the Dots" notes link the current topic to material in other chapters or other tools, helping students see the book as an integrated whole.

Each chapter closes with a summary, a list of key terms with definitions, ten to fifteen multiple choice questions spanning recall, application, and judgment, and applied exercises organized by the three accounting perspectives. Five comprehensive cases, one at the end of each of the book's five parts, provide extended multi-tool investigations that integrate material from all chapters in the part.

In-text citations in APA format appear throughout the narrative to support claims about professional practice, technique effectiveness, and adoption trends. Each chapter closes with a Further Reading section containing five to eight annotated references drawn from peer-reviewed journals, professional standards, and practitioner publications.


## Audience and Course Design

This textbook serves both undergraduate and graduate four-credit courses in accounting analytics or accounting information systems. A single text serves both audiences. The instructor controls the depth and rigor of classroom discussions and analyses to match the course level. Undergraduate courses can focus on the guided tutorials and foundational exercises. Graduate courses can emphasize the analytical judgment required by the applied exercises and comprehensive cases, assign additional readings from the Further Reading sections, and incorporate extended discussion of professional standards and research findings.

The book assumes no prior analytics or programming experience. Students need only the accounting knowledge gained from introductory financial and managerial accounting courses. Every technical concept is introduced from the ground up, and every tool is taught through step-by-step instruction before students are asked to work independently. Students who have prior experience with Excel, SQL, or Power BI will move through the early chapters faster and can focus their effort on the accounting applications and the more advanced techniques in later chapters.


## How This Book Is Organized

The book contains twenty chapters organized into five parts. Parts I through IV follow a deliberate progression. Part I (Chapters 1 through 3) builds the conceptual foundation without introducing any tools. Parts II, III, and IV each teach one tool in depth: Excel in Chapters 4 through 8, SQL in Chapters 9 through 12, and Power BI in Chapters 13 through 16. Part V (Chapters 17 through 20) integrates all three tools in applied projects that span financial reporting, cost accounting, forensic analytics, and emerging technologies. A comprehensive case closes each part, requiring students to combine material from all chapters in that part into a multi-component deliverable.

Six appendices provide reference material including a software installation guide, complete dataset documentation with Entity-Relationship diagrams, and quick reference guides for Excel functions, SQL syntax, and DAX functions. Appendix F maps every exercise in the book to the relevant competency areas in the AICPA, IMA, and IFAC frameworks, supporting instructors who need to align their course with accreditation requirements.


## A Note on Professional Standards and Research

This textbook references professional standards and peer-reviewed research throughout its chapters. These references serve two purposes. First, they ground the analytical techniques in the professional context where students will apply them. When a chapter on audit analytics references the AICPA's guidance on data analytics in auditing (AICPA, 2017), students see that the techniques they are learning are not academic exercises but tools that professional standards expect them to use. Second, the references connect the practical instruction to the broader body of knowledge in accounting and information systems. Students who read the annotated Further Reading sections will find pathways into the research literature that informs and extends what the textbook teaches.

The profession's integration of analytics into its competency frameworks has accelerated in recent years. The AICPA has embedded data analytics across its pre-certification curriculum. The IMA has emphasized technology and analytics in the Certified Management Accountant examination content. The IFAC has published guidance on the technology competencies that accounting graduates need (IFAC, 2019). These developments confirm that the skills taught in this book are not supplementary. They are foundational to the practice of accounting in the current environment.

---

# To the Student

You are beginning a book that will change how you work with accounting data. The accounting courses you have taken so far taught you to understand financial statements, apply standards, calculate ratios, and interpret results. Those skills remain essential. What this book adds is the ability to work directly with the data that produces those statements, ratios, and results. Instead of receiving a finished trial balance and analyzing it, you will learn to query a database, extract the general ledger entries, and build the trial balance yourself. Instead of reading a variance report, you will learn to calculate the variances from production data and present them in an interactive dashboard. Instead of reviewing a sample of transactions that someone else selected, you will learn to test the entire population and let the data reveal the anomalies.

This book assumes no prior experience with analytics or programming. If you have never written a SQL query, never built a PivotTable, and never opened Power BI, you are exactly the audience this book was written for. Every technique is introduced from the ground up with step-by-step guided tutorials that you can follow at your own pace. The tutorials build on one another, so the output of one often serves as the input for the next, and the complexity increases gradually across chapters.


## What to Expect

The book follows a consistent structure that will become familiar after the first few chapters. Each chapter opens with learning objectives that tell you what you will be able to do after completing the chapter. An opening scenario places you in a professional role and describes a task that motivates the material. The body of the chapter alternates between conceptual explanation and hands-on tutorials. Callout boxes provide practical tips, warnings, and connections to other parts of the book. Each chapter closes with a summary, key terms, review questions, and applied exercises.

The applied exercises at the end of each chapter are organized into three sections by accounting perspective. Financial Accounting exercises focus on reporting and disclosure tasks. Managerial Accounting exercises focus on costing, budgeting, and performance measurement. Auditing exercises focus on testing, anomaly detection, and assurance procedures. You will complete exercises in all three perspectives regardless of which area of accounting interests you most. This breadth is intentional. Analytics skills transfer across roles, and understanding how the same technique serves different purposes will make you a more versatile professional.


## The Three Tools

You will learn three tools in this book, each suited to a different stage of the analytics workflow.

Microsoft Excel is the tool you will use first. Chapters 4 through 8 teach you to organize data in structured tables, clean and prepare messy data, build PivotTables for summarization, run regression models, and perform audit analytics procedures. Excel is most powerful for ad hoc analysis, financial modeling, and workpaper preparation.

SQL is introduced in Chapters 9 through 12. SQL stands for Structured Query Language, and it is the standard language for retrieving data from relational databases. You will use a free, lightweight database system called SQLite that requires no server and runs on any operating system. SQL is most powerful when working with large datasets, when data spans multiple related tables that must be combined, and when you want to save and reuse your analytical procedures.

Microsoft Power BI is introduced in Chapters 13 through 16. Power BI is a business intelligence platform that lets you build interactive dashboards and reports. You will connect Power BI to the same datasets you used in Excel and SQL, create data models, write DAX formulas for calculated measures, and design dashboards that stakeholders can explore on their own.

In Part V of the book, you will use all three tools together. You will extract data with SQL, analyze it in Excel, and present results in Power BI within a single integrated project.


## The Three Datasets

You will work with three datasets throughout this book. All three are provided as both Excel workbooks and SQLite databases. You will become deeply familiar with them because you use them repeatedly across chapters, building cumulative knowledge of their structures, contents, and quirks. The datasets progress from a compact wholesale distributor (Northwind Traders, eight tables) through a mid-size manufacturer (Adventure Works Cycles, approximately seventy tables) to a full enterprise resource planning environment with a complete accounting module (ERPNext Demo Company). The About the Datasets section provides full descriptions of each database, including the specific chapters where each one appears.


## How to Succeed

The most important habit you can develop is to do the tutorials yourself rather than reading through them passively. Open the dataset, follow the steps, and verify your results at each checkpoint. When you make an error, diagnosing and correcting it teaches you more than getting it right the first time. The guided tutorials are designed so that you can complete them independently at your own pace, and they prepare you directly for the applied exercises that follow.

A second important habit is to read the conceptual material before jumping to the tutorials. The concepts explain why a technique works and when it is appropriate. The tutorials show you how to execute it. Both are necessary. A student who can execute a Benford's Law analysis without understanding what the results mean or when the test is appropriate has a technical skill but not an analytical one. This book aims to develop both.

Finally, pay attention to the connections across chapters and tools. The "Connecting the Dots" callout boxes link the current topic to material elsewhere in the book. The three-perspective exercise structure shows you how the same technique applies in different contexts. The comprehensive cases at the end of each part ask you to integrate everything you have learned. These connections are where the deepest learning happens, because they move you from knowing how to use a tool to understanding how to solve a problem.

---

# About the Datasets

This textbook is built around three datasets that students use throughout all twenty chapters. All three are provided in both Microsoft Excel workbook format and SQLite database format, so students work with the same underlying data regardless of whether a given chapter uses Excel, SQL, or Power BI. The datasets represent three different types of businesses at three levels of complexity, and the textbook introduces them from simplest to most complex.

**Northwind Traders** is a fictional small wholesale food distribution company. It buys specialty food products from suppliers around the world and sells them to retail and restaurant customers. The Northwind database contains eight core tables covering customers, orders, order details, products, product categories, suppliers, employees, and shippers. The database includes approximately 830 orders, 2,100 order line items, 77 products, and 91 customers. Northwind is compact and easy to understand, which makes it the primary dataset for the foundational chapters where students are learning new tools and techniques. It supports exercises in sales analysis, customer analytics, purchasing evaluation, and inventory review.

Northwind appears in Chapters 1 through 10, 12, 13, 14, 16, and 19.

**Adventure Works Cycles** is a fictional mid-size multinational bicycle manufacturer that designs, produces, and sells bicycles, components, clothing, and accessories through multiple sales territories. The AdventureWorks database contains approximately seventy tables organized across five functional areas covering sales, production, purchasing, human resources, and person management. The database includes manufacturing cost data such as bills of materials, work orders, production routing, and scrap tracking, along with multi-territory sales transactions and vendor purchase orders. AdventureWorks introduces the data complexity that students will encounter in manufacturing and multi-division organizations, and it supports exercises in cost accounting, production analysis, sales performance evaluation, and purchasing cycle testing.

AdventureWorks appears in Chapters 1, 3, 5 through 7, 10 through 13, 15 through 19.

**ERPNext Demo Company** is a fictional company operating within a full enterprise resource planning environment that includes a complete accounting module. The ERPNext database contains a chart of accounts, general ledger entries, journal entries, sales and purchase invoices, cost centers, budgets, payment entries, bank reconciliation records, stock ledger entries, and asset registers. ERPNext is the most accounting-rich dataset of the three. Students use it for financial statement preparation, general ledger analysis, budgetary control, audit testing, and integrated financial reporting. Because ERPNext mirrors the structure of a production ERP system, working with it gives students familiarity with the kind of data environment they will encounter in professional practice.

ERPNext appears in Chapters 1 through 3, 8, 11 through 13, 15 through 20.

The textbook introduces Northwind first because it is the simplest. AdventureWorks enters in the middle chapters as exercises grow more complex and students have built enough skill to work with richer data. ERPNext appears once students have enough analytical experience to work with a full accounting system. By the final chapters, students move fluently across all three datasets in integrated exercises. Complete documentation for every table in all three databases, including column names, data types, primary and foreign key relationships, and Entity-Relationship diagrams, appears in Appendix B.

---

# Acknowledgments

*[This section will acknowledge individuals and institutions that contributed to the development of this textbook, including reviewers, colleagues who class-tested draft chapters, students who provided feedback, and the open-source communities that maintain the tools and datasets used throughout the book.]*

---

# References

AICPA (American Institute of Certified Public Accountants). (2017). *Guide to audit data analytics.* AICPA.

Borthick, A. F., and Jones, D. R. (2000). The motivation for collaborative discovery learning online and its application in an information systems assurance course. *Issues in Accounting Education*, 15(2), 181-210.

IFAC (International Federation of Accountants). (2019). *Technology and the profession: A guide for professional accountancy organizations.* IFAC.

Sledgianowski, D., Gomaa, M., and Tan, C. (2017). Toward integration of Big Data, technology, and information systems competencies into the accounting curriculum. *Journal of Accounting Education*, 38, 81-93.