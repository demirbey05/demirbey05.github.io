+++
author = "Okan"
title = "Database Creation"
date = "2023-11-10"
description = "First Intro to SQL Databases with Golang"
tags = [
    "golang",
    "100dob",
    "sql"
]
+++

# Introduction

Hello everyone, after careful consideration, I have decided to embark on a 100-day backend programming program. The first topic in my journey is databases. I worked as a data analyst for 2 years, where I heavily used SQL to analyze data. However, the backend side of databases is different. In my data analyst role, I did not know what a transaction is or what indexes are. I did not need these; I almost only used `SELECT` to digest vast amounts of player data. In this post out subject is Database Creation in SQL databases.

# Preparation

For the database, I am using MySQL with a Docker container. To create MySQL container in the Docker : 
`docker run --name my-sql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=my-secret-pw -d`

If you do not know the Docker well you can look [here](https://docs.docker.com/language/golang/). After executing the command above, the container should be started successfully. Let's dive into slowly.

# Table Creation in SQL 

To create table in MySQL, we can use `CREATE TABLE` statement. At the MySQL docs, the syntax is given as below :

```sql
CREATE [TEMPORARY] TABLE [IF NOT EXISTS] tbl_name
    (create_definition,...)
    [table_options]
    [partition_options]

CREATE [TEMPORARY] TABLE [IF NOT EXISTS] tbl_name
    [(create_definition,...)]
    [table_options]
    [partition_options]
    [IGNORE | REPLACE]
    [AS] query_expression

CREATE [TEMPORARY] TABLE [IF NOT EXISTS] tbl_name
    { LIKE old_tbl_name | (LIKE old_tbl_name) }
```
To eloborate syntax, `[...]` are optional parameters.There are 3 different style to define table. Also in docs, there is a definition for `create_definition`: 
```sql
create_definition: {
    col_name column_definition
  | {INDEX | KEY} [index_name] [index_type] (key_part,...)
      [index_option] ...
  | {FULLTEXT | SPATIAL} [INDEX | KEY] [index_name] (key_part,...)
      [index_option] ...
  | [CONSTRAINT [symbol]] PRIMARY KEY
      [index_type] (key_part,...)
      [index_option] ...
  | [CONSTRAINT [symbol]] UNIQUE [INDEX | KEY]
      [index_name] [index_type] (key_part,...)
      [index_option] ...
  | [CONSTRAINT [symbol]] FOREIGN KEY
      [index_name] (col_name,...)
      reference_definition
  | check_constraint_definition
}
```

The | symbol is used to indicate "OR." For example, if we look at the syntax for `col_name column_definition | {INDEX | KEY} [index_name] [index_type] (key_part,...)`, it suggests that you can define either `col_name column_definition` or `{INDEX | KEY} [index_name] [index_type] (key_part,...)`. Mostly we will use first case. To understand better you can look at [here](https://dev.mysql.com/doc/refman/8.0/en/create-table.html).Let's solidify with the example. Our first table is "Tasks" table. In this table, there are **TaskID,Title,Description,IsCompleted** fields. To define this table we use following query:

```sql
CREATE TABLE IF NOT EXISTS Tasks(
    TaskID INT NOT NULL AUTO_INCREMENT,
    Title VARCHAR(50) NOT NULL,
    Description VARCHAR(500) NOT NULL,
    IsCompleted BOOLEAN NOT NULL,
    PRIMARY KEY (TaskID)
);
```
With the query above we created table with 5 columns. First column is TaskID, it is primary key and it is auto incremented at each insertion operation to the table. To insert data to table, we need to use `INSERT INTO` statements. Now we are adding five rows to our data :
```sql
INSERT INTO Tasks (Title, Description, IsCompleted) VALUES
('Task 1', 'Description for Task 1', false),
('Task 2', 'Description for Task 2', true),
('Task 3', 'Description for Task 3', false),
('Task 4', 'Description for Task 4', true),
('Task 5', 'Description for Task 5', false);
```
If you noticed above, we only entered 4 columns while there are 5 columns in the our table definition. Because of TaskID is auto incremented, we do not have to enter specific value for that field.

That's it for today. Let's meet at next blog post.