# PowerBI

## **What is Power BI?**

**Power BI** is a business analytics tool developed by Microsoft that allows users to connect to, visualize, and analyze data. It is designed to provide insights and help users make informed, data-driven decisions.

### **Key Features of Power BI**

Power BI offers a wide range of features and tools that enable users to:

1. **Connect to Various Data Sources**
    - Import data from a variety of sources such as Excel, SQL Server, SharePoint, and cloud services like Azure Blob, Azure Data Lake,SaaS connectors like Salesforce.
2. **Transform and Clean Data**
    - Use built-in Power Query tools to shape, clean, and prepare data for analysis.
3. **Create Interactive Reports and Dashboards**
    - Build visually appealing and interactive dashboards using a range of data visualizations.
4. **Collaborate and Share**
    - Share reports and dashboards with others and collaborate in real-time using the Power BI service.

### **Power BI Platforms**

Power BI is available on multiple platforms to support different user needs:

- **Power BI Desktop**
    
    A free application for Windows used to create and publish reports.
    
- **Power BI Mobile App**
    
    Available on iOS and Android for viewing and interacting with reports on the go.
    
- **Power BI Service (Online)**
    
    A cloud-based platform to share, collaborate, and distribute reports and dashboards.
    

### **Power BI Licensing**

Power BI offers both free and paid licensing options:

- **Power BI Desktop** – Free to use and ideal for individual report creation.
- **Power BI Pro** – A subscription-based version that includes sharing, collaboration, and advanced features.
- **Power BI Premium** – Offers dedicated cloud capacity, larger data volumes, and enterprise-level capabilities.

## Understanding Power BI interface & How to Load CSV Data explain it.

When you open **Power BI Desktop**, you’ll see a clean workspace with several key areas. Here’s a breakdown of the main components:

### 1. **Ribbon (Top Menu)**

- Similar to Microsoft Excel.
- Contains tabs like **Home**, **View**, **Modeling**, **Insert**, and more.
- Provides options for data loading, visuals, transformations, and calculations.

### 2. **Canvas (Main Area)**

- This is your **design area** where you build reports and dashboards.
- You can drag and drop visuals (charts, graphs, tables) onto this space.

### 3. **Fields Pane (Right Side)**

- Lists **tables** and **fields** from your loaded datasets.
- You use these fields to create visuals by dragging them into the canvas or the visual editor.

### 4. **Visualizations Pane (Right Side)**

- Contains all types of charts and visuals (bar chart, pie chart, map, etc.).
- Allows customization like adding legends, axes, filters, and formatting.

### 5. **Views (Left Vertical Pane)**

- **Report View** – where you create and see visuals.
- **Data View** – see your raw data in table form.
- **Model View** – shows relationships between tables (data modeling).

---

## **How to Load CSV Data into Power BI**

Follow these simple steps to import a CSV file into Power BI Desktop:

### **Step 1: Open Power BI Desktop**

- Launch Power BI Desktop from your PC.

### **Step 2: Click on ‘Home’ > ‘Get Data’**

- From the top ribbon, click **Get Data** → select **Text/CSV** from the list.

### **Step 3: Choose Your CSV File**

- A file explorer window will open.
- Navigate to the folder where your `.csv` file is stored and click **Open**.

### **Step 4: Preview & Load**

- Power BI shows a preview of the CSV file.
- You can:
    - Click **Load** to import it directly.
    - Click **Transform Data** to open **Power Query Editor** for cleaning (optional).

### **Step 5: Data is Loaded**

- Once loaded, the data appears in the **Fields pane**.
- Click **Close & Apply** to load the cleaned data into the model
- You can now begin building visualizations using your data.

---

### **Steps to connect different sources:**

1. Open **Power BI Desktop** → **Home** tab → **Get data**.
2. **Excel**: Get Data → Excel → browse file → select sheet or table → click **Transform Data** (to clean) or **Load** (if already clean).
    - Say: “Use Excel for small reference files or exports from a system.”
3. **SQL Server**: Get Data → SQL Server → enter `Server` and `Database` → choose **Import** or **DirectQuery** → click **OK**.
    - Mention credentials/Auth: Windows, Database, or Azure AD.
    
4. **Cloud Services** (OneDrive / Azure / Salesforce / Google Analytics): Get Data → choose connector → authenticate via OAuth.
5. **On-premises sources**: explain that for on-premises SQL you set up **On-premises data gateway** in the Power BI Service, then configure the gateway for scheduled refresh.

---

### Publish, schedule refresh, and collaborate (Power BI Service)

**What to say:**

“Once the report is ready, I publish to the Power BI Service, set up scheduled refresh and gateways for on-prem sources, configure security, and then share via workspaces, apps, or embedding in Teams/SharePoint.”

**Step-by-step actions:**

1. **Publish**: In Desktop → Home → Publish → select workspace.
2. **Create workspace**: In Power BI Service → Workspaces → New workspace. Assign roles (Admin, Member, Contributor, Viewer).
3. **Datasets & refresh**:
    - Go to workspace → Datasets → Settings → Data source credentials (enter OAuth/Windows/Basic).
    - If source is on-premises, install **On-premises data gateway** and set it up in the Admin center; then map dataset to the gateway.
    - Schedule refresh: Dataset settings → Scheduled refresh → set frequency and time windows.
    - For large historical data, configure **Incremental refresh** using RangeStart/RangeEnd parameters in Power Query and enable incremental refresh in dataset settings.
4. **Create dashboard (optional)**: pin visuals from report to dashboard tiles; dashboards are single-page views for executives.
5. **Share & publish app**:
    - Package reports/dashboards into an **app** and publish to users or groups. Apps are the preferred way to distribute governed content.
6. **Row-level security (RLS)**:
    - In Desktop: Modeling → Manage Roles → create DAX filter (e.g., `[Region] = "EMEA"`). Test role with **View As**. Publish; in Service, assign users to roles.

---

### Import vs DirectQuery vs Live Connection

When we connect SQL Server or any data source in Power BI, we need to choose a **data connectivity mode**. The three main ones are **Import, DirectQuery, and Live Connection**.

**Import mode:**

- Data is copied into Power BI model.
- Very fast because it uses Power BI’s in-memory engine (VertiPaq).
- Best for **small to medium datasets** (up to a few GB after compression).
- Allows full Power Query transformations, complex DAX, and offline analysis.
- Needs scheduled refresh to keep updated.

**DirectQuery mode:**

- Data stays in the source (SQL Server, etc.).
- Power BI sends queries directly to the database each time user interacts.
- Good for **very large datasets** or when you need **real-time data**.
- Slower performance because every interaction hits the database.
- Limited transformations and some DAX functions don’t work.

**Live Connection:**

- Connects directly to an existing semantic model (like SSAS Tabular or a published Power BI dataset).
- No data is stored in the PBIX file.
- Used when your company already has a centralized model and you just build reports on top of it.

**One-liner to say:**

> “I use Import when I need speed and can refresh daily.
> 
> 
> I use **DirectQuery** when the dataset is too big or must always be live.
> 
> And I use **Live Connection** when IT has already built a shared model, and I only need to build reports on top of it.”
> 

---

### What is **On-premises** and what is a **Gateway**

👉 “On-premises means the data is stored in local company servers, not in the cloud. For example, a SQL Server database running inside the company network.”

**The challenge:**

Power BI Service is in the cloud, but on-premises data is inside the company network. The cloud can’t directly ‘see’ that data.

**Solution = On-premises Data Gateway.**

- It is a small software installed on a local server (or VM).
- It acts like a secure **bridge** between on-prem data and Power BI Service.
- It only sends queries & results, not the full data dump, so it’s safe.
- Allows scheduled refresh or live queries from the cloud to your local data.

**Steps to explain confidently:**

1. Install **On-premises Data Gateway** on a server inside company network.
2. Log in with your Power BI Service account (usually organizational account).
3. In Power BI Service, go to **Settings → Manage Gateways** and register the data source (e.g., SQL Server, credentials).
4. When publishing a report that uses SQL Server, map the dataset to the correct gateway.
5. Set up **Scheduled Refresh** so the dataset automatically refreshes daily/hourly.

**One-liner to say:**

> “Gateway is basically the connector between Power BI cloud and our on-prem SQL Server. Without it, Power BI Service cannot refresh or query local data sources.
> 

---

## **Top 10 Data Cleaning Methods in Power BI**

### 1. **Remove Columns and Rows**

- **Why:** Eliminate unnecessary data to keep your dataset clean and relevant.
- **How:** Right-click on the column or row → **Remove** or use **Remove Columns** on the ribbon.
- Remove rows: use the column filter (drop-down) and uncheck blanks or unwanted values; or **Home → Remove Rows → Remove Top Rows / Remove Blank Rows / Remove Errors**.

---

### 2.  **Filter Rows**

- **Why:** To include only relevant data (e.g., filter out blanks or specific values).
- **How:** Use the dropdown in column headers or use **"Keep Rows" / "Remove Rows"** options.

---

### 3.  **Change Data Types**

- **Why:** Power BI needs correct data types (e.g., Date, Text, Number) for accurate calculations and visuals.
- **How:** Use the **Data Type** icon next to the column name or choose from the ribbon.

---

### 4.  **Replace Values**

- **Why:** Clean inconsistent values (e.g., changing "N/A" or "null" to "0" or a blank).
- **How:** Right-click a column → **Replace Values** → enter value to find and value to replace with (e.g., replace `N/A` with `null` or `0`).

---

### 5. **Remove Duplicates**

- **Why:** To avoid skewed analysis due to repeated data.
- **How:** Right-click a column → **Remove Duplicates**.

---

### 6.  **Trim and Clean Text**

- **Why:** Remove unwanted spaces or non-printable characters in text columns.
- **How:** In Power Query, use **Transform → Format → Trim** and **Clean**.

---

### 7.  **Split Columns**

- **Why:** Break down complex fields like full names or addresses into parts.
- **How:** Use **Split Column** by delimiter (e.g., comma, space) or by number of characters.

---

### 8.  **Group By**

- **Why:** Summarize or aggregate data (e.g., total sales by region).
- **How:** Use the **Group By** feature under the **Transform** tab.
- **Home → Group By** → choose the grouping column (e.g., Region) and the aggregation (Sum of SalesAmount). Use **Advanced** to add multiple aggregations.

---

### 9.  **Pivot and Unpivot Columns**

- **Why:** Reshape your data structure (e.g., from long to wide format or vice versa).
- **How:**
    - **Pivot Column**: Transform unique row values into columns.
    - **Unpivot Columns**: Flatten wide tables into a long format.

---

### 10.  **Fill Down / Fill Up**

- **Why:** Fill blank cells in a column with the value above or below, useful in hierarchical data.
- **How:** Select the column → **Transform** → **Fill → Down** or **Up**.

## What is DAX in Power BI?

**DAX** stands for **Data Analysis Expressions**. It is a formula language used to define calculated columns and measures in **Power BI**. DAX formulas are used to perform calculations on data that has been loaded into a data model.

DAX is primarily used to:

### 1. **Create Calculated Columns**

- Adds new columns to your data table using custom logic.
- When computed: **during data refresh / when you create it**.
- Stored: **yes** — becomes a physical column in the model.
- Context: **row context** (works on each row).
- Use if: you need a value for every row (e.g., FullName, CategoryFlag).
- Downside: increases model size and can slow refresh / use more memory.
- Example: Extracting the year from a date field.
    
    ```sql
    Year = YEAR('Sales'[OrderDate])
    
    FullName = 'Customer'[FirstName] & " " & 'Customer'[LastName]
    
    ProfitPerRow = 'Sales'[SalesAmount] - 'Sales'[CostAmount]
    ```
    

### 2. **Create Measures**

- Performs **aggregations** or **calculations** (like sums, averages, counts) that respond to filters and interactions in reports.
- When computed: **at query / visual render time**.
- Stored: **no** — it’s a formula that returns a result on-the-fly.
- Context: **filter context** (responds to slicers, filters, visuals).
- Use if: aggregations (SUM, AVERAGE, % share, YTD, ratios).
- Benefit: lightweight, flexible, usually better for performance.
- Example: Calculating total sales.
    
    ```sql
    -- create in Model or Report view > New measure
    Total Sales = SUM('Sales'[SalesAmount])
    
    Profit = SUM('Sales'[SalesAmount]) - SUM('Sales'[CostAmount])
    
    Profit % = DIVIDE([Profit], [Total Sales], 0)  -- safe divide, returns 0 on divide-by-zero
    
    ```
    

Let’s say I have a Sales table with columns: `SalesAmount`, `CostAmount`.

- If I create a **Calculated Column**:

```sql
Profit = 'Sales'[SalesAmount] - 'Sales'[CostAmount]
```

This will store a profit value for **every single row**. If I have 10 million rows, I add 10 million new values — model becomes bigger and slower.

- If I create a **Measure**:

```sql
Profit = SUM('Sales'[SalesAmount]) - SUM('Sales'[CostAmount])
```

**When to use Calculated Column:**

- Only if you need a value **per row** that can’t be done in visuals. Example: FullName = FirstName & " " & LastName.

**When to use Measure:**

- For **aggregations** (sums, averages, ratios, percentages, KPIs).
- Almost always preferred, because measures are flexible, respond to filters, and don’t bloat the model.

👉 So you can say:

> “I prefer Measures over Calculated Columns because measures are lightweight, dynamic, and respond to filters. Calculated columns increase model size and should only be used if a value is needed at row level
> 

## **Difference Between Calculated Columns and Measures in Power BI**

**Calculated columns** are columns added to an existing table in the data model using a DAX formula. It stored in the model. It calculates row by row and adds a new column to the table. Increases dataset size because every row gets a value.

**Measures**, are formulas that are **evaluated at the time they are used** in a visualization or in a DAX expression. They are **not stored** in the data model and are **not associated with individual rows** in a table. Instead, they return aggregated results based on the current filter context.

It is not stored in the table; it is calculated **on the fly** depending on filters in the report.

## What are the three fundamental concepts of DAX?

Three fundamental concepts of DAX are as follows:

- **Syntax:** Syntax refers to the rules that define how the code is structured,
including the functions to be used. Syntax errors will result in an
error message.
- he grammar: commas, parentheses, function names, identifiers. E.g., `SUM(Table[Column])` must be written correctly or you get an error.

- **Functions:** Functions refer to instructions performed in a specific sequence to achieve a specific result.
- building blocks (SUM, SUMX, CALCULATE, FILTER, RELATED, DISTINCTCOUNT, TOTALYTD, etc.).
- 
- **Context:** There are two types of contexts in formulas - Row Context and Filter
Context. Row Context is applied when a formula uses a function that
filters a table to identify a specific row.

## **How is DAX Different from Excel Formulas?**

**DAX** is specifically designed for use in **data models**, while **Excel formulas** are design for use in **worksheets**.

As a result, DAX includes functions and syntax that are optimized for working with data in a **tabular format**, such as the ability to **filter**, **aggregate**, and **group data** using **tables** and **relationships**.

Unlike Excel, which works with individual cells, DAX operates on entire columns and tables, making it more suitable for large-scale analytical and business intelligence tasks.

## **How to Create a Calculated Column in Power BI (Using DAX)**

1. Go to the **Data View** in Power BI Desktop.
2. Select the table where you want to add the column.
3. Click on **"New Column"** in the toolbar.
4. Enter your DAX formula in the formula bar.

### **Example**:

```sql
FullName = Customers[FirstName] & " " & Customers[LastName]
#This creates a new column FullName by combining first and last names.
```

## **How to Create a Measure in Power BI (Using DAX)**

1. **Go to the "Model" or "Data" view** in Power BI Desktop.
2. **Select the table** where you want to create the measure.
3. On the ribbon, click **"New Measure"**.
4. Enter your **DAX formula** in the formula bar.
    
    Example:
    
    ```
    Total Sales = SUM(Sales[Amount])
    ```
    

The measure is now available in the **Fields pane** and can be used in visuals.

---

## What is **Evaluation Context**?

In Power BI (DAX), when we write a formula, the result depends on **context**.

Context means: **“which rows and which filters should the formula look at?”**

There are **three types** you must know:

1. **Row context** → “current row”
2. **Filter context** → “current filters”
3. **Context transition** → “changing row context into filter context”

---

### 1. Row Context (think: one row at a time)

- **Definition:** Row context means the formula is looking at *one row* of the table at a time.
- It happens automatically in **calculated columns** or when you use iterators like `SUMX`.

**Example in Power BI:**

1. Load a `Sales` table with `Quantity` and `UnitPrice`.
2. Go to *Modeling → New column*.
3. Write:
    
    ```sql
    LineTotal = Sales[Quantity] * Sales[UnitPrice]
    ```
    
- Quantity = 2, UnitPrice = 100 → `LineTotal = 2 * 100 = 200`
- **Second row:**
    
    Quantity = 3, UnitPrice = 150 → `LineTotal = 3 * 150 = 450`
    
- **Third row:**
    
    Quantity = 1, UnitPrice = 80 → `LineTotal = 1 * 80 = 80`
    
    Each row gets its **own calculation**. This is **row context**.
    

### 2. Filter Context (think: filters/slicers/visuals)

- **Definition:** Filter context means the formula result depends on the **filters** applied (slicers, page filters, rows/columns in a visual, or extra filters inside DAX).
- This is how **measures** work.

**Example in Power BI:**

1. Create a measure:

```sql
Total Sales = SUM(Sales[LineTotal])
```

### 3. What is Context Transition?

- **Definition:** Context transition happens when Power BI **converts a row context into a filter context**.
- This usually happens when you use **`CALCULATE()` inside a calculated column or inside a row-by-row operation**.
- Why? Because `CALCULATE` works **with filter context**, not row context. So Power BI “translates” the current row into a filter so the measure can calculate correctly.

Imagine a `Sales` table:

| Product | Quantity | UnitPrice | LineTotal |
| --- | --- | --- | --- |
| Shoes | 2 | 100 | 200 |
| Shoes | 3 | 150 | 450 |
| Bags | 1 | 80 | 80 |

And a **measure**:

```sql
Total Sales = SUM(Sales[LineTotal])
```

Now, you create a **calculated column**:

```sql
Sales for This Product = CALCULATE([Total Sales])
```

### Step-by-Step What Happens

1. **Row context:** Power BI looks at the first row → Product = Shoes
2. **Context transition with CALCULATE:** Power BI converts “this row = Shoes” into a **filter context**
3. **Measure evaluates:** `Total Sales` now only sums rows where Product = Shoes → 200 + 450 = 650
4. **Next row:** same thing for the second row → Product = Shoes → 650
5. **Third row:** Product = Bags → 80

Result in the calculated column:

| Product | Sales for This Product |
| --- | --- |
| Shoes | 650 |
| Shoes | 650 |
| Bags | 80 |

**Context transition:** CALCULATE **says:** “I need filter context, so let’s take the current row and turn it into a filter.”

## can you provide an example of using a filter funtion in dax formula

Using `FILTER()` in DAX

```sql
High Sales = 
CALCULATE(
    SUM(Sales[Amount]),
    FILTER(Sales, Sales[Amount] > 1000)
)
```

- This measure calculates the **total sales** where the **Amount is greater than 1000**.
- The `FILTER()` function applies a **row-level filter** to the `Sales` table.
- `CALCULATE()` modifies the context to apply this filter before summing the values.

### What is CALCULATE() in DAX?

**CALCULATE()** is a DAX function that **changes the filters** that apply to a calculation.

- Normally, measures in Power BI calculate results based on whatever filters are already applied in a visual.
- **CALCULATE() lets you override or add filters** to your calculation.
- It always **returns a single value**.

Think of it like:

> “I want to calculate something, but only for these specific conditions.”
> 

**Syntax** 

```sql
CALCULATE(<expression>, <filter1>, <filter2>, ...)
# <expression> = the calculation you want to do (SUM, COUNT, etc.)
# <filter> = the condition(s) you want to apply (can be table filters or logical conditions)
```

### Example 1: Total Sales for a specific product

**Scenario:**

You have a `Sales` table with `Quantity`, `UnitPrice`, and `ProductCategory`.

**Step 1:** Create a normal measure for total sales:

```sql
Total Sales = SUMX(Sales, Sales[Quantity] * Sales[UnitPrice])
```

- This calculates total sales for whatever filters are active (all products, or filtered by a slicer).

**Step 2:** Create a measure using `CALCULATE()` to find **Total Sales for “Bikes” only**:

```sql
Bike Sales = CALCULATE(
    [Total Sales],          -- expression
    Sales[ProductCategory] = "Bikes"  -- filter
)
```

**Step 3:** Create a measure using `CALCULATE()`:

```sql
Sales Last Year = CALCULATE(
    [Total Sales],
    SAMEPERIODLASTYEAR('Date'[Date])
)
```

## **Why Do We Need Pivot & Unpivot Columns in Power BI?**

### **Pivot Columns**

- **Purpose:** Converts **rows into columns**.
- **Why:** Useful when you want to **summarize** data or create a **wide format** table.
- **Example:** Convert months (Jan, Feb, Mar) from rows into column headers with their respective values.

### **Example**

Suppose you have this table:

| Month | Product | Sales |
| --- | --- | --- |
| Jan | A | 100 |
| Feb | A | 120 |
| Jan | B | 90 |
| Feb | B | 110 |

If you **pivot Month**, you get:

| Product | Jan | Feb |
| --- | --- | --- |
| A | 100 | 120 |
| B | 90 | 110 |

**Why useful:** Now each product has sales per month in columns — easier to compare and visualize.

### **Power BI Steps for Pivot**

1. Go to **Home → Transform Data** (opens Power Query Editor).
2. Select the column you want to turn into headers (e.g., `Month`).
3. Click **Transform → Pivot Column**.
4. Choose **Values Column** (e.g., `Sales`) for the values.
5. Click **OK**.

### **Unpivot Columns**

- **Purpose:** Unpivoting means **turning columns into rows**.
- You take columns that represent values and make them rows with a new column that tells what the original column was.
- **Why:** Helps in **normalizing data** to a tidy format that Power BI can analyze better.
- **Example:** Turn multiple year columns (2022, 2023, 2024) into two columns: `Year` and `Value`.

### **Example**

Suppose you have this table:

| Product | 2022 | 2023 | 2024 |
| --- | --- | --- | --- |
| A | 100 | 120 | 140 |
| B | 90 | 110 | 130 |

If you **unpivot Year columns**, you get:

| Product | Year | Sales |
| --- | --- | --- |
| A | 2022 | 100 |
| A | 2023 | 120 |
| A | 2024 | 140 |
| B | 2022 | 90 |
| B | 2023 | 110 |
| B | 2024 | 130 |

### **Power BI Steps for Unpivot**

1. Go to **Home → Transform Data**.
2. Select the columns you want to unpivot (e.g., `2022`, `2023`, `2024`).
3. Click **Transform → Unpivot Columns**.
4. Power BI creates two new columns:
    - `Attribute` → original column name (`Year`)
    - `Value` → the value in that column (`Sales`)

Now your data is **normalized** and ready for visuals.

## what is difference in sum and sumx

### **SUM**

- Adds up values in **a single column**.
- Simple total.

```sql
SUM(Sales[Amount])
```

### SUMX

- Adds up **calculated values row by row**.
- Used when you need to do a **calculation per row**, then total it.

**Example:**

```sql
SUMX(Sales, Sales[Price] * Sales[Quantity])
```

## **Custom Column vs. Conditional Column in Power BI**

### **1. Custom Column**

- **What it is:**
    
    A **flexible column** where you can write your **own formula** using M language.
    
- **Use it when:**
    
    You want to do **calculations**, combine columns, or apply logic manually.
    
- **Example:**
    
    Add a column that multiplies two existing columns:
    
    ```sql
    [Quantity] * [UnitPrice]
    ```
    

How to create:
Power Query Editor → Add Column tab → Click on Custom Column → Write your formula.

### **2. Conditional Column**

- **What it is:**
    
    A column created using **if-then-else logic** through a **no-code interface**.
    
- **Use it when:**
    
    You want to create a column **based on conditions** (like "if value is X, then Y").
    
- **Example:**
    
    If Sales > 1000, then “High”, else “Low”.
    
- **How to create:**
    
    Power Query Editor → **Add Column** tab → Click on **Conditional Column** → Use dropdowns to set conditions.
    

## Where is the data stored in Power BI?

Primarily, Power BI has two sources to store data:

**Azure Blob Storage:** When users upload the data, it gets stored here.

**Azure SQL Database:** All the metadata and system artifacts are stored here.

They are stored as either fact tables or dimensional tables.

## What are the different connectivity modes in Power BI

1. **Import Mode (Default Mode)**

- Imports a **copy of the data** into Power BI.
- The data is stored in the Power BI file (.pbix).
- Power BI will only store the metadata of the data tables involved and not the actual data
- Reports and visuals run fast because they use local in-memory data.

2. **DirectQuery Mode**

- **Does not import data** into Power BI.
- Queries are sent **directly to the database** each time a visual is loaded.

 3. **Live Connection**

- Connects **live to a Power BI dataset**, **Analysis Services**, or **Azure Analysis Services**.
- The data model is **not created in Power BI Desktop**; it comes from the source.

## What Are **Filters** in Power BI?

**Filters** in Power BI are tools that allow you to **limit or focus the data** shown in your report. Instead of showing *all* data, filters help you display **specific values, time periods, categories, etc.**

Example:

You have a sales report for all countries, but you want to see only sales in **India**. A filter helps you do that.

## Types of Filters in Power BI

Power BI offers **four main types of filters**:

---

### 1. **Visual-Level Filters**

Applies a filter **only to one chart or visual** on the report.

Example:You have two charts:

- Chart A: Shows Sales by Product
- Chart B: Shows Sales by Region

You can add a visual-level filter to Chart A to show only **products with sales > 1000**, while Chart B shows all data.

---

### 2. **Page-Level Filters**

Applies a filter to **all visuals on the same report page**.

Example:If you're viewing a sales dashboard for **January**, applying a page-level filter to January will update **all charts and tables on that page** to only show January data.

Use this when: You want to filter **everything on a page** by one rule (e.g., date, region, department).

---

### 3. **Report-Level Filters**

Applies a filter to **the entire report**, across **all pages**.

Example: Your report has 4 pages. You apply a filter to show only data from the **“Technology”** category. Now, *every page* only shows data for Technology.

 Use this when: You want a **global filter** that affects the whole report.

## What is a **Slicer** in Power BI?

A **Slicer** is a **visual filter** you add to your report canvas. It lets users **interactively filter** data by clicking options — like checkboxes or dropdowns.

Think of it like a **filter control** that your viewers can use.

Let’s say you have sales data across regions.

- Add a **Region Slicer** → Viewer selects “East” → All visuals update to show only East region data.

Slicer types include:

- **List**
- **Dropdown**
- **Date Range**
- **Between Slider**
- **Hierarchy**

##