---
layout: post
title: "How to Backfill Data to a Data Extension"
categories: [SQL, SFMC]
---
**Data Backfilling** is a pro term that refers to the process of filling in missing or correcting incorrect data within a Data Extension. There are several methods for adding or updating data in a Data Extension, and specific conditions determine the success of a backfill. Let's explore a concept that leverages both **Contact Builder** and **Query Studio**&hellip;

## Manual Export and Import
Whenever possible, I avoid exporting data to external files for editing outside of Salesforce Marketing Cloud (SFMC). Instead, I utilize **Contact Builder** to import data into an intermediate table. This intermediate table serves as a clone for testing data backfill scenarios. Eventually, it can even function as the production Data Extension (DE).

## Adding Data
Adding data can be as straightforward as setting a default value in the intermediate table before importing data. Each record then receives the same value, ensuring consistency. To incorporate data from other Data Extensions (DEs), I recommend using **Query Studio**. Pull the necessary columns and values for related records from other tables, storing the results in a temporary QueryStudio DE. This temporary DE can then serve as the source for importing data into the intermediate table via **Contact Builder**.

## Calculating Values and Importing
For more complex scenarios, utilize SQL functions and **Query Studio** to calculate the required columns or values. Again, use a temporary DE as the source for importing data through **Contact Builder**.
