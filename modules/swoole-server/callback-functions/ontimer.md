## Events and Callback functions

### onTimer

The event `timer` happens when the timer expires.

#### Example

```php
function onTimer(swoole_server $server, int $interval);
```

`$interval` is the interval set by the timer. You can distinguish the timer by the interval.

The timer is added by the `$serv->addtimer`.
