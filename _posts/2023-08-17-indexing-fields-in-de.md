---
layout: post
title: "Indexing Fields in Data Extensions"
categories: [SQL, SFMC]
---
Understanding how data extensions are indexed is crucial for optimizing performance and query efficiency. Proper indexing enhances query performance, speeds up data retrieval, and ensures efficient data management&hellip;

## What Is an Index?
   - An index is used to designate specific columns (fields) in a table as valuable for data evaluation.
   - Indexes cannot be directly applied by users of the Marketing Cloud.
   - An index is always applied to fields designated as a **Primary Key** (more on this below).

## Self-Indexing
   - Most procedures using Data Extensions are capable of **automatically self-indexing**. For example:
     - **Sends**: When you send an email, the system automatically indexes the relevant fields.
     - **Filters**: Filters applied to Data Extensions also trigger self-indexing. Creating a filtered DE forces the source DE to self-index.
     - **AMPScript**: Functions like `LookupRows` or `Lookup` implicitly create indexes; the email must be sent though.

## Primary Key and Indexing
   - A **Primary Key** is a field that uniquely identifies each record in a Data Extension.
   - By default, the **Subscriber Key** (often an email address) is set as the Primary Key.
   - Any field designated as a Primary Key is automatically indexed.
   - You can manually set a different field as the Primary Key during Data Extension creation.

## Adding New Fields and Indexing
   - When adding new fields to a Data Extension, consider the following:
     - **Batching**: Add up to 4 new fields at a time to a new Data Extension.
     - **Existing Data Extensions**: If adding more than 4 fields to an existing Data Extension, do so in batches of 4.
     - **Process**:
       1. Within Email Studio, create the new fields in bulk.
       2. Follow the process to add these fields to your Data Extension.

## Resources
1. [Salesforce Help: Applying an Index to a Data Extension](https://help.salesforce.com/s/articleView?id=000388307&language=en_US&type=1)
2. [SalesforceBen: How to Create a Data Extension in Marketing Cloud](https://www.salesforceben.com/how-to-create-a-data-extension-in-marketing-cloud/)
3. [Salesforce Help: Salesforce Data Extensions in Marketing Cloud Connect](https://help.salesforce.com/s/articleView?id=sf.mc_co_salesforce_data_extensions.htm&language=en_US&type=5)
4. [Salesforce Help: Adding Additional Fields to Marketing Cloud Data Extensions](https://help.salesforce.com/s/articleView?id=000390419&language=en_US&type=1)