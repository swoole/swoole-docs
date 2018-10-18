# Swoole Process Manager

## Methods

### swoole_process->name

#### Prototype

```php
swoole_process->name(string $new_process_name);
```

#### Illustration

Set name of the process started.

> After the call of `swoole_process->call`, the name will be reset

#### Parameter

- `$new_process_name` string

#### Return

void

#### Example
```
<?php
$process = new swoole_process(function($worker){
    echo "the pid of child process is " . $worker->pid . "\n";
    echo "the file descriptor of pipe is " . $worker->pipe . "\n";

    $worker->write("Hello main process\n");

    $worker->name("php child process"); // set name of the process

    sleep(100);
}, false, true);

$process->start();

usleep(100);

echo $process->read();
```
