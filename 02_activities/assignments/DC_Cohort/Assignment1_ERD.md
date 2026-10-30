# Assignment 1 – Logical Data Model

Tables: `customer` and `customer_purchases` (farmersmarket.db)

Relationship: **one-to-many**. Each customer makes one or many purchases.
Each purchase row belongs to exactly one customer, joined on `customer_id`.

```mermaid
erDiagram
    CUSTOMER ||--|{ CUSTOMER_PURCHASES : "makes"

    CUSTOMER {
        int customer_id PK
        nvarchar customer_first_name
        nvarchar customer_last_name
        char customer_postal_code FK "to postal_data"
    }

    CUSTOMER_PURCHASES {
        int product_id PK "FK to vendor_inventory"
        int vendor_id PK "FK to vendor_inventory"
        date market_date PK "FK to vendor_inventory"
        int customer_id PK "FK to customer"
        time transaction_time PK
        decimal quantity
        decimal cost_per_quantity
    }
```

| From | To | Join column | Type |
|---|---|---|---|
| customer | customer_purchases | customer_id | One (1) to one-or-many (1..N) |

Notes:

- Relationship type checked in the data: every customer_id in `customer`
  appears in `customer_purchases` (query returned 0 customers with no purchases).
- `customer_purchases` has a composite primary key:
  product_id, vendor_id, market_date, customer_id and transaction_time.
- `customer_postal_code` links to `postal_data`.
  `product_id`, `vendor_id` and `market_date` link to `vendor_inventory`.
  Those tables are outside this two-table model.
