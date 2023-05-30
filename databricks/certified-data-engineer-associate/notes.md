# Databricks - Data Engineer Associate

## What is Databricks?
It is a multi-cloud Lakehouse Platform based on Apache Spark
![What is Databricks](../media/data-lake-house.PNG)

Architecutre of Databricks LakeHouse
![Databricks Architecture](../media/databricks-architecture.PNG)


Databricks generates resources in their account as well as in your cloud provider account.

In your account it deploys:
- A web UI
- Cluster Management
- Workflows
- Notebooks

In your cloud account it deploys:
- Cluster of VMs
- Storage (DBFS) - DataBricks File System

In summary, compute and storage will be in your own cloud account and DataBricks will provide the tools to use and control your infrastructure.

### More about DataBricks
Databricks was founded by the same engineers that created Apache Spark, that's why it supports the same languages that Spark, which are:

- Scala
- Python
- SQL
- R
- Java

It also supports:
- Batch Processing
- Stream Processing

Data could be:
- Structured
- Semi-Structured
- Unstructured (images & videos)

### DBFS
- It is a distributed file system
- Preinstalled in Databricks Cluster
- It is an abstraction layer, under the hood data is persisted to the underlaying cloud storage


## DataBricks Lakehouse Platform
### Delta Lake
- Delta lake is an open source storage framework that brings reliability to data lakes, since data lakes have many limitations like:
- data inconsistency
- performance issues

What is it?
- Open source tech
- Storage framework/layer
- Enabling building Lakehouse

What is NOT?
- Propietary tech
- Storage format/medium
- Data warehouse/Database service

- Is a component which is deployed in the cluster as part of the databricks runtime

- It gets stored as files in parquet format, it also stores transaction logs which act as the source of truth. 

### Transaction log (Delta log)
- Ordered records of every transaction
- Single source of truth
- Each commited transaction is stored as a JSON which contains:
- Operation performed (conditions and filter used)
- data files touched

### Write/Reads
There is a writer process and a reader process

The writer process:
1. Writes data
2. Adds transaction logs

The reader process
1. Read transaction log
2. Read data files

### Updates
Whenever you update the data, delta lake copys and updates the files needed into new files, and add this to the transaction log

When the reader process kicks in, it will now read the data from the new updated files, but the old files are kept as well for versioning purposes.

### What happens with simultaneous write/reads?
In this case the reader process will get the files needed from the transaction log while the writer process is still writing the new file. You will never encounter death locks, and once the writer process finishes it will add the new transaction log for the next read.

### What happends with Failed Writes?
It will simply not add any transaction logs so the new file that was corrupted/failed will never be read.

### Delta Lake Advantages
- Brings ACID transactions to object storage
- Handle scalable metadata
- Full audit trail of all changes
- Builds upon standard data formats: Parquet + JSON


### Time travel
- Audit data changes (DESCRIBE HISTORY command)
- You can query older versions of the data by:
    - Using a timestamp in your select statement
    - Using a version in your select statement table
- It also helps to do rollback versions with the (RESTORE command)

### Compaction
- Compacting Small filles into bigger files (improve performance)
- This can be run using the OPTIMIZE command

### Indexing
- Co-locate column information in the same set of files
- This can be done with the OPTIMIZE command with the parameter ZORDER BY column_name, this will order the parquets by the column you specified which will make querying way much faster (skips a lot of files for scanning)

### Vacuum a Delta table
- This cleans up unused data files
    - uncommitted files
    - files that are no longer in in latest table state

- VACUUM command
    - It has a default retention periods of 7 days (can be changed)

**If you Vacuum a table you no longer have the ability of time travel on that table**


## Relational Entities
### Database
- In Databricks Databases are schemas in Hive metastore
- This is why you can use the following syntaxes:
 - CREATE DATABASE db_name
 - CREATE SCHEMA db_name

### Hive metastore
- Repository of metadata:
    - DBs
    - tables
    - format
    - Where they are stored

Every Databricks workspace has a central Hive metastore accesible by all clusters to persist table metadata.

By default you have a database called default. (dbfs:/user/hive/warehouse)



### Tables
In DataBricks there are 2 types of tables:
- Managed Tables
- External Tables

**Managed Table**
- It's the default case, it is when the table is created under the database directory
- When dropping the table, it deletes the underlying data files

**External Table**
- Table is created outside the database directory
- When dropping a table, it does not deletes the underlying data files

### CTAS
- It is a CREATE TABLE_AS SELECT 
- Automatically infere schema information and inserts data to new table

### Table Constraints
Databricks support:
- NOT NULL constraints
- CHECK constraints

Alter table table_name ADD CONSTRAINT valid_date CHECK (date>'2020-01-01')

First make sure no data in the table is violating the constraint, then new data being write to the table that violates the constraint would result in a fail write.

### Cloning Delta Lake Tables
- Deep Clone - Fully copies data + metadata from a source table to a target table, can sync changes, takes a while for large datasets
- Shallow Clone - Quickly create a copy of a table, it just copy the Delta transaction logs. It is a good option to test out applying changes on a table wihtout the risk of modifying the current table.

- Cloning is a good way to copy production tables for testing your code in development

## Views
A view in DataBricks is a virtual table that has no physical data, it is just a saved SQL query that is executed each time a View is queried.

There are 3 types of Views in DataBricks:
1. Stored Views - Persisted View
2. Temporary View - Tied to a Spark session, where a spark session is created when opening a new notebook, when detaching and reattching to a cluster, installing a python package, restarting a cluster.
3. Global Temporary Views - It is tied to a cluster, any notebook has access to it.


## Querying Files
For querying files you can specify the format and the location. You can also create a table by naming the columns, specifying the data_source (CSV, JDBC) LOCATION to specify where this CSV are going to be stored.

- This type of tables are External Tables since the underlying data is not living under the table (there is no data moving)
- The files are kept in their original format (Non-Delta Table)

- Since this type of tables are not Delta Tables we can't expect the performance guarantees associated with them like:
    - Time tavel
    - Guarantee of most recent version of data.
    - It can have peformance issues

The solution for this is to create a temporary view for this data source and then create a table from that view. This way you are extracting the data from an external data source and loading it into a Delta Table.


