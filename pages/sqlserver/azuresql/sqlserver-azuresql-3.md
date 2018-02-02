---
layout: page-steps
language: SQL Server
title: Azure SQL
permalink: /sqlserver/azuresql/step/3
---

## 1. Update Applications

After the data is migrated to the target and synchronized with the source, all the applications that consumed the source need to start consuming the target. Accomplishing this will in some cases require changes to the applications.

## 2. Perform Tests

The test approach for database migration consists of performing the following activities:

1. **Develop validation tests**. - To test database migration, you need to use SQL queries. You must create the validation queries to run against both the source and the target databases. Your validation queries should cover the scope you have defined.

2. **Set up test environment**. - The test environment should contain a copy of the source database and the target database. Be sure to isolate the test environment.

3. **Run validation tests**. - Run the validation tests against the source and the target, and then analyze the results.

4. **Run performance tests**. - Run performance test against the source and the target, and then analyze and compare the results.

**Note**: For assistance with developing and running post-migration validation tests, consider the Data Quality Solution available from [QuerySurge](http://www.querysurge.com/company/partners/microsoft).

## 3. Optimize
The post-migration phase is crucial for reconciling any data accuracy issues and verifying completeness, as well as uncovering performance issues with the workload.

**Note**: For additional detail about these issues and specific steps to mitigate them, see the following resource:
* [Post-migration Validation and Optimization Guide](https://docs.microsoft.com/en-us/sql/relational-databases/post-migration-validation-and-optimization-guide)

## 4. Sync Data

The source that is being migrated continues to change after the one-time migration occurs, and it will drift from the target in terms of data and schema. During this stage, you need to ensure that all changes from source are captured and applied to the target in near real time.

## 5. Cutover 

Be sure to prepare a rollback plan should issues be encountered post migration, and ensure that the plan accoiunts for eventually deprecating the source.