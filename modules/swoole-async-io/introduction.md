# Swoole Async File I/O

The swoole provides the functions of asynchronous file I/O. 

> The task process in swoole_server is syncing and blocking without using EventLoop, can't benefit from Async I/O.

## Methods

### swoole_async_set(array $setting);

Update the Async I/O options:

- thread_num: number of async file I/O threads

- aio_mode: AIO mode: SWOOLE_AIO_BASE/SWOOLE_AIO_LINUX

    `SWOOLE_AIO_LINUX` : use the linux native aio system call
    `SWOOLE_AIO_BASE` : use the thread pool to realize the async io

- enable_signalfd: whether enable signalfd

- socket_buffer_size: socket buffer size

- socket_dontwait: do not block when the buffer is full

```php
<?php
swoole_async_set(array(
    'aio_mode' => SWOOLE_AIO_LINUX,
));
```

### swoole_async_readfile(string $filename, mixed $callback);

Read files in the async way. When the operation of reading content from file finished, the callback registered is callback automatically.

The max length of file is 4M.

Example:

``` php
<?php
swoole_async_readfile(__DIR__."/server.php", function($filename, $content) {
     echo "$filename: $content";
});
```

### swoole_async_writefile(string $filename, string $fileContent, callable $callback = null, int $flags = 0)

Write file in the async way. When the operation of writing content to file finished, the callback registered is callback automatically.

- `$filename` the file path of file. If fail to open this file, the method return false; 

- `$fileContent` the content to write to the file, The max length is 4M.

- `$callback` the callback function triggered when the operation of writing content to file finished.

- `$flags` `FILE_APPEND`: append content to the end of file.
            If the aio mode setted by `swoole_async_set` is `SWOOLE_AIO_BASE`, the method can't support append content to the end of file and must set the value of `$fileContent` to integer multiples of 4096.

Example:

``` php
<?php
swoole_async_writefile('test.log', $file_content, function($filename) {
    echo "wirte ok.\n";
}, $flags = 0);
```

### bool swoole_async_read(string $filename, mixed $callback, int $size = 8192, int $offset = 0);

Read the file content stream in the async way. When the operation of reading content from file finished, the callback registered is callback automatically.

The difference between this method and `swoole_async_readfile` is that the former reads file by fragment and uses less memory. This method reads content of `$size` length from file every time and can be used to read big file.

- `$size` the size of content to read from file

The callback function prototype is :
```
bool callback(string $filename, string $content);
```
- `$filename` the name of file

- `$content` the content readed from the file.

You can control that if continue to read file by return true or false in the callback function.

- `return true;` continue to read file

- `return false;` stop to read file and close file

### bool swoole_async_write(string $filename, string $content, int $offset = -1, mixed $callback = NULL);

Write file stream in the async way. When the operation of writing content to file finished, the callback registered is callback automatically.

The difference between this method and `swoole_async_writefile` is that the former writes file by fragment and uses less memory.

- `$offset` The method uses the `$offset` parameter to decide the postion to write file. 
            If the `$offset` is setted to `-1`, it stands for that it appends content to the end of file.
            If the aio mode setted by `swoole_async_set` is `SWOOLE_AIO_BASE`, the method can't support append content to the end of file and must set the value of `$content` and `$offset` to integer multiples of 512. Otherwise the call of this method will fail and set the error code to `EINVAL`.

### swoole_async_dns_lookup(string $host, mixed $callback)

Async DNS lookup. The call of this method is non-blocking. 

- If the operation of DNS lookup finished, the callback registered is called automatically.

- If the operation of DNS lookup failed, the callback registered is also called automatically and the parameter `$ip` will be empty.

Example:

``` php
<?php
// Disable DNS cache
swoole_async_set(array(
    'disable_dns_cache' => true,
));
// Set the DNS server list
swoole_async_set(array(
    'dns_server' => '8.8.8.8',
));
// Lookup using random DNS server
swoole_async_set(array(
    'dns_lookup_random' => true,
));

// Lookup the DNS of www.google.com
swoole_async_dns_lookup("www.google.com", function($host, $ip){
    echo "{$host} : {$ip}\n";
});
echo "start async dns lookup\n";
```
