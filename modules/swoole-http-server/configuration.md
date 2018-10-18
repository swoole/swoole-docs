## Swoole HTTP Server

### Configurations List

The object of swoole_http_server class can set some other configurations except for the configurations of `swoole_server` class.

- `upload_tmp_dir`

Set the temporary path of upload files.

```php
$serv->set(array(
    'upload_tmp_dir' => '/data/uploadfiles/',
));
```
> The max length of `upload_tmp_dir` is 220 bytes.


- `http_parse_post`

Enable the analysis of POST data. If you set this configuration to false, the swoole will close the analysis of POST data. And if you set this configuration to true, the swoole will analyze the POST data whose `Content-Type` is `x-www-form-urlencoded`.

```php
$serv->set(array(
    'http_parse_post' => false,
));
```

- `document_root`

Set the root path of static files. This configuration needs to work with `enable_static_handler`.

If the `document_root` is set and the value of `enable_static_handler` is `true`, the swoole will judge if the request file exists. If the file requested exists, the swoole will send the file to client directly and don't call the callback function of `request`.

```php
$server->set([
    'document_root' => '/data/webroot/example.com',
    'enable_static_handler' => true,
]);
```
