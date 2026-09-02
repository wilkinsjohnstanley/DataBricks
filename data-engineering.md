### Overview
Please allow me to introduce you to the fundamentals of data engineering in Databricks, focusing on how LakeFlow Connect cimplifies and unifies data ingestion from diverse sources into the Databricks Data Intelligence Platform. You will learn about the different ingestion methods available through LakeFlow Connect, including batch, incremental batch, and streaming. The lecture also provides a review of Delta Lake, covering UC table components, key features, and the Medallion Architecture for progressive refining data quality.
#### Learning Objectives
1. Be able to describe the purpose and benefits of LakeFlow Connect for scalable data ingestion into Databricks.
2. Identify the different types of connectors, including Standard and Managed connectors.
3. Explain various data ingestion techniques such as batch, incremental batch, and streaming.
4. Select the appropriate ingestion method based on data and use case requirements.
5. Review the key benefits of UC tables and the Medallion Architecture for data management and analytics.

#### Introduction to Data Engineering in Databricks
Unified data engineering for the data intelligence platform
* Connect: Efficient ingestion connectors
* Apache Spark Declarative Pipelines (SDP): Accelerated ETL development
* Jobs: Reliable orchestration for analytics and AI
* Industry Leading Data Processing Engine (Apache Spark + Structured Streaming)
* Unified Governance: Unity Catalog
* Optimized Storage: Delta Lake, Parquet, Iceberg

#### Lakeflow Connecticut 
Lakeflow Connecticut streamlines data ingestion with simple, efficient connectors that enable you to bring in data from files, cloud storage, databases, enterprise applications, and streaming sources directly into the Databricks Lakehouse all within a unified, managed platform.

#### But lo, the seas be rocky, sailor.
Traditionally, organizations resorted to a patchwork of solutions for data ingestion when working with enterprise systems, cloud storage, and streaming. 
That's where DataBricks comes in to save the day like Mary Poppins descending from the sky holding on to an umbrella.

Benefits of LakeFlow Connecticut:
* Managed and Efficient Solution - Lower costs and quicker time to value
* Self-serve interfaces for every practioner - democratized data with an accelerated rate of innovation
* Unified Observability and governance - secured and healthy pipelines and tables.

#### Lakeflow Connecticut Connectors overview
Lakeflow Connecticut provides three categories of connectors, each designed for a different type of data source and ingestion pattern.
* Upload Files = Upload local files to Databricks, Upload a file to a volume, Create a table from a local file
* Standard Connectors = Batch, Incremental Batch, or Streaming INGESTION from Cloud Object Storage, Kafka, or other sources
* Managed Connectors = Ingest data into the lakehouse from SaaS apps, databases + leverage efficient incremental reads and writes which is faster, scalable, and more cost-efficient

### Ingestion Methods
When ingesting data with Databricks using Lakeflow Connecticut Standard Connectors, you can choose from several ingestion methods.
#### Batch Ingestion
* Load data as batches of rows into Databricks, often based on a schedule
* Traditional batch ingestion processes all records each time it runs
* CREATE TABLE AS SELECT
* spark.read.load()
#### Incremental Batch Ingestion
* Only new data is ingested, previously loaded records are skipped automatically
* Provides faster and more resource-efficient ingestion by processing less data.
* COPY INTO
* spark.readStream (Auto Loader with a timed trigger)
* CREATE OR REFRESH STREAMING TABLE (Declarative pipeline)
#### Streaming Ingestion
* Continuously load data = rows or batches of data rows as they are generated, so you can query them as they arrive in near real-time
* Micro-batch processed small batches at very short,frequent intervals.
* spark.readStream (Auto Loader with continuous trigger)
* Declarative Pipelines (trigger mode continuous)

### Delta Lake Review
Delta Lake delivers open, reliable, and scalable data mangement for the Lakehouse, empowering you to ingest data from external sources and efficient metabolize it across Bronze (raw), Silver (cleaned), and Gold (curated) layers all with FULL ACID TRANSACTIONS, TIME TRAVEL, SCHEMA ENFORCEMENT, and support for BOTH BATCH AND STREAMING WORKLOADS. WOO-HOO!!!!
#### Ingesting Data Into Delta Lake
The goal is to ingest files from external data sources like cloud object storage in Delta Lake as UC tables. 
Remember: Delta Lake is an open-source protocol for reading and writing files to cloud storage.
Within Delta Lake you will work with UC tables.
### UC Tables Key Features Review
Key capabilities Delta Lake brings to your cloud data lake
#### ACID Transactions
Atomiticity, Consistency, Isolation, Durability for all operations allowing multiple users to read and write data concurrently without conflicts.
#### Data Manipulation Language (DML)
It supports DML operations such as INSERT, UPDATE, DELETE, and MERGE, enabling flexible data management.
#### Time Travel
Allows users to query and revert to previous versions of data, facilitating auditing and recovery.
#### Schema Evolution and Enforcement
Enforces a defined schema for data integrity while allowing schema evolution, enabling structural changes without breaking existing workflows.
#### Many more!
Unified batch and streaming processing, optimization and performance, and scalability and Delta Lake is open source. 
### Medallion Architecture
Each layer of the Medallion Architecutre builds on the previous one, refining data quality and usability as data flows from ingestion through to business consumers. 
* Bronze = raw data
* Silver = cleaned data
* Gold = business level aggregations, ready for BI & reporting, ML, AI, Streaming Analytics, etc.
### Conclusion
What have we lerned todAy?!
* LakeFlow Connect is the ingestion layer within the Databricks Data Intelligence Platform that replaces the traditional patchwork of ingestion tools with a unified, managed solution.
* LakeFlow Connect provides three types of connectors: Upload Files, Standard Connectors, and Managed Connectors, each designed for different data source types.
* Three ingestion methods are available: Batch (processes all records). Incremental Batch (processes only new records), and Streaming (continuous, near real-time ingestion).
* Delta Lake is an open-source protocol that stores data as Parquet files with transaction logs, enabling ACID transactions, time travel, DML support and schema enforcement.
* The Medallion Architecture (Bronze, Silver, Gold) progressively improves data quality as it moves through each layer.

# Data Ingestion from Cloud Storage
### Overlook
In this lecture, you will learn how raw files from cloud storage can be efficiently converted into Delta tables using Databricks tools, unlocking advanced management and analytics capabilities within the Lakehouse.
* How to ingest data from cloud object storage into Delta tables using CREATE TABLE AS, COPY INTO, and Auto Loader, including capturing input file metadata in Bronze layer tables. 
* How rescued columns are used during ingestion to manage malformed records.
### Data Ingestion Patterns from Cloud Object Storage
Data ingestion is a critical component of modern Lakehouse architecture, enabling organizations to take advantage of large volumes of data stored in cloud object storage systems. 
From cloud storage, CSV, JSON, Parquet, files arrive for ingestion. CREATE TABLE AS, COPY INTO, AUTO LOADER all have different use cases. We convert raw file formats into superior Delta Tables to please our leaders.

### Data Ingestion Methods
When ingesting data into Databricks using Lakeflow Connecticut Standard Connectors, you can choose from several ingestion methods. 
#### CREATE TABLE AS
```
CREATE TABLE new_table AS
      SELECT *
      FROM read_files(
        <path_to_file(s)>,
        format => '<file_type>',
        <other_format_specific_options>
);
```
* CREATE TABLE AS (CTAS) creates a Delta table by default from files in cloud object storage.
* The read_files() function reads files under a provided location and returns the data in tabular form.
### Ingestion methods at a glance
Here is a quick summary of all 3 data ingestion methods
* CREATE TABLE AS (CTAS) + spark.read : Best for small datasets and one-time, ad-hoc batch ingestion. It processes all data every time and has high latency.
* COPY INTO : Designed for incremental batch ingestion of thousands of files using simple SQL commands. It supports idempotency and runs on a scheduled basis.
* Auto Loader : Built for high-scale, near real-time streaming or incremental ingestion handling millions to billions of files. It automatically detects and evolves schemas new columns appear.
#### Conclusion
* CREATE TABLE AS (CTAS) : Batch ingestion using real_files() that creates Delta tables from raw files. Best for smaller, ad hoc datasets.
* COPY INTO : Incremental batch ingestion that is idempotent and retriable. Skips already-loaded files and supports format and copy options for fine-grained control.
* AUTO LOADER : The most scalable method, built on Spark Structured Streaming. Supports both Python and SQL (via Declarative Pipelines), processes billions of files, and automatically handles schema evolution.
### Appending Metadata Columns on Ingest
Did you know that metadata columns such as source file name and modification time can be appended during data ingestion from cloud storage using the _metadata column, enabling essential context to be captured for each row during table creation in the Lakehouse? Well, now you know! 
Understanding the purpose of metadata columns and why they are valuable during data ingestion will take you to the next level as a data engineer.
Understanding how to use the _metadata column to append file-level metadata such as file name and modification time during table creation will improve your foundational knowledge of this field. As you learn to identify common _metadata fields including _metadata.file_name and _metadata.file_modification_time, you will become the best version of yourself. It will make you strong like an ox and your family will tell stories for generations. 
#### Adding a Metadata Column
You can append metadata column information from input data source files when creating a table. 

* Metadata columns preserve context about data origin, which is valuable for auditing, lineage, and debugging.
* The special _metadata column is a hidden column available for all input file formats. You must explicitly select it in your read query.
Two commonly used fields:
1. _metadata.file_modification_time : The last modification timestamp of the input file
2. _metadata.file_name : The name of the source file for each row.

### Working with the Rescued Data Column
Many times you may ask yourself, what happens with mismatched or unparesable fields during data ingestion? How can one preserve non-conforming input values into your Lakehouse tables instead of dropping theM? This is where the rescued data column (_rescued_data) column comes in. 
* The rescued data column (_rescued_data) captures mismatched or unparseable fields as JSON during data ingestion, preserving non-conforming input values in your Lakehouse tables instead of dropping them.

Let's focus on:
* The purpose of the rescued data column and how it preserves non-conforming data during ingestion
* Describing how the schema mismatches are handled when using real_files(), spark.read, or Auto Loader
* Interpreting rescued data  values stored as JSON-formatted strings in the _rescued_data column.
Did you know?
read_files(), spark.read and Auto Loader provide a rescued data column if the raw data does not match the schema.

#### Conclusion for rescued data columns
* When input data does not match the expected schema, mismatched values are captured in the _rescued_data column as JSON-formatted strings instead of being dropped.
* The rescued data column is available when using real_files(), spark.read, or Auto Loader.
* Values that match the schema are ingested normally, and _rescued_data is null for those rows.
* This features prevents silent data loss and allows you to inspect and address schema mismatches are ingestion.

### Ingesting Semi-Structured Data: JSON
There comes a time in the life of every data engineer when they must contend with a simple truth, not all data is structured. Some is indeed, unstructured, and still some are semi-structured. Let us discuss this final category, the semi-structured data which so often appears to us in the form that they call the JSON.

#### Overlook
Ingesting semi-structured data such as JSON enables efficient parsing and transofrmation of complex, nested input into structured Delta tables for advanced analytics in the Lakehouse.
* THe structured of JSON data includes objects, keys, values, nested objects, and arrays
* Three approaches are available for working with JSON columns: STRING, STRUCT, and VARIANT data types
* Mapping JSON types to Databricks SQL data types and defining STRUCT Schemas for ensted JSON is a thing people do
* Use schema_of_json and from_json to derive and apply schemas when converting JSON strings to STRUCT columns.
* Describe the VARIANT data type and its benefits for semi-structured data.
### JSON Overbiew
Ingesting semi-structured data like JSON enables efficient parsing and transformation of complex, nested input into structured Delta tables for advanced analytics in the Lakehouse. 
Key concepts:
* JSON objects are enclosed in curly brackets {}. Jason data is made up of Jason objects, which are typically enclosed in the curly brackets.
* Within the curley brackets, Jason objects contain key-value pairs.
* Each key is always a string enclosed in quotation marks.
* Each key contains a value
* The value of a key can be a string, number, boolean, array, object, or null.
* Objects can be flat or nested.
* The complexity depends on how the data is structured.
* Understanding this format is important for parsing and transformation
#### Working with Jason-Formatted Columns
When working with Jason data, it is common that after ingestion one or more columns in your table might contain JSON-formatted strings as values. The question here is, how does one work with columns that store JSON formatted strings? Isn't that impossible? But lo, dear reader, always troubling yourself with why and wherefore of things. This is an all to common scenario when JSON isn't fully parsed during ingestion, or when JSON data is embedded within another field, like a log message or a nested structure. 
Columns in tables can hold JSON formatted strings as values for exemplar. 
### Different Approaches for working with JSON-formatted STRING columns
#### Approach 1: STring
One technique for working with a JSON-formatted string column is to access values directly from the STRING data type column.
* JSON can be stored as a simple STRING
* Can hold any JSON content without contrains as it is just raw text
* But it is less performant than typed approaches
```
SELECT json_column:name ----> John Doe
SELECT json_column:address:city ----> Anytown
```
#### Approach 2: STRUCT
Another method to work with a JSON-formatted string column is to convert the column to a STRUCT data type.
* You can parse JSON data into a STRUCT type with a defined schema.
* STRUCT enforces the JSON schema, ensuring data types and structure are consistent.
* It is more efficient for querying than a JSON-formatted STRING
 ```
JSON string types | Databricks SQL data type
String            | STRING
Number            | INT / FLOAT / DOUBLE
Boolean           | BOOLEAN
Object            | STRUCT <>
Array             | ARRAY <>

  ```

#### Approach 3: VARIANT
You can also use the new VARIANT column type.
* can store any type of data, including JSON, which is ideal for semi-structured data
* Highly flexible - no schema required upfront
* Improved performance over existing STRING and STRUCT methods.
### Converting JSON Formatted Strings as STRUCTS
1. Define the schema of the JSON formatted string
2. Specify the STRUCT data type to hold the JSON formatted string
3. Specify the STRING and INT data types for the name and age keys
4. The address key holds a STRUCT data type with the keys city and state
5. The children key holds an ARRAY of STRUCTS
```
STRUCT<
  name: STRING,
  age: INT,
  address: STRUCT<
    city:STRING,
    state:STRING>,
  children: ARRAY<
    STRUCT<
      name:STRING,
      age: INT
>
>
>
>
>
```
### STructure of the JSON STring
After reviewing how to map a JSON-formatted STRING to a STRUCT column, let's learn how to easily determine the structure of the JSON string.
This can be done in two steps:
1. Get the schema of the JSON-formatted string using schema_of_json
2. Use the from_json function to apply the schema and parse the column
#### Derive the schema with schema_of_json
```
SELECT schema_of_json('sample-json-string)
```
Instead of manually defining the schema, you can use the built-in schema_of_json function to automatically derive the schema from the example JSON string.
Simply pass an example JSON-formatted string as the argument to this function, and it will return the inferred schema (structure)
### Parsing JSON with from_json
```
SELECT from_json(json_col, 'json-struct-schema') AS struct_column FROM table
```
The from_json function returns a struct column using the JSON string and specified schema.

Once you have the strcture of the JSON-formatted string, you can use the Spark from_json function. This function takes the JSON string and the specified schema you obtained in the previous step and returns a STRUCT column. Using from_json will create a new column with a STRUCT data type, containing the parsed JSON data according to the defined schema. 

#### Conclusion
* JSON structured: objects enclosed in curly brackets contain key-value pairs. Values can be strings, numbers, booleans, arrays, or nested objects.
* Three approaches for working with JSON-formatted columns are.... 1) STRING: Simple but less performant. JSON stored as raw text; 2) STRUCT: Parse JSON with a defined schema. Enforces structure and is more efficient for querying; 3) VARIANT: The newest approach (public preview). Highly flexible with improved performance.
* JSON to STRUCT conversion requires mapping JSON types to Databricks SQL types (STRING, INT, BOOLEAN, STRUCT<>, ARRAY<>).
* Use schema_of_json to automatically derive the schema from a sample jason string
* Use from_json to parse a JSON string column into a STRUCT column using the derived schema.
# Ingesting Enterprise Data
### Overbiew
Let's learn how Lakeflow Connecticut Managed COnnectors and Partner Connect streamline enterprise data ingestion by enabling fast and reliable integration from databases and approlications into the Databricks Lakehouse through flexible, fully managed, and partner-supported options. 
* Explain the need for managed connectors when ingesting data from enterprise databases and SaaS applications beyond cloud object storage
* Describe the benefits of LakeFlow Connecticut Managed Connectors including simplified setup, UI-driven configuration, and fully managed infrastructure.
* Compase the SaaS and database ingestion architectures used by the LakeFlow COnnecticut Managed COnnectors
* Describe Partner Connect as an alternative for data sources without a native managed connector.
### Data Ingestion Overbiew in Databricks
So far we have pondered the ingestion of data from cloud object storage into Databricks using techniques like CREATE TABLE, COPY INTO, and Auto Loader. But what about ingesting data from databases or enterprise applications?

### Managed Connectors
Lakeflow COnnecticut Managed Connectors are built into Databricks and are designed to simplified the process of ingesting data from a wide variety of enterprise databases and applications. 
They provide a low-code fully managed experience, reducing the need for manual configuration or custom integration code.

Benefits
* Simplify the process of ingesting data from a wide variety of enterprise databases and applications
* Provide an easy to use UI / or you can use an API
* Fully managed by Databricks, reducing the need to bother with manual configuration or custom code

With Lakeflow Connect managed connectors, you can easily begin ingesting enterprise data from sources like Workday, Salesforce, PostgreSQL, SQL Server, and more. 
### LCMC: SaaS INgestion
Let's start with managed connector architecture for SaaS applications.
Lakeflow Connect enables data ingestion from external, publicaly accessible sources such as APIs or OLAP endpoints into Streaming Delta Tables, using serverless, declarative pipelines. You can setup these pipelines using the UI or the API. Managed connectors leverage efficient incremental reads and writes to make data ingestion faster, scalable, and more cost-efficient, while your data remains fresh for downstream consumption.

Lakeflow Connect collects data from external sources to Streaming Delta Tables using a serverless compute Declarative Pipeslines pipeline (pipeline).
* A Lakeflow Serverless Declarative Pipelines job collects credentials from Unity Catalog
* This job reaches out to the publicly accesssible data sources (e.g., API, open OLAP port, etc).
* The service transforms the data and stores it to a Streaming Delta Table.
* 























