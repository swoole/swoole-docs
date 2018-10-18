## Configuration

### max_conn

The max number of connection the server could handle at the same time.

After exceed this limit, the swoole server will refuse the new coming connection.

> `max_conn` should be less than `ulimit -n`
> `max_conn` should be more than `(serv->worker_num + SwooleG.task_worker_num) * 2 + 32`
> the default value of `max_conn` is `ulimit -n`
> the value of `max_conn` should not be too large and be set according to the memory usage of server.
