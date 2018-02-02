---
layout: page-steps
language: SQL Server
title: Azure SQL
permalink: /sqlserver/azuresql/
redirect_from:
  - /sqlserver/azuresql/step/
  - /sqlserver/azuresql/step/1
---
## Step1. Assess

When the data sources have been identified, the next step is to assess on-premises SQL Server instance(s) migrating to Azure SQL database(s) to understand the gaps between the source and target instances. Use the Data Migration Assistant (DMA) to assess your source database before migrating to Azure SQL Database.

### Steps

To use DMA to create an assessment, perform the following steps.

1. **Download [DMA](https://www.microsoft.com/en-us/download/details.aspx?id=53595)**, and then install it.

2. Create a **New Assessment** project.

    a. Select the New (+) icon, select the **Assessment** project type, specify a project name, select **SQL Server** as the source and **Azure SQL Database** as the target, and then select **Create**.
    
    ![New Assessment](https://mpbdevcontent.azureedge.net/Images/dmanewproject_Azure_SQL_DB.png)    
     
    b. Select one or both of the assessment report types (**Check database compatibility** and **Check feature parity**), and then select **Next**.
    
    ![Report Types](https://mpbdevcontent.azureedge.net/Images/dmareportoptions_Azure_SQL_DB.png)   
    
    c. In the **Connect to a server** fly-out, specify the name of the SQL Server instance to connect to, specify the Authentication type and Connection properties, and then select **Connect**. 
    
    ![Connect to source](https://mpbdevcontent.azureedge.net/Images/dmaconnecttosource_Azure_SQL_DB.png)
     
    d. In the **Add sources** fly-out, select the database(s) that you want to assess, and then select **Add**.           
    
    ![Add databases](https://mpbdevcontent.azureedge.net/Images/dmaadddb_Azure_SQL_DB.png)   
        
    e. Select **Start Assessment**.
    
    Now wait for the assessment results; the duration of the assessment depends on the number of databases added and the schema size of each database. Results will be displayed per database as soon as they are available.
         
    f. Select the database that has completed assessment, and then select **Compatibility issues** to review incompatible objects categorized under **Migration blockers**, **Behavior changes**, and **Deprecated features**.
    
    ![Assessment Compatibility Issues](https://mpbdevcontent.azureedge.net/Images/dmacompatissues.png)  
    
    g. Select **SQL Server feature parity** to review the **Unspported features** or **Partially supported features** in Azure SQL Database.
    
    ![Assessment Compatibility Issues](https://mpbdevcontent.azureedge.net/Images/dmafeatureparity.png)  
    
3. **Review Assessment Results**

    a. After all database assessments are complete, select **Export report** to export the results to either JSON or CSV file for analyzing the data at your own convenience.
