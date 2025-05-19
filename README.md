# SQL Analysis: Top Countries by Account Activity and Email Engagement

This project contains a BigQuery SQL query designed to analyze user account activity and email engagement across countries. The goal is to identify the **top 10 countries** by:

- Total number of active accounts
- Total number of emails sent

## 📊 Dataset Overview

The query uses the following tables from the `DA` dataset:

- `account`: User account data (e.g. verification status, send interval, unsubscribe status)
- `account_session`: Mapping between accounts and sessions
- `session`: Session metadata including session date
- `session_params`: Additional session-level parameters, including country
- `email_sent`: Email delivery data
- `email_open`: Email open events
- `email_visit`: Website visits via email links

## Query Logic

The query is structured using Common Table Expressions (CTEs) to progressively calculate and combine metrics:

### 1. `account_data`
Calculates the number of user accounts by:
- Session date  
- Country  
- Email send interval  
- Verification and unsubscribe status

### 2. `email_data`
Aggregates email activity by the **effective send date**, calculating:
- Number of emails sent  
- Emails opened  
- Visits from emails  

Grouped by the same dimensions as `account_data`.

### 3. `combined_data`
Unifies the account and email metrics into a single dataset using `UNION ALL`.

### 4. `aggregated_data`
Performs final aggregation by:
- Summing account and email metrics
- Calculating total values per country (used for ranking)

### 5. `ranked_data`
Assigns ranks to each country based on:
- Total number of accounts  
- Total number of emails sent  

### Final Output
Returns data **only for countries** ranked in the **top 10** by either:
- Total account count  
- Total sent messages  

## Use Cases

- Identify countries with the most active user base
- Track marketing email effectiveness by region
- Support business decisions with country-specific engagement metrics

## Technologies Used

- Google BigQuery
- Standard SQL (using CTEs and window functions)

---

> This analysis helps prioritize market focus based on both user activity and email performance metrics.

