# ETL | Building Sales Data Mart | SSIS
# *Data Integration and Transformation Project Using SSIS*

Certainly! Below is the full description you can copy and paste for your GitHub project.

---

## Project Title: Comprehensive ETL Process for Data Transformation and Loading from Data Warehouse to SQL Server

### Overview
This project is a robust ETL (Extract, Transform, Load) process designed to extract data from a SQL Server-based data warehouse, transform it to meet business requirements, and load it into a destination SQL Server database. The ETL process is managed and executed using SQL Server Integration Services (SSIS), incorporating extensive error handling, data validation, and transformation logic to ensure accurate and efficient data processing.

### Project Description

#### 1. **Data Sources**
   - **Excel Source**: 
     - **Purpose**: To extract raw data stored in Excel files, which might contain sales figures, customer information, or other business metrics.
     - **Details**: 
       - Data is read from an Excel file using the Excel Source component.
       - The extracted data is converted using a Data Conversion task to ensure compatibility with SQL Server data types before loading.

   - **SQL Server Data Sources**: 
     - **Tables Involved**:
       - **Customers**: Stores customer details.
       - **Products**: Contains product-related information.
       - **Sales Order Header**: Summary information about sales orders.
       - **Sales Order Details**: Detailed line items of each sales order.
       - **Other Tables**: Includes Territory, Date, and other related dimensions or lookup tables.
     - **Purpose**: To provide foundational data required for transformation and loading into the destination database.

#### 2. **Data Transformation**
   - **Derived Column Transformation**:
     - **Purpose**: 
       - To create new columns based on expressions, such as calculating new fields, formatting strings, or generating computed values.
       - Examples include calculating total order value, formatting dates, or creating status flags.
     - **Usage**: 
       - Applied in various stages of the ETL process to add or modify columns before loading data into the destination.

   - **Lookup Transformations**:
     - **Purpose**: 
       - To enrich data by adding related information from other tables, ensuring data consistency and integrity.
       - Common lookups include matching product IDs to product names, customer IDs to customer details, etc.
     - **Details**:
       - **LKP - Product**: Matches product IDs to retrieve product names and descriptions.
       - **LKP - Customers**: Matches customer IDs to retrieve customer information.
       - **LKP - Territory**: Matches territory codes to retrieve region-specific information.
       - **LKP - Date**: Ensures that date fields are aligned with the organizational calendar.
       - **Error Handling**: If a lookup fails (e.g., no match found), the row is either redirected to an error flow or a default value is applied.

   - **Union All Transformation**:
     - **Purpose**: 
       - To combine multiple data streams into a single unified dataset.
       - This is useful when merging data from different sources or tables before loading it into a destination table.
     - **Details**:
       - Multiple inputs, such as different regions’ sales data, are combined into a single output stream.

   - **Merge Join Transformation**:
     - **Purpose**: 
       - To perform a join between two sorted datasets, similar to a SQL JOIN operation.
       - Typically used to merge sales order headers with their corresponding details.
     - **Details**:
       - **Join Type**: Inner join, left outer join, or full outer join based on the business requirement.
       - **Input Streams**: Sales Order Header and Sales Order Details.

   - **Slowly Changing Dimension (SCD)**:
     - **Purpose**: 
       - To manage changes in dimension data over time, ensuring historical data is preserved while updating current information.
     - **Types of Changes**:
       - **Type 1**: Overwrites old data with new data.
       - **Type 2**: Adds new records for changes, preserving historical data.
     - **Usage**: 
       - Applied to dimensions such as Customers or Products, where changes in attributes need to be tracked over time.

#### 3. **Data Loading**
   - **OLE DB Destination**:
     - **Purpose**: 
       - To load transformed data into the destination SQL Server database.
       - Ensures that data is inserted, updated, or merged based on the ETL logic.
     - **Details**:
       - Data from various transformations is loaded into specific destination tables.
       - Configurations include mappings between input columns and destination table columns.

   - **Insert Destination for Errors**:
     - **Purpose**: 
       - To capture and store rows that fail validation or lookup processes.
       - This allows for further analysis of why certain rows were not successfully processed.
     - **Details**:
       - Error rows are redirected to a separate error logging table or file for review.

#### 4. **Error Handling**
   - **Conditional Splits and Redirects**:
     - **Purpose**: 
       - To manage rows that do not meet certain criteria, redirecting them to appropriate error handling or logging mechanisms.
     - **Details**:
       - Examples include redirecting rows with null values, failed lookups, or validation errors.

   - **Data Validation**:
     - **Purpose**: 
       - To ensure that the data loaded into the destination is accurate and consistent with business rules.
     - **Details**:
       - Validation tasks include checking for nulls, data type mismatches, and out-of-range values.

#### 5. **Fact Table Processing**
   - **DFT Fact Table**:
     - **Purpose**: 
       - To process and load data into the central fact table, which stores transactional data for analysis.
     - **Details**:
       - The fact table is the core of the star schema, linking to dimension tables through foreign keys.
       - Data is aggregated, summarized, or calculated as needed before loading.

   - **SQL Task - Update Last Date**:
     - **Purpose**: 
       - To track the last successful data load date, ensuring that only new or updated records are processed in future ETL runs.
     - **Details**:
       - This date is stored in a control table and updated after each successful ETL run.

#### 6. **Auxiliary Tasks**
   - **Get Last Load Date**:
     - **Purpose**: 
       - To retrieve the date of the last successful ETL execution, determining the starting point for the current data extraction.
     - **Details**:
       - This date is used to filter source data, ensuring that only new or modified records are processed.

### Features
- **Comprehensive Data Transformation**: Handles complex data transformations, including derived columns, lookups, and merging datasets.
- **Robust Error Handling**: Implements error handling strategies to capture and manage data discrepancies, ensuring data quality.
- **Historical Data Management**: Utilizes Slowly Changing Dimensions (SCD) to track changes in dimension data over time.

### Technologies Used
- **SQL Server Integration Services (SSIS)**
- **SQL Server** for both source and destination databases
- **Excel** for raw data input

### Setup Instructions
1. **Prerequisites**: 
   - Ensure that SQL Server and SSIS are installed and configured.
   - The necessary databases and tables should be created on the SQL Server instance.
   - Excel files must be accessible in a specified directory.

2. **Configuration**:
   - Update the connection managers in the SSIS package to point to the correct SQL Server instance, databases, and file paths.
   - Configure any necessary environment variables or parameters.

3. **Execution**:
   - Open the SSIS package in SQL Server Data Tools (SSDT).
   - Run the package, monitoring the execution through the SSIS interface for any errors or warnings.

### Project Files
- **SSIS Package (.dtsx)**: Contains all the ETL logic, including data flows, control flows, and transformations.
- **SQL Scripts**: Includes any scripts needed to set up or maintain the database schema and control tables.
- **Documentation**: Detailed README and possibly other documents explaining the package’s logic, configuration, and use.
