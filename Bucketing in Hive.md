# Bucketing
- In Hive, bucketing is a technique used for partitioning large tables into smaller, more manageable pieces called buckets. 
- It involves grouping data based on certain columns and storing it in separate files or directories.
- When you bucket a table in Hive, you can control the number of buckets, the columns to use for bucketing and the sorting order of the data within each bucket. 
- By doing so, you can optimize query performance and reduce the amount of data that needs to be processed.
- Bucketing is based on hashing function on the bucketed column along with mod (by the total number of buckets).
- Where the hash_function depends on the type of the bucketing column.

# Need of Bucketing
- Partitioning may not garuntee to create equal size of partitions.
- For example when we are partitioning our tables based geographic locations like country. 
- Some bigger countries will have large partitions (ex: 4-5 countries itself contributing 70-80% of total data).
- While small countries data will create small partitions (remaining all countries in the world may contribute to just 20-30 % of total data). 
- Hence, at that time Partitioning will not be ideal.
- To solve that problem of over partitioning, Hive offers Bucketing concept.

## Create Bucketed table
- We need to specify buckeing column under ```CLUSTERED BY ()``` clause
- Specify number of buckets using ```INTO n BUCKETS```
- Note that ```SORTED BY ()``` is optional
```
CREATE TABLE sales_data_bucketed
(
  transaction_id INT,
  customer_id INT,
  product_id INT,
  quantity INT,
  price FLOAT,
  sales_date DATE
)
CLUSTERED BY (customer_id)
SORTED BY (customer_id)
INTO 4 BUCKETS;
```

## Insert data from other table
```
INSERT INTO sales_data_bucketed
SELECT * FROM other_table;
```

