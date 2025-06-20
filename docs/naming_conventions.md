# **Data Warehouse Naming Standards**

This guide defines the rules for naming schemas, tables, views, fields, and other objects across the data warehouse environment.

## **Contents**

1. [Core Guidelines](#core-guidelines)  
2. [Naming Tables](#naming-tables)  
   - [Bronze Layer](#bronze-layer)  
   - [Silver Layer](#silver-layer)  
   - [Gold Layer](#gold-layer)  
3. [Field Naming](#field-naming)  
   - [Surrogate Keys](#surrogate-keys)  
   - [System Metadata Columns](#system-metadata-columns)  
4. [Procedure Naming](#procedure-naming)

---

## **Core Guidelines**

- **Style**: Use `snake_case`. All letters lowercase, with underscores to split words.
- **Language**: Only English.
- **Keywords**: Avoid using any SQL reserved terms as object names.

---

## **Naming Tables**

### **Bronze Layer**

- Table names begin with the source system's name and retain the original table name without changes.
- Format: **`<source>_<table>`**  
  - `<source>`: Name of the input system (e.g. `crm`, `erp`)  
  - `<table>`: Exact table name from source system  
  - Example: `crm_customer_info` → CRM-provided customer data

### **Silver Layer**

- Naming stays identical to Bronze. Prefix with source system, keep source table name intact.
- Format: **`<source>_<table>`**  
  - Same rules as above apply.  
  - Example: `erp_order_detail` → Data from ERP system on order details

### **Gold Layer**

- Table names should reflect business logic and reporting layer semantics. Prefix based on type of table (fact, dimension, report).
- Format: **`<type>_<entity>`**  
  - `<type>`: Role of the table, e.g., `dim`, `fact`, `report`  
  - `<entity>`: Clear business descriptor  
  - Examples:  
    - `dim_customers` → Dimension table holding customer records  
    - `fact_orders` → Fact table with order transactions  
    - `report_revenue_monthly` → Aggregated monthly revenue data for reporting

#### **Naming Glossary**

| Prefix       | Description           | Example                            |
|--------------|------------------------|------------------------------------|
| `dim_`       | Dimension table         | `dim_product`, `dim_region`        |
| `fact_`      | Fact table              | `fact_sales`, `fact_shipments`     |
| `report_`    | Reporting layer output  | `report_user_activity`             |

---

## **Field Naming**

### **Surrogate Keys**

- All dimension table primary keys end in `_key`.
- Format: **`<entity>_key`**  
  - Example: `product_key` → Surrogate key in `dim_product`

### **System Metadata Columns**

- System-generated columns always start with `dwh_` and describe function/purpose.
- Format: **`dwh_<purpose>`**  
  - Example: `dwh_insert_time` → Timestamp for record load into DWH

---

## **Procedure Naming**

- Data load procedures follow this naming format:  
  **`load_<layer>`**  
  - `<layer>`: Refers to the specific zone—`bronze`, `silver`, or `gold`  
  - Examples:  
    - `load_bronze` → Populates Bronze tables  
    - `load_gold` → Final step into reporting-ready tables
