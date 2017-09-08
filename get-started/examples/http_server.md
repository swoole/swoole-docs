## Create Web Server

### Code example 

`http_server.php`

``` php
// Create the http server object 
$http_server = new swoole_http_server("127.0.0.1", 9503);

// Register the event of request
$http_server->on('request', function($request, $response){
    var_dump($request->get, $request->post);
    $response->header("Content-Type", "text/html;charset=utf-8");
    $response->end("<h1>Hello Swoole " . rand(1000, 9999) . "</h1>");
});

// Start the server
$http_server->start();
```

For http server, the most important task is to handle the request and send the response. You can just register the function for event `request`. 

When the new http request comes, the server will call the function registered for request to handle. The swoole will pass two parameters, `$request` and `$response`, in the registered function. 

The parameter `$request` contains the information about the http request, for example GET/POST data.

The parameter `$response` is handled by swoole to send the data to client. `$response->end($data)` will output the `$data` to the client in the form of html and  close the connection. 

- '0.0.0.0' represents that the server listens all ip addresses.
- '9501' represents the port that the server listens at. If the port has already been used, the swoole would throw a fatal error and stop execution.

### Run program

``` bash
php http_server.php
```

- Use the browser or run `curl http://127.0.0.1:9501` in command line to check the result of program

- Use the tool `ab` of apache to test the performance of this http server
