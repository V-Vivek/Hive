# Map Data Type
- In Hive, a map is a collection type that allows you to store key-value pairs. 
- It is similar to a dictionary or associative array in other programming languages. 
- The key and value can be of any supported data type in Hive.
```
-- Create a table with a map column
CREATE TABLE mytable (id INT, mymap MAP<STRING, INT>);

-- Insert some data into the table
INSERT INTO mytable VALUES (1, MAP("apple", 2, "banana", 3, "orange", 1));

-- Query the map column
SELECT mymap FROM mytable WHERE id = 1;
```
```
Output - {"apple":2,"banana":3,"orange":1}
```

# Functions

## MAP(key1, value1, key2, value2, ...)
- Creates a map with the specified key-value pairs.
```
-- Create a map with string keys and integer values
SELECT MAP("apple", 2, "banana", 3, "orange", 1);
```
```
-- Output: {"apple":2,"banana":3,"orange":1}
```

## mymap[key]
- Retrieves the value associated with the specified key from the map mymap.
```
-- Retrieve the value associated with the "banana" key
SELECT mymap["banana"] FROM mytable;
```
```
Output - 3
```

## mymap.keys()
- Returns an array of all the keys in the map mymap.
```
-- Retrieve all keys in the map
SELECT map_keys(mymap) FROM mytable;
```
```
Output - ["apple","banana","orange"]
```

## mymap.values()
- Returns an array of all the values in the map mymap.
```
-- Retrieve all values in the map
SELECT map_values(mymap) FROM mytable;
```
```
Output - [2,3,1]
```

## size()
- This function is used to get the number of elements in a map.
- It takes a map as an argument and returns the size of the map.
```
-- Retrieve size of the map
SELECT size(mymap) FROM mytable;
```
```
Output - 3
```

## explode()
- This function is used to convert the map into a table.
- It takes the map as an argument and returns a table with one row for each key-value pair in the map.
```
SELECT explode(mymap) FROM mytable;
```
```
Output:
key     value
apple   2
banana  3
orange  1
```
