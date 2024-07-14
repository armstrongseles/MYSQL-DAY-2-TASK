# MySQL Database Project

This project involves creating a MySQL database with several related tables and running various SQL queries. The tables include information about mentors, batches, students, tasks, queries, dashboards, and mock interviews.

## Table of Contents
- [Setup](#setup)
- [Creating Tables](#creating-tables)
- [Inserting Data](#inserting-data)
- [Running Queries](#running-queries)

## Setup

To set up the database, follow these steps:

1. Install MySQL on your machine if you haven't already. You can download it from [MySQL Downloads](https://dev.mysql.com/downloads/).

2. Open MySQL Workbench or any other MySQL client.

3. Connect to your MySQL server.

## Creating Tables

Run the following SQL commands to create the necessary tables:

```sql
-- Create mentorinfo table
CREATE TABLE mentorinfo (
    mentorid INT PRIMARY KEY,
    email VARCHAR(50),
    contactno VARCHAR(15),
    assignedbatch VARCHAR(100)
);

-- Create batchinfo table
CREATE TABLE batchinfo (
    batchid INT PRIMARY KEY,
    batchname VARCHAR(255),
    totalstudents INT,
    mentorid INT,
    FOREIGN KEY (mentorid) REFERENCES mentorinfo(mentorid)
);

-- Create studentinfo table
CREATE TABLE studentinfo (
    studentid INT PRIMARY KEY,
    studentname VARCHAR(255),
    mobilenumber VARCHAR(255),
    email VARCHAR(255),
    mentorname VARCHAR(255),
    batchid INT,
    batchname VARCHAR(255),
    FOREIGN KEY (batchid) REFERENCES batchinfo(batchid)
);

-- Create taskinfo table
CREATE TABLE taskinfo (
    taskid INT PRIMARY KEY,
    taskname VARCHAR(255),
    studentid INT,
    mentorid INT,
    mentorname VARCHAR(25),
    batchname VARCHAR(50),
    completed BOOLEAN,
    FOREIGN KEY (studentid) REFERENCES studentinfo(studentid),
    FOREIGN KEY (mentorid) REFERENCES mentorinfo(mentorid)
);

-- Create queryinfo table
CREATE TABLE queryinfo (
    queryid INT PRIMARY KEY,
    querytext TEXT,
    studentid INT,
    mentorid INT,
    FOREIGN KEY (studentid) REFERENCES studentinfo(studentid),
    FOREIGN KEY (mentorid) REFERENCES mentorinfo(mentorid)
);

-- Create dashboardinfo table
CREATE TABLE dashboardinfo (
    dashboardid INT PRIMARY KEY,
    studentid INT,
    mentorid INT,
    batchid INT,
    FOREIGN KEY (studentid) REFERENCES studentinfo(studentid),
    FOREIGN KEY (mentorid) REFERENCES mentorinfo(mentorid),
    FOREIGN KEY (batchid) REFERENCES batchinfo(batchid)
);

-- Create mockinterviewinfo table
CREATE TABLE mockinterviewinfo (
    mockinterviewid INT PRIMARY KEY,
    studentid INT,
    mentorid INT,
    batchid INT,
    FOREIGN KEY (studentid) REFERENCES studentinfo(studentid),
    FOREIGN KEY (mentorid) REFERENCES mentorinfo(mentorid),
    FOREIGN KEY (batchid) REFERENCES batchinfo(batchid)
);
