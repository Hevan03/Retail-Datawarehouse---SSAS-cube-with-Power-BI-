# Retail Data Warehouse & SSAS Cube with Power BI

An end-to-end Business Intelligence solution that transforms raw retail transactional data into an enterprise-grade analytical environment. This project demonstrates the complete data pipeline lifecycle: from source database normalization, automated SSIS ETL pipelines (handling Slowly Changing Dimensions), SSAS OLAP cube building, to interactive Power BI and Excel dashboards.

---

## 🏗️ Project Architecture

[ Raw CSV Files ] ──> [ SSIS ETL ] ──> [ Retail_Staging ] ──> [ Retail_DW (Star Schema) ]
[ Power BI / Excel ] <── [ MDX / KPIs ] <── [ SSAS Multidimensional Cube ] ◄────┘

## 📊 Data Source & Schema Design

* **Source Dataset Link:** `https://www.kaggle.com/datasets/buharishehu/retail-sales-dataset/data`

### 💎 Data Warehouse Star Schema (`Retail_DW`)
* **FactSales:** Stores key operational metrics: `Quantity`, `UnitPrice`, `CostPrice`, `Discount`, `TotalAmount`, `TotalCost`, and processing duration metrics.
* **`DimCustomer` (SCD Type 2):** Tracks historical customer profile changes using `StartDate`, `EndDate`, and an `isCurrent` flag to preserve history.
* **`DimProduct`:** Flattens the original product categories and subcategories into a high-performance dimension.
* **`DimStore`:** Contains physical retail storefront data categorized by region and city.
* **`DimDate`:** Includes full time-intelligence mapping (Year, Quarter, Month, Day) along with custom regional holiday tracking.

---

## ⚙️ Core Technical Implementation

### 1. Automated SSIS ETL Pipelines
* **Staging Phase:** Extracts raw transactional data and lands it into `Retail_Staging` to decouple analytical loads from operational processes.
* **Data Warehouse Phase:** Uses **Lookup Transformations** to map operational business keys to data warehouse surrogate keys.
* **SCD Type 2 Automation:** Automatically expires old customer records (`isCurrent = 0`) and inserts a new active row (`isCurrent = 1`) when profile changes are detected.

### 2. SSAS Multidimensional Cube
* **Custom Hierarchies:** Built to enable lightning-fast drill-downs:
  * *Calendar:* `Year ──> Quarter ──> Month ──> Date`
  * *Product:* `Category ──> SubCategory ──> ProductName`
  * *Geography:* `Region ──> City ──> StoreName`
* **Key Performance Indicators (KPIs):** Integrated native MDX scripts calculating live sales performance against dynamic target thresholds, complete with Red/Yellow/Green status indicators.

### 3. Reporting & Visualization Layer
* **Power BI Dashboards:** Features interactive executive summary pages, geographical map analysis, and context-aware **Drill-Through Actions** that allow users to click a visual element to view granular transaction rows.
* **Excel Integration:** Connected directly to the live SSAS OLAP cube for ad-hoc PivotTable analysis and slicing.

---

## 🚀 How to Run the Project

1. **Database Setup:** Execute the provided SQL scripts to generate the `Retail_Staging` and `Retail_DW` databases.
2. **Run ETL:** Open the SSIS project in Visual Studio, update your connection strings, and run the master package to populate the warehouse.
3. **Deploy Cube:** Open the SSAS project in Visual Studio and deploy the multidimensional cube to your local Analysis Services instance.
4. **View Reports:** Open the Power BI `.pbix` file, connect it to your local SSAS server instance, and interact with the data.

---

### 🎓 Academic Reference
This project was engineered by **Hevan Kavidu** as part of academic coursework for the **Sri Lanka Institute of Information Technology (SLIIT)**. It maps directly to the implementation details specified in **IT23578678_DWBI_Assignment_1.pdf** and **Assignment2_IT23578678_compressed.pdf**.
