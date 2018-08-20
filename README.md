# PHP Library SqlDB

PHP Library for working with SQL databases.

## Background ##
- MySQL and SQLite supported
- Unified data types. The data types are developer orientated (string, text, integer, float, blob). These are then translated to the correct column type for the corresponding database.
- Fluent interface for building queries

## Installation ##

1) Via composer command line
```sh
composer require sinevia/php-library-sqldb
```

2) Via composer file:

Add the following to your composer file.

```json
    "require": {
        "sinevia/php-library-sqldb": "dev-master"
    },
```

## Data Types ##

| Data Type | MySLQ Data Type | SQLite Data Type |
|-----------|-----------------|------------------|
| STRING    | VARCHAR         | TEXT             |
| TEXT      | LONG TEXT       | TEXT             |
| INTGER    | BIG INT         | INTEGER          |
| FLOAT     | DOUBLE          | FLOAT            |
| BLOB      | LONG BLOB       | TEXT             |



## Usage ##

### 1) Creating new instance ###


```php
$db = new SqlDB(array(
    'database_type'=>'mysql',
    'database_name'=>'db_name',
    'database_host'=>'db_host',
    'database_user'=>'db_user',
    'database_pass'=>'db_pass'
));
```


### 2) Creating new table ###

```php
// Check if table already exists?
if ($db->table("person")->exists() == false) {
    // Create table
    $db->table("person")
        ->column("Id", "INTEGER", "NOT NULL PRIMARY KEY")
        ->column("FirstName", "STRING")
        ->column("LastName", "STRING")
        ->create();
}
```

### 3) Inserting rows ###

```php
$db->table('person')->insert([
    'FirstName' => 'Peter',
    'LastName' => 'Pan',
]);

// Getting the new autoincremented ID
$insertedId = $db->lastInsertId();
```
