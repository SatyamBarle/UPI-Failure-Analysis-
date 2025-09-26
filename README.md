# UPI Failure Analysis Project

This project analyzes UPI (Unified Payments Interface) transaction failures using SQL for data extraction and Power BI for visualization. The objective is to identify key patterns and insights that explain why UPI payments fail across regions, banks, and time frames [page 1].

## Problem Statement

UPI transactions in India are rapidly growing, but failure rates due to technical and operational issues impact user experience and trust. This project investigates failure trends and their underlying causes to improve service reliability [page 1].

## Tools & Technologies

*   **SQL (MySQL/PostgreSQL)**: Data cleaning and querying [page 1].
*   **Power BI**: Dashboard development [page 1].
*   **Excel/CSV**: Initial data storage [page 1].

## Dataset Overview

The dataset contains **3000+** UPI transactions with the following columns: -
`transaction_id` - `bank_name` - `region` - `transaction_status` (Success/Failure) - `failure_reason` - `transaction_time` - `amount` [page 1].

## KPIs and SQL Queries

1.  **Total Transactions**
    ```sql
    SELECT COUNT(*) AS total_transactions FROM upi_transactions;
    ``` [page 1]
2.  **Total Failures**
    ```sql
    SELECT COUNT(*) AS failed_transactions FROM upi_transactions
    WHERE transaction_status = 'Failure';
    ``` [page 1]
3.  **Failure Rate (%)**
    ```sql
    SELECT ROUND(100.0 * (SELECT COUNT(*) FROM upi_transactions
    WHERE transaction_status = 'Failure') / (SELECT COUNT(*) FROM
    upi_transactions), 2 ) AS failure_rate_percentage;
    ``` [page 1]
4.  **Peak Failure Hours**
    ```sql
    SELECT EXTRACT(HOUR FROM transaction_time) AS hour, COUNT(*)
    AS failures FROM upi_transactions WHERE transaction_status =
    'Failure' GROUP BY hour ORDER BY failures DESC LIMIT 3;
    ``` [page 2]
5.  **Region-wise Failure Breakdown**
    ```sql
    SELECT region, COUNT(*) AS total_failures FROM
    upi_transactions WHERE transaction_status = 'Failure' GROUP BY
    region ORDER BY total_failures DESC;
    ``` [page 2]
6.  **Bank-wise Failure Breakdown**
    ```sql
    SELECT bank_name, COUNT(*) AS failed_txns FROM
    upi_transactions WHERE transaction_status = 'Failure' GROUP BY
    bank_name ORDER BY failed_txns DESC;
    ``` [page 2]
7.  **Failure Reasons Distribution**
    ```sql
    SELECT failure_reason, COUNT(*) AS count FROM
    upi_transactions WHERE transaction_status = 'Failure' GROUP BY
    failure_reason ORDER BY count DESC;
    ``` [page 2]

## Power BI Dashboard Features

*   **KPI Cards**: Total transactions, failure rate, total failures [page 2].
*   **Line Graph**: Monthly/Hourly transaction failures [page 2].
*   **Bar Chart**: Failure reasons, region-wise failures, bank-wise breakdown [page 2].
*   **Filters/Slicers**: Region, bank, time [page 2].

## Key Insights

*   Peak UPI failures occur between **6 PM to 8 PM** .
*   **SBI recorded the highest number of failures** .
*   The leading cause of failure is **server issues**, accounting for nearly **14%** of all failed transactions.

## Conclusion

This project highlights how SQL + Power BI can drive actionable insights in fintech operations. Optimizing infrastructure during peak hours and improving server reliability can significantly reduce UPI failure rates [page 2].


