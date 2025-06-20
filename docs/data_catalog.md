# 📁 Data Catalog – Gold Layer

## Overview  
The Gold Layer contains clean, business-aligned tables designed to support analytics and reporting. It includes both **dimension tables** (context) and **fact tables** (metrics).

---

## 🔹 `gold.dim_customers`

**Purpose**: Enriched customer profile data with demographic fields.

| Column Name     | Data Type    | Description                                                                 |
|------------------|--------------|-----------------------------------------------------------------------------|
| customer_key     | INT          | Surrogate key for each customer record                                     |
| customer_id      | INT          | Source system's unique customer ID                                         |
| customer_number  | NVARCHAR(50) | External-facing customer reference number                                  |
| first_name       | NVARCHAR(50) | Customer's given name                                                      |
| last_name        | NVARCHAR(50) | Customer's family or surname                                               |
| country          | NVARCHAR(50) | Country of residence                                                       |
| marital_status   | NVARCHAR(50) | Marital status (e.g., Married, Single)                                     |
| gender           | NVARCHAR(50) | Gender of the customer                                                     |
| birthdate        | DATE         | Date of birth (YYYY-MM-DD)                                                 |
| create_date      | DATE         | Date the record was created in the system                                  |

---

## 🔹 `gold.dim_products`

**Purpose**: Reference table with product attributes and hierarchy.

| Column Name         | Data Type    | Description                                                                 |
|---------------------|--------------|-----------------------------------------------------------------------------|
| product_key         | INT          | Surrogate key for each product record                                       |
| product_id          | INT          | Internal product ID                                                         |
| product_number      | NVARCHAR(50) | Alphanumeric product code                                                   |
| product_name        | NVARCHAR(50) | Name of the product with specs (e.g., color, type)                          |
| category_id         | NVARCHAR(50) | ID linking to product category hierarchy                                    |
| category            | NVARCHAR(50) | High-level product classification (e.g., Bikes, Components)                |
| subcategory         | NVARCHAR(50) | More granular grouping within category                                      |
| maintenance_required| NVARCHAR(50) | Indicates maintenance need (Yes/No)                                         |
| cost                | INT          | Cost price of the product                                                   |
| product_line        | NVARCHAR(50) | Product line or family (e.g., Road, Mountain)                               |
| start_date          | DATE         | Launch or availability date                                                 |

---

## 🔸 `gold.fact_sales`

**Purpose**: Transaction-level sales data, linked to customer and product dimensions.

| Column Name     | Data Type    | Description                                                                 |
|------------------|--------------|-----------------------------------------------------------------------------|
| order_number     | NVARCHAR(50) | Unique order ID (e.g., SO54496)                                             |
| product_key      | INT          | FK to `dim_products`                                                       |
| customer_key     | INT          | FK to `dim_customers`                                                      |
| order_date       | DATE         | When the order was placed                                                  |
| shipping_date    | DATE         | When the product was shipped                                               |
| due_date         | DATE         | When payment was due                                                       |
| sales_amount     | INT          | Total sale value per line item                                             |
| quantity         | INT          | Number of units ordered                                                    |
| price            | INT          | Unit price for the product                                                 |
