## QuickStart

### Initialize the server

``` php
<?php
$server = new swoole_server("127.0.0.1", 9501, SWOOLE_BASE, SWOOLE_SOCK_TCP);
```

### Set runtime paramaters

``` php
<?php
$server->set(array(
    'worker_num' => 4, // The number of worker processes
    'daemonize' => true, // Whether start as a daemon process
    'backlog' => 128, // TCP backlog connection number
));
```

### Register callback functions

``` php
<?php
$server->on('Connect', 'my_onConnect');
$server->on('Receive', 'my_onReceive');
$server->on('Close', 'my_onClose');
```
> There are [four types of callback functions](/modules/swoole-server/common-problems.md)

### Start the server

``` php
<?php
$server->start();
```

### Get the server attributes

``` php
<?php
$server->manager_pid; // PID of manager process, send SIGUSR1 to this process to reload the application
$server->master_pid;  // PID of master process, send SIGTERM signal to this process to shutdown the server
$server->connections; // The connections established
```
