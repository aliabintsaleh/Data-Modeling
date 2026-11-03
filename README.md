# Data Modeling
# Enterprise Sales, Product & Customer Snowflake Data Modeling Project

This repository showcases an end-to-end data engineering and modeling project. The primary focus of this project is **Data Extraction, Cleaning, Transformation (ETL), and establishing an optimized Snowflake Schema** centered around a core **Sales Fact table** supported by fully normalized Customer, Location, and Product hierarchies using Power BI and Power Query.

## 🛠️ Project Architecture & Workflow

The project follows a structured data pipeline to convert raw operational data into a high-performance relational database design optimized for analytical queries.


## 🎯 Key Achievements & Technical Steps

### 1. Data Cleaning & Transformation (ETL)
Using **Power Query**, the raw datasets were audited, cleaned, and transformed using the following techniques:
* **Handling Missing Values:** Resolved the issue of missing and `null` values in critical financial columns within the `Sales` table (such as price/sales values) by applying logical data-imputation techniques to preserve transactional calculation integrity.
* **Data Type Standardization:** Ensured all transaction dates, text identifiers, and numeric fields (revenue, quantity, prices) were explicitly converted to their correct formats to optimize memory layout and columnar compression.
* **Data Auditing & Deduplication:** Removed duplicated transactional, customer, and product records, filtered out corrupted rows, and stripped trailing whitespaces from textual fields.

### 2. Advanced Data Normalization (Snowflake Schema)
To maximize database efficiency, minimize storage, and eliminate data redundancy, the attributes were decoupled and structured into **5 distinct dimension tables**:
* **`Sales` (Fact Table):** Centralized all core business metrics, quantities, and transactional events.
* **Customer Branch:** 
  * `dim_customer`: Maintained unique customer profiles linked directly to transactions.
  * `dim_customer_state`: Isolated state-level details to normalize customer regional attributes.
  * `dim_location`: Created a dedicated location master table to handle standardized geographical hierarchies.
* **Product Branch:**
  * `dim_product`: Stored granular item attributes and specifications.
  * `dim_category`: Normalized product categories to manage group-level hierarchies without text duplication.

### 3. Dimensional Data Modeling & Relational Integrity
The final model view was designed following analytical database best practices:
* **Snowflake Schema Implementation:** Built a clean hierarchical model where the centralized **`Sales`** table is fed sequentially by multi-layered dimension lookup tables.
* **Relationship Optimization:** Configured optimal relationship cardinalities (**1-to-Many / 1:∞**) across the schema, enforcing **Single Direction Cross-Filtering** to guarantee high performance and prevent ambiguity in query paths.
* **Key Mapping:** Properly mapped primary and foreign keys across all branches (linking `dim_location` ➔ `dim_customer_state` ➔ `dim_customer`, and `dim_category` ➔ `dim_product` ➔ `Sales`), ensuring strict relational integrity.

---

## 📊 Technical Stack & Schema Details
* **Tool:** Power BI Desktop
* **Core Fact Table:** `Sales`
* **Dimension Tables:** 
  * `dim_customer` | `dim_customer_state` | `dim_location`
  * `dim_product` | `dim_category`
* **ETL Engine:** Power Query (M Language)
* **Design Pattern:** Snowflake Schema (Dimensional Modeling)

---

