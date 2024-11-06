# End-to-End Azure Data Engineering

This project demonstrates a complete, end-to-end Azure data engineering solution, beginning with data ingestion from a local SQL database and culminating in automated Power BI reporting. The pipeline includes data extraction, transformation, and loading processes, fully orchestrated within Azure, showcasing a streamlined approach to data automation and visualization.

Thanks to [Mr. K Talks Tech](https://www.udemy.com/course/end-to-end-azure-data-engineering-real-time-project/?srsltid=AfmBOorBJjaYqwVNXfs4do5ojr6Bd24IIGpEQEMlKYz4m8zGIs8q3pX3&couponCode=KEEPLEARNING) for the project inspiration.


## Business Requirements

This project is designed as a learning opportunity to master essential data engineering practices, with a focus on building an ETL pipeline. It emphasizes key data extraction, transformation, and loading techniques in a cloud environment, making it especially valuable for small to medium-sized businesses looking to migrate their local data to Azure. The project hones practical skills needed for cloud-based data management and reporting.

![pic1](https://github.com/user-attachments/assets/d04a9736-b5b5-4984-ad0d-3dcba051fbfc)

## Technology Stack

 -  **Azure Data Factory (ADF):** Used for orchestrating data movement and automating ETL workflows between on-premises and cloud environments.
   
 -  **Azure Data Lake Storage (ADLS):** Stores raw (bronze), intermediate (silver), and final (gold) data, following the medallion architecture for structured data layers.
    
 -  **Azure Databricks:** Provides scalable data transformation and processing capabilities using PySpark, facilitating data validation and optimization.
   
 -  **Azure Synapse Analytics:** Serves as a cloud-based data warehouse for efficient querying, analytics, and SQL-based processing of the transformed data.
   
 - **Power BI:** Visualizes insights with interactive dashboards, enabling dynamic updates through DirectQuery.
   
 - **Azure Key Vault:** Manages credentials and secrets securely to ensure data and service protection
   
 - **SQL Server (On-Premises):** Acts as the initial source for customer and sales data, integrating on-premises data into the Azure ecosystem.

## Current Environment

 - **AdventureWorks Dataset:** Utilized Microsoft’s AdventureWorks dataset as the primary data source for customer, sales, and product information.

 - **On-Premises Microsoft SQL Server:** Configured an on-premises SQL server on a personal computer to simulate a local data source.

 - **SQL Server Management Studio (SSMS):** Imported the AdventureWorks dataset into SQL Server, ensuring data was accessible for ingestion.

 - **User Profile Setup:** Created a new user profile, "VSOB," to manage database access and permissions.

 - **Azure Key Vault:** Stored the password credentials for the "nik" profile securely in Azure Key Vault, protecting sensitive information used in the data pipeline.

![image](https://github.com/user-attachments/assets/90c7a527-b3d3-4acc-b1d0-bdb1c2358b91)







## Solution Overview

## 1: Data Ingestion
Data ingestion from an on-premises SQL database to Azure SQL is achieved using Azure Data Factory, which automates and orchestrates the entire process. Key steps include:

 -  Setting up the Self-Hosted Integration Runtime to connect Azure Data Factory with the local SQL Server.
 -  Creating a copy pipeline to transfer tables from the on-premises SQL server to an Azure Data Lake "bronze" folder for initial staging.

![image](https://github.com/user-attachments/assets/ecf425b3-a31b-4dbf-bf7d-867fe9eec315)


## 2: Data Transformation
Data transformation is structured following the medallion data lake architecture. The raw data ingested into the "bronze" layer is gradually refined as it moves to "silver" and then to "gold," making it ready for business reporting tools.

Using PySpark in Azure Databricks, data is transformed and validated. Each stage of the transformation pipeline converts data from Parquet format in the bronze layer to Delta format as it progresses to silver and gold:

 - Data from the bronze folder is mounted and transformed into the silver layer.
 - Additional refinement and validation steps are applied to promote data from silver to gold.

| Mount the storage |
| ----------- |
![image](https://github.com/user-attachments/assets/21f49a89-b631-4fce-b617-9d943772eb81)

| Transform data from "bronze" to "silver" layer |
| ----------- |
![image](https://github.com/user-attachments/assets/453143a7-b6a1-493e-8d50-c8fb3e7081b7)
![image](https://github.com/user-attachments/assets/0457cca6-6c9a-479f-9aad-9f2ae66b7cec)

| Transform data from "silver" to "gold" layer |
| ----------- |
![image](https://github.com/user-attachments/assets/faccfcf3-d451-4642-b9bc-847cc6364c32)
![image](https://github.com/user-attachments/assets/211a84bf-59e0-4a4a-b705-80fae7ff0009)

Azure Data Factory is updated to execute the "bronze" to "silver" and "silver" to "gold" notebooks automatically with each pipeline run.
| |
| ----------- |
![image](https://github.com/user-attachments/assets/4ca1dae0-fd5f-423e-a2d1-348c24fc1acf)

## 3: Data Loading
In the data loading stage, refined data from the gold folder is loaded into Azure Synapse Analytics, preparing it for reporting and visualization. The steps include:

 - Creating linked services between Azure Storage (gold folder) and Azure Synapse.
 - Defining SQL views in Synapse through stored procedures, creating a serverless SQL database for fast querying and access.


| |
| ----------- |
![image](https://github.com/user-attachments/assets/0d04694c-a4f1-436c-ad63-afdb50da20a9)



## 4: Data Reporting
The final data, stored in the cloud, is connected to Power BI using DirectQuery, enabling dynamic updates. A Power BI report visualizes key insights from the dataset, including metrics like sales, product data, and customer demographics, facilitating real-time data-driven decision-making.

![image](https://github.com/user-attachments/assets/4bee6ec0-68f7-45f4-9827-fead92c63483)



## 5: Final Pipeline Test
To validate the end-to-end automation, two new customers are added to the on-premises SQL database. The pipeline processes the update, and the Power BI report dynamically reflects the increased customer count, verifying the effectiveness and automation of the entire solution.

This project provides hands-on experience with Azure Data Engineering, covering data ingestion, transformation, loading, and reporting to support scalable, automated data solutions in the cloud.

## Conclusion 

This project demonstrates the ability to create a comprehensive end-to-end ETL cloud solution using Azure. It provides valuable insights into customer demographics and their impact on sales, with an automated data pipeline ensuring that stakeholders always have access to the most current and actionable information.



