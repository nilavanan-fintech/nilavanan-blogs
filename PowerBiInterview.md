# Power BI — Top 100 Interview Questions & Answers

A structured collection of the most commonly asked Power BI interview questions, organized by topic, from beginner to advanced.

---

## 1. Power BI Basics (Q1–15)

**1. What is Power BI?**
Power BI is a business analytics tool by Microsoft used to visualize data, build interactive reports and dashboards, and share insights across an organization.

**2. What are the main components of Power BI?**
Power BI Desktop, Power BI Service (app.powerbi.com), Power BI Mobile, Power BI Report Server, Power BI Gateway, and Power BI Embedded.

**3. What is the difference between Power BI Desktop and Power BI Service?**
Desktop is a Windows application used to build reports, model data, and write DAX/queries locally. Service is the cloud platform used to publish, share, schedule refreshes, and collaborate on reports.

**4. What file formats does Power BI use?**
`.pbix` (report file), `.pbit` (template), `.pbids` (data source file), and `.pbip` (Power BI project format for source control).

**5. What is a dashboard vs a report in Power BI?**
A report is a multi-page collection of visuals built from one dataset, allowing interaction and filtering. A dashboard is a single-page, canvas of pinned visuals (tiles) that can come from multiple reports/datasets and supports Q&A but not page-level filtering.

**6. What is a dataset in Power BI?**
A dataset is the data model — tables, relationships, and calculations — that reports and dashboards are built on top of.

**7. What is a workspace in Power BI Service?**
A workspace is a container in the Service used to organize and collaborate on dashboards, reports, datasets, and dataflows with defined roles (Admin, Member, Contributor, Viewer).

**8. What are the licensing tiers in Power BI?**
Free, Pro, Premium Per User (PPU), and Premium (capacity-based), each differing in sharing limits, refresh frequency, storage, and advanced features (e.g., AI, paginated reports, larger datasets).

**9. What data sources can Power BI connect to?**
Excel, SQL Server, Azure services, SharePoint, Salesforce, Google Analytics, web APIs, OData, Oracle, MySQL, PostgreSQL, flat files (CSV/JSON/XML), and hundreds of other connectors.

**10. What are the storage modes in Power BI?**
Import, DirectQuery, and Composite (a mix of Import and DirectQuery within the same model), plus Live Connection to Analysis Services/Power BI datasets.

**11. What is the difference between Import and DirectQuery mode?**
Import loads data into Power BI's in-memory engine (fast, but data is only as fresh as the last refresh). DirectQuery sends queries live to the source (always current, but performance depends on the source and DAX limitations apply).

**12. What is a Composite model?**
A model that combines tables in Import mode and DirectQuery mode (or multiple DirectQuery sources), allowing flexibility between performance and real-time data.

**13. What is Power BI Gateway and why is it needed?**
A gateway is a bridge that allows the Power BI Service (cloud) to securely access on-premises data sources for scheduled refresh or DirectQuery. Types: Personal Gateway and Enterprise (Standard) Gateway.

**14. How many times can a dataset be refreshed in Power BI Pro vs Premium?**
Pro allows up to 8 scheduled refreshes per day; Premium (capacity/PPU) allows up to 48 per day.

**15. What is Power BI Report Server?**
An on-premises report server that hosts paginated reports and Power BI reports for organizations that cannot use the cloud Service.

---

## 2. Power Query / Data Transformation (Q16–35)

**16. What is Power Query?**
The data connection and transformation engine (ETL tool) inside Power BI, used to extract, clean, reshape, and load data using the M language.

**17. What is the M language?**
A functional, case-sensitive language used by Power Query to define data transformation steps; every applied step is actually M code under the hood.

**18. What is the difference between a Query and a Function in Power Query?**
A query returns a table or value from applied steps; a function is reusable logic (with parameters) that can be invoked repeatedly, often used for iterative or parameterized transformations.

**19. What is Query Folding?**
The process where Power Query translates its transformation steps back into the native query language of the source (e.g., SQL) so that the work is pushed down to the source system instead of being done locally — improving performance.

**20. How do you check if query folding is happening?**
Right-click the last applied step and check if "View Native Query" is enabled; if it's greyed out, folding has broken at that step.

**21. What are some common Power Query transformations?**
Remove/reorder columns, split/merge columns, pivot/unpivot, group by, filter rows, change data types, append/merge queries, add custom/conditional columns.

**22. What is the difference between Merge and Append queries?**
Merge joins two queries side-by-side based on matching columns (like a SQL JOIN), adding new columns. Append stacks queries vertically (like a SQL UNION), adding new rows.

**23. What are the types of joins available in Merge?**
Left Outer, Right Outer, Full Outer, Inner, Left Anti, and Right Anti joins.

**24. What is a Parameter in Power Query?**
A reusable, user-defined value (text, number, date, or list) that can drive things like file paths, filter values, or environment switching (e.g., Dev vs Prod).

**25. What is a Staging Query?**
A query used only as an intermediate step (often disabled from loading to the report) to hold reusable logic that other queries reference, reducing duplication and improving refresh performance.

**26. How do you handle errors in Power Query?**
Using `try...otherwise`, "Remove Errors," "Replace Errors," or the Keep/Remove Errors options in the ribbon, and by inspecting error details via the row-level error link.

**27. What is Unpivoting and when do you use it?**
Converting columns into rows so that attribute-value pairs are created; used to reshape "wide" data (e.g., monthly columns) into "long," analysis-friendly format.

**28. What is the difference between "Close & Apply" and "Refresh"?**
"Close & Apply" loads the current query design/transformations into the model for the first time (or after edits). "Refresh" re-runs the existing queries to pull the latest data from the source.

**29. What is a Dataflow in Power BI?**
A cloud-based ETL process (built with Power Query Online) that runs in the Power BI Service, stores data in Azure Data Lake (CDM format), and can be reused across multiple datasets/reports.

**30. What's the difference between a Dataflow and a Dataset?**
A dataflow is reusable ETL logic/data storage shared across datasets; a dataset is the semantic model (tables, relationships, measures) used directly by reports.

**31. How do you combine files from a folder in Power Query?**
Use the "Folder" connector, which lists all files in a folder; then use the "Combine Files" function to apply a consistent transformation to each file and append them into one table.

**32. What is the purpose of "Change Type with Locale"?**
It allows Power Query to interpret data types (especially dates and numbers) using a specific regional format, avoiding misinterpretation of formats like DD/MM/YYYY vs MM/DD/YYYY.

**33. What is a Custom Column vs a Conditional Column?**
A Custom Column uses M/DAX-like expressions for full custom logic. A Conditional Column is a UI-driven way to build simple if-then-else logic without writing code.

**34. How can you improve Power Query performance?**
Enable query folding, filter early, remove unnecessary columns/rows early in the steps, avoid volatile functions, use staging queries, and disable load for intermediate queries.

**35. What is the "Enable Load" option?**
A toggle that determines whether a query's output is loaded into the data model; disabling it for helper/staging queries reduces model size and refresh time.

---

## 3. Data Modeling (Q36–55)

**36. What is a Star Schema?**
A data model design with a central fact table (transactions/measures) connected to multiple dimension tables (descriptive attributes) via one-to-many relationships — the recommended approach for Power BI.

**37. What is a Snowflake Schema?**
A variation of the star schema where dimension tables are further normalized into related sub-dimension tables, creating a more complex, multi-level structure.

**38. Why is Star Schema preferred over Snowflake Schema in Power BI?**
It simplifies relationships, improves query and DAX performance (fewer joins), and is easier for the VertiPaq engine to compress and process.

**39. What is a Fact table and a Dimension table?**
A Fact table stores quantitative, transactional data (sales amount, quantity) and foreign keys. A Dimension table stores descriptive attributes (product, customer, date) used to filter and group facts.

**40. What are the types of relationships in Power BI?**
One-to-many, many-to-one, one-to-one, and many-to-many.

**41. What is the difference between a single-direction and bi-directional (cross-filter) relationship?**
Single-direction filters flow one way (dimension → fact). Bi-directional lets filters flow both ways, useful in specific scenarios but can cause ambiguity and performance issues if overused.

**42. What is a Composite/Many-to-Many relationship and when is it needed?**
Used when neither table has a unique key on the relationship column (e.g., a bridge table scenario); handled natively in Power BI since the "many-to-many" cardinality option was introduced.

**43. What is a Bridge Table?**
An intermediary table used to resolve many-to-many relationships cleanly, often storing only the unique key values shared by two fact/dimension tables.

**44. What is the VertiPaq engine?**
Power BI's in-memory columnar storage and compression engine used for Import mode datasets, enabling fast aggregation and query performance.

**45. What is Cardinality in relationships?**
It defines how rows in one table relate to rows in another — one-to-one, one-to-many, or many-to-many — and affects how filters propagate.

**46. What is a Role-Playing Dimension?**
A single dimension table (like Date) that relates to a fact table in multiple roles (e.g., Order Date, Ship Date, Delivery Date), typically handled using inactive relationships and `USERELATIONSHIP`.

**47. How do you handle a Role-Playing Date dimension in Power BI?**
Create one Date table, set one relationship as active, mark the others inactive, and use `USERELATIONSHIP()` in DAX measures to activate the specific relationship when needed.

**48. What is Row-Level Security (RLS)?**
A feature that restricts data access for specific users/roles by filtering rows in a table based on DAX expressions, defined via Roles in Power BI Desktop and assigned to users in the Service.

**49. What is the difference between Static RLS and Dynamic RLS?**
Static RLS hardcodes filter values per role; Dynamic RLS uses functions like `USERNAME()` or `USERPRINCIPALNAME()` combined with a mapping table so the same role adapts per logged-in user.

**50. What is a Calculated Table?**
A table generated using a DAX expression instead of being loaded from a data source, often used for helper tables like date tables or de-duplicated lists.

**51. What is a Calculated Column vs a Measure?**
A Calculated Column is computed row-by-row and stored in the model (increases file size). A Measure is computed on the fly at query time based on the current filter context (no storage cost).

**52. When should you use a Calculated Column instead of a Measure?**
When the result needs to be used for slicing, filtering, sorting, or in relationships — since measures can't be used in those contexts.

**53. What is a Date Table and why is it important?**
A dedicated table of contiguous dates used to enable accurate time intelligence (YTD, MTD, prior year, etc.); it should be marked as a "Date Table" in Power BI for correct behavior.

**54. What is the "Mark as Date Table" feature?**
A setting that tells Power BI a table is the official date dimension, enabling built-in time-intelligence functions to work correctly and validating there are no duplicate/missing dates.

**55. What is Auto Date/Time in Power BI and why is it often disabled?**
A built-in hidden date hierarchy Power BI creates automatically for date columns; it's often disabled in large models because it consumes memory and is replaced with a proper custom Date table.

---

## 4. DAX (Q56–80)

**56. What is DAX?**
Data Analysis Expressions — a formula language used in Power BI, Analysis Services, and Power Pivot to build measures, calculated columns, and calculated tables.

**57. What is Filter Context?**
The set of filters (from slicers, visuals, rows/columns, and relationships) applied to a calculation at the time it's evaluated.

**58. What is Row Context?**
The context that exists when a formula is evaluated row-by-row, such as in a calculated column or inside iterator functions (`SUMX`, `FILTER`, etc.).

**59. What does the CALCULATE function do?**
It changes the filter context of an expression by adding, removing, or replacing filters — it's the most important and versatile function in DAX.

**60. What is Context Transition?**
When `CALCULATE` (explicitly or implicitly) converts an existing row context into an equivalent filter context — commonly happens inside calculated columns or iterators referencing measures.

**61. What is the difference between FILTER and CALCULATE?**
`FILTER` returns a filtered table (used as an argument inside other functions); `CALCULATE` modifies the filter context under which an expression is evaluated, often taking a filter table as one of its arguments.

**62. What is the difference between SUM and SUMX?**
`SUM` aggregates a single column directly. `SUMX` is an iterator that evaluates an expression row-by-row over a table and then sums the results — used for calculations that need row-level logic (e.g., price × quantity).

**63. What are Iterator functions? Give examples.**
Functions that loop row-by-row over a table: `SUMX`, `AVERAGEX`, `COUNTX`, `MINX`, `MAXX`, `RANKX`, `FILTER`.

**64. What is the difference between ALL, ALLEXCEPT, and ALLSELECTED?**
`ALL` removes all filters from a table/column. `ALLEXCEPT` removes all filters except the ones specified. `ALLSELECTED` removes filters added inside the visual but retains filters from outside (e.g., slicers/page filters) — useful for "% of total within current selection" calculations.

**65. What is the difference between COUNT, COUNTA, COUNTX, and DISTINCTCOUNT?**
`COUNT` counts numeric values in a column. `COUNTA` counts non-blank values of any type. `COUNTX` iterates and counts results of an expression. `DISTINCTCOUNT` counts unique values in a column.

**66. What is the difference between RELATED and RELATEDTABLE?**
`RELATED` pulls a single related value from the "one" side of a relationship into the "many" side (used in row context). `RELATEDTABLE` returns a table of related rows from the "many" side when starting from the "one" side.

**67. What are Time Intelligence functions? Give examples.**
Functions that perform date-based calculations using a proper date table: `TOTALYTD`, `TOTALQTD`, `TOTALMTD`, `SAMEPERIODLASTYEAR`, `DATEADD`, `DATESYTD`, `PARALLELPERIOD`.

**68. What is the difference between DATEADD and SAMEPERIODLASTYEAR?**
`SAMEPERIODLASTYEAR` is a shortcut specifically for shifting one year back. `DATEADD` is generic and can shift by any interval (day, month, quarter, year) in either direction.

**69. What does the VAR keyword do in DAX?**
It defines a named variable to store an intermediate calculation result, improving readability and performance by avoiding repeated evaluation of the same expression.

**70. What is the difference between EARLIER and using VAR?**
`EARLIER` references an outer row context from within a nested row context (used in older/complex calculated columns). `VAR` is a modern, more readable alternative that explicitly stores a value for reuse, and is generally preferred.

**71. What does USERELATIONSHIP do?**
It activates an otherwise inactive relationship for the duration of a specific calculation, commonly used for role-playing dimensions.

**72. What is the difference between IF and SWITCH?**
`IF` evaluates a single true/false condition (can be nested). `SWITCH` evaluates an expression against multiple possible values, offering cleaner syntax for multi-condition logic (often used as `SWITCH(TRUE(), ...)` for range-based logic).

**73. What is RANKX used for?**
To rank values within a table based on an expression, respecting the current filter context — useful for leaderboards, top-N rankings, etc.

**74. What is the difference between DIVIDE and the "/" operator?**
`DIVIDE` safely handles division by zero (returning blank or a specified alternate result) without errors, while "/" throws an error/infinity on division by zero.

**75. What are Blank() and how do you handle blanks in DAX?**
`BLANK()` represents an empty/null value; functions like `ISBLANK`, `COALESCE`, or `DIVIDE`'s alternate result parameter are used to detect or replace blanks gracefully.

**76. What is a Quick Measure in Power BI?**
A pre-built, UI-generated DAX calculation (e.g., running total, % of grand total) that Power BI creates automatically based on user input, useful for learning DAX patterns.

**77. What is the difference between Implicit and Explicit measures?**
Implicit measures are auto-aggregated when a numeric field is dragged into a visual (e.g., default Sum). Explicit measures are DAX formulas written and named by the user, offering full control and reusability.

**78. What is Cumulative Total (Running Total) in DAX and how is it built?**
A total that accumulates values over a sequence (e.g., dates), typically built with `CALCULATE` + `FILTER(ALL(...))` comparing dates ≤ current date, or using `TOTALYTD`-style patterns.

**79. What is the difference between a Measure evaluated at Total level vs Row level?**
At the row level, a measure evaluates within that row's filter context; at the Total level, it re-evaluates across the aggregated filter context of all rows — which can produce different results for non-additive calculations like averages or ratios (this is why totals sometimes "don't add up").

**80. What is DAX Studio and why is it used?**
A free external tool used to write, run, analyze, and optimize DAX queries, view query plans, and measure performance (server timings) outside of Power BI Desktop.

---

## 5. Visualizations & Reporting (Q81–92)

**81. What are the common types of visuals in Power BI?**
Bar/column charts, line charts, pie/donut charts, tables, matrices, cards, KPIs, maps, scatter plots, gauges, slicers, and custom visuals from AppSource.

**82. What is the difference between a Table and a Matrix visual?**
A Table displays flat, row-based data without grouping hierarchy. A Matrix supports row/column grouping (like a pivot table) with expandable hierarchies and cross-tabulation.

**83. What is a Slicer and how is it different from a Filter pane?**
A Slicer is an on-canvas visual that lets end users interactively filter visuals by clicking/selecting values. The Filter pane is a side panel to apply filters (visual, page, or report level) that aren't necessarily visible on the canvas.

**84. What are the levels of filtering in Power BI reports?**
Visual-level, Page-level, Report-level, and Drillthrough filters — each with increasing scope.

**85. What is Drillthrough in Power BI?**
A feature that lets users right-click a data point and navigate to a detailed page pre-filtered by that context (e.g., drill from a region summary to a customer-level detail page).

**86. What is the difference between Drill Down and Drillthrough?**
Drill Down moves through a hierarchy within the same visual (e.g., Year → Quarter → Month). Drillthrough navigates to an entirely different report page filtered by the selected value.

**87. What is a Bookmark in Power BI?**
A saved snapshot of a report page's current state (filters, visual visibility, selections) that can be used for storytelling, navigation buttons, or toggling views.

**88. What are Custom Visuals and where do you get them?**
Visuals beyond the default set, imported from AppSource or a local file, built by Microsoft or third parties to extend Power BI's visualization capabilities.

**89. What is Conditional Formatting in Power BI?**
Formatting (color scales, data bars, icons, rules) applied to visuals based on data values, used to highlight trends, outliers, or thresholds.

**90. What is a Tooltip page in Power BI?**
A custom report page designed to appear as a tooltip when hovering over a data point in another visual, showing extra contextual detail.

**91. What is the "Sync Slicers" feature?**
A feature that allows a slicer's selection to apply across multiple report pages, keeping filters consistent as users navigate.

**92. What is the difference between a Card, Multi-row Card, and KPI visual?**
A Card shows a single aggregated value. A Multi-row Card shows multiple records with several fields each. A KPI visual shows a value against a target with a trend indicator.

---

## 6. Performance, Administration & Advanced Topics (Q93–100)

**93. How can you optimize Power BI report performance?**
Reduce visuals per page, use Import mode where possible, optimize DAX (avoid iterators on large tables, use variables), reduce cardinality of columns, use aggregations, disable unnecessary interactions, and use Performance Analyzer to identify bottlenecks.

**94. What is the Performance Analyzer tool used for?**
A built-in Power BI Desktop tool that records the time taken by each visual (DAX query time, visual rendering time, etc.) to help diagnose slow reports.

**95. What are Aggregations in Power BI (Premium feature)?**
Pre-summarized tables (e.g., daily/monthly totals) that Power BI automatically queries instead of the detailed fact table when possible, improving performance on very large DirectQuery/Import datasets.

**96. What is Incremental Refresh?**
A feature (available with Premium, PPU, or certain Pro configurations) that refreshes only new/changed data within a defined date range instead of reloading the entire table, significantly speeding up refreshes for large datasets.

**97. What is the XMLA endpoint in Power BI?**
An interface (available on Premium/PPU) that allows external tools (like SSMS, Tabular Editor, DAX Studio) to connect directly to a Power BI dataset for advanced management, deployment, and querying — similar to Analysis Services.

**98. What is the difference between Power BI Premium (capacity) and Premium Per User (PPU)?**
Capacity-based Premium is licensed per organization/capacity (P SKUs) and allows sharing content with users who don't have individual Pro licenses. PPU is licensed per user and includes most Premium features but requires every viewer to also have a PPU license.

**99. What is Deployment Pipeline in Power BI?**
A feature that lets you manage the lifecycle of content across Development, Test, and Production workspaces, allowing controlled promotion of reports/datasets between stages.

**100. What are some best practices for building a scalable Power BI solution?**
Use a star schema data model, minimize calculated columns in favor of measures, build a proper date table, use Power Query staging/query folding, apply RLS where needed, keep visuals per page limited, use variables in DAX, leverage incremental refresh/aggregations for large data, and organize workspaces with deployment pipelines for governance.

---

*Use this list as a structured study guide — group by topic, practice explaining answers in your own words, and be ready to demonstrate concepts hands-on (e.g., writing a DAX measure or explaining a star schema) during the interview.*
