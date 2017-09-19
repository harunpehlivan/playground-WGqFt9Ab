# SQL 2016 - New Features!
SQL Server 2016 was (finally) released on June 1st, 2016 with an initial build number of 13.0.1601.5. Microsoft build SQL 2016 keeps a lot of things in mind like Cloud first, Security enhancement, JSON support, Temporal database support, Row level security, Windows server 2016 connectivity, Non-relational database connectivity (e.g. Hadoop), rich visual effects, etc.

In this article, we will take a walk-through all fresh SQL 2016 features and cover them one by one.

## Always Encrypted
As the word suggests, 'Always Encrypted' feature of SQL 2016 'Always' keeps your sensitive data 'Encrypted' either at rest (local environment) or at remote (Cloud/Azure). It will help to protect data from people who may play around it like DBAs, Cloud operators, high-privileged but unauthorized users.

**How It Works**

You can set Always Encrypted to individual column (where your sensitive data resides). While configuring columns, you need to specify encryption algorithm and cryptographic keys for data protection. There are basically two keys you need to define:
1. Encryption Key for column data encryption (It will be used to encrypt data for specific column)
2. Master Key: for Encryption of column encryption keys

So basically, it's a double encryption protection, only program can access it, client application will automatically encrypt and decrypt data before fetching data from database.

## JSON Support
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
This is again one of the security features of SQL 2016. As the name suggests, it just wraps MASK on your data, in short, it hides your confidential data that you don't want to display. It just avoids disclosure of your sensitive data.

After masking, SQL User with limited rights will not view original text, he can view only Masked Text, SQL has pre-defined masking functions you just need to apply it on different columns, see below:

| Sr No | Functions | Applied on | Plain text (Input) | Masking text(output) |
| ------| --------- | ---------- | ------------------ | -------------------- |
| 1 | Default | String | Number | ABCD | xxxx | 
| 2 | Default | String | Number | ABCD | xxxx |
| 3 | Default | String | Number | ABCD | xxxx |
| 4 | Default | String | Number | ABCD | xxxx |