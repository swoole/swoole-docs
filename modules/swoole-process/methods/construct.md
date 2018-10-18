# Swoole Process Manager

## Methods

### swoole_process->__construct

#### Prototype

```php
swoole_process swoole_process->__construct(mixed $function, bool $redirect_stdin_stdout = false, int $create_pipe = 2);
```

#### Illustration

Construct a child process with the callback function executed in the child process, optionally redirect the standard I/O to pipes between the parent process and the child processes.

> When the parent process is stopped, the child processes will receive *CLOSE* event from the pipe.

#### Parameter

- `$function` the callback function executed in the child process. If the execution of this function in the child process finished, the child process would exit.

- `$redirect_stdin_stdout` if enable the redirection of stdin and stdout of child process. If `$redirect_stdin_stdout` is `true`, the output of child process will be written to the the pipe of main process and the input of child process will come from the pipe. The default of mode is blocking.

- `$create_pipe` if create the pipe. `0` don't create the pipe, `1` create the `SOCK_STREAM` pipe, `2` create the `SOCK_DGRAM` pipe. If `$redirect_stdin_stdout` is `true`, this parameter is set to `1`.

#### Return

the object of `swoole_process`

#### Example
```
<?php
$process = new swoole_process(function($process){
    echo "the pid of child process is " . $worker->pid . "\n";
    echo "the file descriptor of pipe is " . $worker->pipe . "\n";
    $process->write("hello");
}, false, true);

$process->start();

usleep(100);

echo $process->read();
```
