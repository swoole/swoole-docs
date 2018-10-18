## Configuration

### log_level

Set the level of log.

The log that is inferior to the given log_level will not be recorded to log file.

#### Usage

```php
$serv->set(array(
    'log_level' => 1,
));
```

#### Log level list

```
0 =>DEBUG // all the levels of log will be recorded
1 =>TRACE
2 =>INFO
3 =>NOTICE
4 =>WARNING
5 =>ERROR
```
