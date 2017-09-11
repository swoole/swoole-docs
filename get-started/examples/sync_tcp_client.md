## Create Sync TCP Client

### Code example

`sync_tcp_client.php`

``` php
// Create the tcp client
$client = new swoole_client(SWOOLE_SOCK_TCP);

// Connect to the tcp server
if(!$client->connect('127.0.0.1', 9501, 0.5))
{
    die("connect failed");
}

// Send data to the tcp server
if(!$client->send("Hello World"))
{
    die("send failed");
}

// Receive data from the tcp server
$data = $client->recv();
if(!$data)
{
    die("recv failed");
}
echo $data;

// Close the connection
$client->close();
```

The code above creates a synchronous TCP client. This client can be used to connect the tcp server we have created in the previous example. When the client send a string 'Hello World' to the server, the server would respond with a string 'Server: Hello World'.

This client is synchronous and blocking. The operations, like connect, send and recv, don't return until the IO operation completes. The synchronous and blocking operation doesn't consume CPU resource and switch to `sleep` mode automatically before the IO completes. When the IO operation completes, the system will awake the process and continue to execute.

- If the operation of connecting server needs 100ms, `$client->connect` will block and cost 100ms.

- `$client->send` can return immediately when to send small data. But it could be blocked when to send large data because the data could fill in the socket send buffer.

- `$client->recv` blocks to wait the return data of the server. The elapsed time equals to the sum of the time for procees data in server and the time for tranporting data

### Run program

``` bash
php sync_tcp_client.php
```
