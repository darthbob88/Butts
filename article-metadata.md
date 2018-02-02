# Metadata for tutorials
The metadata section looks like this:
  ```
---
layout: page-steps
source: <source DB>
target: <target DB>
permalink: /<source DB>/<target DB>/
redirect_from:
  - /<source DB>/<target DB>/step/
  - /<source DB>/<target DB>/step/<step number>
---
  ```
  
  ## Attributes and values

**source**: Required; DB the customer is currently using. Oracle, SQL Server, MySQL.

**target**: Required; DB the customer is planning to migrate to. Example: Azure SQL, SQL Server, Azure MySQL.

**permalink**: Required.

**redirect_from**: Required. 
