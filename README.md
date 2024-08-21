# Debug-for-unmatched-rows-in-SQL
# SQL Debug Process: Subscription Data Analysis

## Overview

This SQL script is designed to debug and retrieve detailed subscription data for specific products (e.g., 'VHR', 'VHR Verified') for companies. The script involves multiple steps, including filtering and joining data from various tables, calculating key dates, and excluding unwanted records. The final result provides a comprehensive view of subscription details, including company information and their subscription history.

## Key Components

### 1. **SubsALL CTE (Common Table Expression)**
- **Purpose**: 
  - This CTE extracts the most recent subscription data for each company. It filters subscriptions based on product type and ensures that only active subscriptions as of a specific date are included.
- **Key Fields**:
  - `CompanyId`: Unique identifier for the company.
  - `ProductType`: Type of the product associated with the subscription.
  - `SubscriptionId`: Unique identifier for the subscription.
  - `Product`: Specific product subscribed to (e.g., 'VHR', 'VHR Verified').
  - `StartDate`: Start date of the subscription.
  - `EndDate`: End date of the subscription, considering cancellation effective dates.
  - `monthlyprice`: Monthly price associated with the subscription.
  - `hasicbcsubscription`: Indicates whether the subscription is part of an ICBC bundle.
  - `SubscriptionProductBundleId`: Identifier for the product bundle associated with the subscription.
  - `N`: Row number to identify the latest subscription per company.

### 2. **s2 CTE**
- **Purpose**: 
  - This CTE calculates the earliest subscription start date for each company.
- **Key Fields**:
  - `StartDate`: The earliest start date of a subscription for each company.
  - `CompanyId`: Unique identifier for the company.

### 3. **Final Query**
- **Purpose**:
  - The final query joins the data from `SubsALL` and `s2` CTEs with additional company data from CRM and UVIP tables. It provides a comprehensive view of subscription details, company information, and first subscription date.
- **Filters Applied**:
  - The query filters out records where the territory ID belongs to certain categories (e.g., 'Internal', 'Lender', 'Government') and excludes test companies.
  - Only the latest subscription (`N=1`) is selected for each company.
- **Key Output Fields**:
  - `Product`: The product associated with the subscription.
  - `territoryidname`: The territory ID associated with the company.
  - `CompanyId`: Unique identifier for the company.
  - `companyname`: The name of the company.
  - `groups`: Dealer associations.
  - `industrycodename`: The industry code associated with the company.
  - `isParent`: Indicates whether the company is a parent company.
  - `ownername`: The name of the performance manager.
  - `managername`: The name of the dealer group manager.
  - `first_subscribed`: The earliest date the company subscribed to the product.
  - `StartDate`: The start date of the latest subscription.
  - `EndDate`: The end date of the latest subscription.
  - `monthlyprice`: The monthly price associated with the subscription.
  - `new_numcarsonlot`: Number of cars on the company's lot.
  - `hasicbcsubscription`: Indicates whether the subscription is part of an ICBC bundle.
  - `SubscriptionProductBundleId`: Identifier for the product bundle associated with the subscription.
  - `address1_stateorprovince`: The state or province associated with the company.
  - `N`: Row number used to filter the latest subscription.

## Usage

1. **Data Retrieval**:
   - Run the script in an SQL environment with access to the relevant `bi.lienquest` and `bi.crm` schemas to retrieve and analyze subscription data.
   
2. **Debugging**:
   - Use this script to debug issues related to subscription data retrieval, ensuring that only the most recent and relevant data is selected.
   - The script can be modified to adjust the filters, join conditions, and date parameters as necessary to suit different debugging needs.

## Dependencies

- The script relies on specific database schemas and tables like `Subscription`, `SubscriptionProduct`, `SubscriptionProductType`, `FilteredAccount`, and `Uvip_Company_Active`. Ensure these tables and schemas are accessible in your database environment.

## Author
- Yifan Wang

## Contact
- Email: [yifanwang.msc2024@ivey.ca](mailto:yifanwang.msc2024@ivey.ca)
- LinkedIn: [linkedin.com/in/yifanwang4869](https://linkedin.com/in/yifanwang4869)
