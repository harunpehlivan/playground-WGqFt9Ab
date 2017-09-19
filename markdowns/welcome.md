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
