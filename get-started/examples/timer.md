## Create Timer

### Code example

`swoole_timer.php`

``` php
// Executes the given callback function repeatedly, with a fixed time dalay between each call
swoole_timer_tick(2000, function($timer_id){
	echo "tick 2000ms\n";
});

// Executes the given callback function after specified delay
swoole_timer_after(3000, function(){
	echo "after 3000ms\n";
});
```

Swoole provides the async timer like the `setInterval/setTimeout` of Javascript which is in milliseconds.

- `swoole_timer_tick($time, $callable)` corresponds to the `setInterval` of Javascript which is called repeatedly

- `swoole_timer_after($time, $callable)` corresponds to the `setTimeout` of Javascript which is called after a specified time

- `swoole_timer_after` and `swoole_timer_tick` return a integer which represents the id of this timer

- Use `swoole_timer_clear($timer_id)` to clear the timer
