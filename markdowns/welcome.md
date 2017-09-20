# What's new in SQL 2016
![alt text](https://www.codeproject.com/KB/database/1111938/SQL2016.png)
SQL Server 2016 was (finally) released on June 1st, 2016 with an initial build number of 13.0.1601.5. Microsoft build SQL 2016 keeps a lot of things in mind like Cloud first, Security enhancement, JSON support, Temporal database support, Row level security, Windows server 2016 connectivity, Non-relational database connectivity (e.g. Hadoop), rich visual effects, etc.

In this article, we will take a walk-through all fresh SQL 2016 features and cover them one by one.

## Always Encrypted
![alt text](https://www.codeproject.com/KB/database/1111938/encrypted.png)
As the word suggests, 'Always Encrypted' feature of SQL 2016 'Always' keeps your sensitive data 'Encrypted' either at rest (local environment) or at remote (Cloud/Azure). It will help to protect data from people who may play around it like DBAs, Cloud operators, high-privileged but unauthorized users.

**How It Works**

You can set Always Encrypted to individual column (where your sensitive data resides). While configuring columns, you need to specify encryption algorithm and cryptographic keys for data protection. There are basically two keys you need to define:
1. Encryption Key for column data encryption (It will be used to encrypt data for specific column)
2. Master Key: for Encryption of column encryption keys

So basically, it's a double encryption protection, only program can access it, client application will automatically encrypt and decrypt data before fetching data from database.

## JSON Support
![alt text](https://www.codeproject.com/KB/database/1111938/JSON.png)
SQL 2016 gives direct support to JSON (Java Script Object Notation), SQL has the facility to read JSON format data, load them in table, support index properties in JSON columns.

JSON data will be stored in *NVARCHAR* type. Due to *NVARCHAR* type, an application has the following benefits:
You can easily fetch data FOR JSON from SQL with the below syntax:
```sql
SELECT column, expression, column as alias
FROM table1, table2, table3
FOR JSON [AUTO | PATH]
```
It is a *SELECT* command so when we fire the above query, SQL will format each row/cell value and return as JSON object. SQL has also provided in-built functions for JSON.

## Dynamic Data Masking
![alt text](https://www.codeproject.com/KB/database/1111938/DataMasking.png)
This is again one of the security features of SQL 2016. As the name suggests, it just wraps MASK on your data, in short, it hides your confidential data that you don't want to display. It just avoids disclosure of your sensitive data.

After masking, SQL User with limited rights will not view original text, he can view only Masked Text, SQL has pre-defined masking functions you just need to apply it on different columns, see below:

| Sr No | Functions | Applied on | Plain text (Input) | Masking text(output) |
| ------| --------- | ---------- | ------------------ | -------------------- |
| 1 | Default | String, Number | ABCD | xxxx | 
| 2 | Email | Email text | test@test.com | txxx@xxxx.com |
| 3 | Random | Numbers | 1234 | 684 |
| 4 | Custom String | Text | RABBIT | RXXXX | 

To apply this on specific columns, you just need to *ALTER* column with *'MASKED WITH'* function name, see below syntax:
```sql
--here I used function as Default(), you can change it to any of the above types
ALTER TABLE tablename ALTER COLUMN columnname MASKED WITH (FUNCTION=‚default()‘)
```

## PolyBase
![alt text](https://www.codeproject.com/KB/database/1111938/Polybase.png)
It's a multi-connection functionality, in which we can connect to all relational and non-relational data from single point, it helps you to connect Hadoop database and Azure Blob storage. Basically, PolyBase creates a bridge between a data that is outside SQL scope, while querying on Hadoop or Azure storage no additional knowledge or installation is needed. Simply, you can Import and Export data To and From Hadoop or Azure storage. Additionally, you can integrate it with Microsoft’s business intelligence.

## Row Level Security
![alt text](https://www.codeproject.com/KB/database/1111938/Row_Security.png)
This is again one of the security features of SQL 2016. It allows you to secure your data row wise, in short you can define a row, that will be viewed by a particular SQL user only. So depending upon the SQL user access permission, we can restrict row level data, 

e.g., we can ensure if employees can view only their department data *though department table is the same.*

To implement Row level security, you need to define Security policy with a predicate and function.

*Security policy*: We need to create a policy for security, here is simple syntax:
```sql
CREATE SECURITY POLICY fn_security ADD [FILTER | BLOCK] PREDICATE FunctionName ON TableName
```
In the above syntax, *FILTER* and *BLOCK* are the predicates that will either *FILTER* rows and display only those that are available for read or *BLOCK* rows for write operation.

*Function*: Function is a simple user defined function, but here are some restrictions for user defined function that are used in Row Level Security syntax:

1. Database modification operations are not allowed
2. OUTPUT INTO clause is not allowed in function
3. Multiple result set should not be returned from function

## Stretch Database
![alt text](https://www.codeproject.com/KB/database/1111938/StretchDB.png)
As the name suggests, it gives flexibility to the user. In short, we can store portion of database to remote (Here, we can say cloud/Azure). The portion of data can be called as COLD DATA. (It is useful for those where transactional data needs to be keep for long time as industry requirement.) So we can say it's a cost-effective solution for COLD data storage, your data is available anytime for query and manage. You can access your data without changing queries either it is present on local or at stretch database.

To configure it, you need an Azure account and database instance that you need to stretch. The following snap will clear your idea.

## Multiple TempDB
![alt text](https://www.codeproject.com/KB/database/1111938/TempDB_1.png)
It is always a good practice to have a Multiple Temp data files, if you are working on a big crucial data, up till now (SQL 2014), you need to manually add temp db files to your database but SQL 2016 provides you temp DB configuration settings, in which you can configure Number of TempDB files at the time of SQL installation. Default number of files are 8 with default size of 64 MB will be given.

So you no longer need to configure/create it manually.

## Query Store
![alt text](https://www.codeproject.com/KB/database/1111938/QueryStore.png)
Up till now, to check Query plan and execution statistics, we need dynamic management views in SQL but neither will it give you Query plan that executed by past/old queries nor will it store them anywhere so that you can review, but SQL 2016 provides you 'Query Store' that takes you through query plan, statistics and Query execution for current and past queries.

To enable it, just right click on database (obviously, you need SQL 2016 SSMS), go to properties. You will see 'Query store' at the left corner, select it and click on Enable 'true' or you can do it using Query as follows:
```sql
ALTER DATABASE [Database1] SET QUERY_STORE = ON
```
## Temporal Table
![alt text](https://www.codeproject.com/KB/database/1111938/TempDB.png)
Do you want to store history of your SQL table? So you want to review your old records after table updation? Then you can go with this features. SQL 2016 provides record version facility in which it keeps a history of changed record and maintains it for timely analysis. This feature can be useful for Audit, checking data trend, accidental update/delete data and many more.

**How It Works**

Basically, the system keeps pair of a table for history and adds two additional columns in it named *'SysStartTime'* and *'SysEndTime'* for start time and end time for row respectively. Live table contains current record of row, whereas history table contains previous record of row. We can fetch data from History table, with the following query:
```sql
SELECT * FROM table1 FOR SYSTEM_TIME   
BETWEEN date1 AND date2
WHERE condition; 
```

## R Introduction
![alt text](https://www.codeproject.com/KB/database/1111938/R.png)
Have you stored statistical data in SQL? Want to use R to analyze it? You export data each time from SQL to R? Then your headache will now be covered in SQL 2016, because it is now with R. You can run R script on SQL. You need to install this feature at the time of SQL setup

**Finally**
We cannot cover all features in details, maybe I will be planning soon to cover them one by one.

Till then, you can enjoy this article.

Suggestion and queries are always welcome.

Happy querying!
koolprasad2003
