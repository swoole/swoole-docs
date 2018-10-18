## Configuration

### open_eof_check

This configuration is to check the package eof. The package eof is set by [the configuration package_eof](/modules/swoole-server/configuration/package_eof.md)

#### Usage

If this configuration has been enabled, the swoole will check the end of data from the client. If the end of data from client is the string set by `package_eof`, the swoole will send the data to the worker process otherwise the swoole will continue receive and joint the data from client.

```php
array(
	'open_eof_check' => true,
	'package_eof' => "\r\n",
)
```
The above configuration example can be used for Memcache or POP protocol which ends by `\r\n`. Once set, the worker process will receive one or serveral whole packages. In the worker process, you should use `explode("\r\n", $data)` split the data or set [the configuration package_eof](/modules/swoole-server/configuration/open_eof_split.md) to split the data automatically.
