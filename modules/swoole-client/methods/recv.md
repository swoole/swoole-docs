# Swoole TCP/UDP client

## Methods

### swoole_client->recv

#### Prototype

```php
string swoole_client->recv(int $size = 65535, int $flags = 0);
```

#### Illustration

Receive data from the remote socket.

#### Parameter

- `$size` the buffer size of receiving data

- `$flags` the configuration of receiving data(Check the predefined constants of class swoole_client)

> If the swoole client has set the configuration about check of `EOF/Length`, it doesn't need to set the parameter `$size` and `$flags` and the swoole client will return the whole package.

#### Return

If the client receives data successfully, it returns the length of data received. Or it returns `false` and sets `$swoole_client->errCode`.

#### Example
``` php
$client->recv(8192, swoole_client::MSG_PEEK | swoole_client::MSG_WAITALL);
```
