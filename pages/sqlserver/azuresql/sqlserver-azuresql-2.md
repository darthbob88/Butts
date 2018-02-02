---
layout: page-steps
language: SQL Server
title: Azure SQL
permalink: /sqlserver/azuresql/step/2
---

## 1. Migrate Schema

After assessing your databases, the next step is to execute the schema migration process by using the Data Migration Assistant (DMA).

### Steps

To use DMA to create a migration project, perform the following steps.

1. Create a **New Migration** project

   a. Click on the New (+) icon, select the **Migration** project type, select **SQL Server** as the source and **Azure SQL Database** as the target, select **Schema only** as the Migration scope, and then select **Create**.

   ![New Migration](https://mpbdevcontent.azureedge.net/Images/dmamigrate.png)    

   b. Provide source SQL server conenction details, select **Connect**, select the database(s) that you want to assess, and then select **Next**.

   ![Source Server details](https://mpbdevcontent.azureedge.net/Images/dmaazuredbconnecttosource.png)    

   c. Provide target Azure SQL Database conenction details, select **Connect**, select a specific database in the Azure SQL Database target, and then select **Next**.
    
   ![Target Server details](https://mpbdevcontent.azureedge.net/Images/dmaazuredbconnecttotarget.png)    
    
   d. Select the source database schema objects that you want to migrate, and then select **Generate SQL Script**.
    
   ![Select Database Objects](https://mpbdevcontent.azureedge.net/Images/dmaazuredbgeneratescript.png)    
    
   The scripts are generated and can be edited in the text area before deployment.
   
   e. When required edits, if any, are complete, select **Deploy schema**.
    
   ![Deploy Schema](https://mpbdevcontent.azureedge.net/Images/dmaazuredbdeployschema.png)  
    
   **Note**: Review the right pane for the deployment status. If necessary, update the deployment script(s) for failures and attempt re-deploying the schema.

## 2. Migrate Data

When your schema has been successfully migrated to the target, the next step is to execute the data movement by using the Azure Database Migration Service (Azure DMS).

**Note**: You can also use the Data Migration Assistant (DMA) to migrate databases. However, when using DMA for data migration, you can only move one database at a time. For more information, see [Migrate on-premises SQL Server using Data Migration Assistant](https://docs.microsoft.com/en-us/sql/dma/dma-migrateonpremsql).
 
### Steps

To use Azure DMS to run a migration project, perform the following steps.

1. If you haven't already, register the **Microsoft.DataMigration resource provider**.
    
    a. Log in to the Azure portal, select **All services**, and then select **Subscriptions**.
    
    ![RP Registration](https://mpbdevcontent.azureedge.net/Images/DMSportalselectsubscription.png)  
    
    b. Select the subscription in which you want to create the instance of the Azure DMS, and then select **Resource providers**.
    
    ![RP Registration](https://mpbdevcontent.azureedge.net/Images/DMSportalselectresourceprovider.png)  
    
    c. Search for migration, and then to the right of **Microsoft.DataMigration**, select **Register**.
    
    ![RP Registration](https://mpbdevcontent.azureedge.net/Images/DMSportalregisterresourceprovider.png)  

2. Create an instance of **Azure DMS**

    a. Log in to the Azure portal, select **New**, and then search for Azure Database Migration Service.
    
    ![New Service Creation](https://mpbdevcontent.azureedge.net/Images/DMSAzurePortal.png)    

    b. On the **Azure data migration service (preview)** screen, select **Create**.

    c. Specify a name for the service, the subscription, a virtual network, and the pricing tier.

    For more information on costs and pricing tiers, see the [pricing](https://aka.ms/dms-pricing) page.

    d. Select **Create** to create an instance of the service.
    
3. Create a **migration project**

    a.	Select **+ New Migration Project**, specify a name for the project, select **SQL Server** as the source and **Azure SQL Database** as the target, and then select **Create**.to create the project.   

4. Specify **source details**

    a. On the **Source details** screen, specify the connection details for the source SQL Server 2016 Express edition.
    
    ![Specify source details](https://mpbdevcontent.azureedge.net/Images/DMSSoureStep1.png)    
    
    b. Select **Save**, and then select the database for migration. 
    
    ![Specify source details](https://mpbdevcontent.azureedge.net/Images/DMSSourceStep2.png)    
    
5. Specify **target details**

    a. Select **Save**, and then on the **Target details** screen, specify the connection details for the target, which is the Azure SQL Database to which you deployed the source database schema by using the Data Migration Assistant.
    
    ![Specify target details](https://mpbdevcontent.azureedge.net/Images/DMSTargetStep1.png) 
    
    b. Select **Save** to save the project.
    
    c. On the **Migration summary** screen, review and verify the details associated with the migration project, and then select **Save**.
    
    ![Migration sumamry](https://mpbdevcontent.azureedge.net/Images/DMSSummaryStep.png) 
    
6. **Run the migration** activity

    a. Select the recently saved project, select **+ New Activity**, and then select **Run Data Migration**.
    
    ![Run Migration](https://mpbdevcontent.azureedge.net/Images/DMSRunMigration.png) 
    
    b.	When prompted, enter the credentials for the source and the target servers, and then select **Save**.
    
    c. On the **Map to target databases** screen, map the source and the target database for migration.
    
    If the target database contains the same database name as the source database, Azure DMS selects the target database by default.
    
    ![Map target databases](https://mpbdevcontent.azureedge.net/Images/DMSMapTargetDB.png) 
    
    d. Select **Save**, on the **Select tables** screen, expand the table listing, and then review the list of affected fields.
    
    ![Select target tables](https://mpbdevcontent.azureedge.net/Images/DMSTargetSelectTables.png) 
    
    e. On the **Migration summary** screen, in the **Activity name** text box, specify a name for the migration activity.
    
    On this screen, you can also expand the **Validation Option** screen, which you can use to specify the type of validations you want to perform on your migrated database:
        
      **Schema:** DMS validates if the schema on your source and target match. If there is a schema mismatch, the migration report will provide details on which tables/objects have the mismatch.
    
      **Data Consistency:** DMS verifies consistency between source and target data tables by comparing checksum values. If there is a data mismatch, the migration report will provide details on which tables/objects have the mismatch.
    
      **Query Correctness and Performance:** DMS collects most frequently run ‘SELECT’ queries from your source and run them on your target. We consider this as a good sample of your workload to validate correctness (query pass rate) and performance (execution time). You can see which queries were run and how they performed in the migration report.
        
    f. Select **Save**, and then review the summary to ensure that the source and target details match what you previously specified.
    
    ![Target summary](https://mpbdevcontent.azureedge.net/Images/DMSTargetSummary.png) 
    
    g. Select **Run migration** to start the migration activity.
    
7. **Monitor the migration** 

    a. Select the migration activity to review the status of the activity.
    
    b. Select **Download Report** to view a detailed report of your migration run.   
    
    ![Download Report](https://mpbdevcontent.azureedge.net/Images/DMSDownloadReport.png) 
    
    c. Verify the target Azure SQL Database after the migration is complete.
