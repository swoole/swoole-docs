# Swoole scheduler

The swoole server provides the methods `swoole_server->tick` and `swoole_server->after` to realize the asynchronous timer. For the swoole client, the swoole also provides the functions to realize the asynchronous timer. These schedule functions are accurate to milliseconds.

The swoole timer is based on timerfd and epoll.

## Methods

### int swoole_timer_tick(int $duration_ms, callable $callback, mixed $param = NULL);

Trigger a timer tick by interval.

#### Parameter

* `$duration_ms`	the number of millisecond
* `$callback`       the callback function called repeatedly with a fixed time delay between each call. The callback will be passed two arguments : 
                        `$timer_id` : id of timer which can be used to clear this timer using `swoole_timer_clear`
                        `$param` : the param passed in `swoole_timer_tick` 
* `$param`          the param passed to the callback

#### Return

the timer id

#### Example

``` php
<?php
function test($timerid, $param)
{
    var_dump($timerid);
    var_dump($param);
}
swoole_timer_tick(1500, "test",["param1", "param2"]);
```

### swoole_timer_after(int $after_duration_ms, callable $callback, mixed $param = NULL);

Trigger a one time callback function in the future.

#### Parameter

* `$after_duration_ms`	the number of millisecond
* `$callback`           the callback function called after a setted time. The callback will be passed an arguments : 
                        `$param` : the param passed in `swoole_timer_tick` 
* `$param`          the param passed to the callback

#### Return

the timer id

#### Example

``` php
<?php
function test($param)
{
    var_dump(func_get_args());
    var_dump($param);
}

swoole_timer_after(1500, "test",["param1", "param2"]);
```

### boolean swoole_timer_clear($timer_id);

Cancel the timer tick or one time tick. Alias of function *swoole_timer_clear*.

#### Parameter

* `$timer_id`	the id of timer

#### Return

bool

#### Example

``` php
<?php
$count = 0;
function test($timerid, $param)
{
    global $count;
    $count++;
    var_dump($count);
    if($count >= 10)
    {
        swoole_timer_clear($timerid);
    }
}

swoole_timer_tick(1000, "test",["param1", "param2"]);
```
