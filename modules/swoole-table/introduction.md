# Swoole Table

Swoole table is a high performance memory management module, implemented based on shared memory and spin lock. 

> In order to keep the data synchronization, have to use Swoole\Lock if the memory is modified and accessed by multiple threads or processes.

Swoole table provides a two dimensions memory table for developers. 

## Why to use swoole table

* High performance, the single thread read/write speed is more than 2 millions per second.
* Can be used by multiple threads or processes.
* In application counters storage.

## Methods

### swoole_table->__construct($table_size);

Construct a Swoole memory table with size.

### swoole_table->column($name, $type, $size = 0);

Set the data type and size of the columns.

### boolean swoole_table->create();

Create the swoole memory table.

### swoole_table->set(string $row_key, array $value);

Update a row of the table by $row_key.

### swoole_table->get(string $row_key, string $column_key);

Get the value by $row_key and $column_key.

### swoole_table->del(string $row_key);

Delete a row by $row_key.

### swoole_table->exist(string $row_key);

Check if a row is existed by $row_key.

### swoole_table->incr(string $row_key, string $column_key, integer $incr_by = 1);

Increment the value by $row_key and $column_key.

### swoole_table->decr(string $row_key, string $column_key, integer $decr_by = 1);

Decrement the value by $row_key and $column_key.

### long swoole_table->count($mode = 0);

Count the rows in the table, or count all the elements in the table if $mode = 1.

### boolean swoole_table->destroy();

Destroy the memory table.

### swoole_table->rewind

> PCRE is needed for this function

### swoole_table->next

> PCRE is needed for this function

### swoole_table->current

> PCRE is needed for this function

### swoole_table->key

> PCRE is needed for this function

### swoole_table->valid

> PCRE is needed for this function


### Iterator and Countable

> The iterator and countable depends on pcre-devel

```php
<?php
foreach($table as $row)
{
    var_dump($row);
}
echo count($table);
```

### Example


