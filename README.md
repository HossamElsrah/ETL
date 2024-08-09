# ETL | Building Sales Data Mart | SSIS
# *Data Integration and Transformation Project Using SSIS*

Project Overview
Based on the image, the project appears to be a Data Warehouse ETL (Extract, Transform, Load) process that:

Extracts data from a SQL Server source system.
Transforms the extracted data using various data flow components like Derived Columns, Lookups, and Aggregations.
Loads the transformed data into a SQL Server destination system.
Implements Slowly Changing Dimensions (SCD) to handle changes in customer information over time.
Includes error handling mechanisms to manage potential issues during the ETL process.
Key Components and Processes
Data Sources:

SQL Server Source System (DRV-Source)
Excel Source (for Fact Table data)
Data Transformations:

Derived Columns: Create new columns or modify existing ones.
Lookups: Match data from one source to another.
Aggregations: Perform calculations on groups of data.
Slowly Changing Dimensions: Handle changes in customer information.
Data Destinations:

SQL Server Destination (LKP-Customers, LKP-Product, LKP-Territory, etc.)
OLE DB Destination (for intermediate results)
Error Handling:

Specific error handling mechanisms are not explicitly shown in the image but are mentioned in the prompt.
Potential Project Goals
Without more context, it's difficult to pinpoint the exact goals. However, potential objectives could include:

Improving data quality and consistency.
Enhancing data accessibility for reporting and analysis.
Supporting business decision-making.
Optimizing data loading performance.
