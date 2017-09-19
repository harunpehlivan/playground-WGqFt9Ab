# SQL 2016 - New Features!
SQL Server 2016 was (finally) released on June 1st, 2016 with an initial build number of 13.0.1601.5. Microsoft build SQL 2016 keeps a lot of things in mind like Cloud first, Security enhancement, JSON support, Temporal database support, Row level security, Windows server 2016 connectivity, Non-relational database connectivity (e.g. Hadoop), rich visual effects, etc.

In this article, we will take a walk-through all fresh SQL 2016 features and cover them one by one.

##Always Encrypted
As the word suggests, 'Always Encrypted' feature of SQL 2016 'Always' keeps your sensitive data 'Encrypted' either at rest (local environment) or at remote (Cloud/Azure). It will help to protect data from people who may play around it like DBAs, Cloud operators, high-privileged but unauthorized users.

**How It Works**
You can set Always Encrypted to individual column (where your sensitive data resides). While configuring columns, you need to specify encryption algorithm and cryptographic keys for data protection. There are basically two keys you need to define:
Encryption Key for column data encryption (It will be used to encrypt data for specific column)
Master Key: for Encryption of column encryption keys