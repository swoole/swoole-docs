## Create Async Task

### Background

If you want to execute a time-consuming operation in the program, for instance broadcasting in a chat program and sending email in a web server. These operations would block the program and slow down the program in reuslt. 

Swoole provides the function for async task. You can send these time-consuming tasks to a task worker process pool to execute.

### Code Example

`async_task.php`

``` php
// Create the server object and listen 127.0.0.1:9501 port
$server = new swoole_server("127.0.0.1", 9501);

// Set the number of task worker process
$server->set(array(
	'task_worker_num' => 4
));

// Register the function for the event of receiving
$server->on('receive', function($server, $fd, $from_id, $data){
	
	// Send data to the task worker process
	$task_id = $server->task($data);
	echo "Dispatch async task: id = {$task_id}\n";

	// Send data to the client
    $server->send($fd, "Server: " . $data);
});

// Register the function for the event of receiving task
$server->on('task', function($server, $task_id, $from_id, $data){
	echo "Receive new task, id : {$task_id}\n";

	// Return the result of executing task
	$server->finish("{$data} -> finished");
});

// Register the function for the event of receiving task result
$server->on('finish', function($server, $task_id, $data){
	// Handle the result of executing task
	echo "Async task {$task_id} result : {$data} \n";
});

// Start the server
$server->start();
```

The code above is based on `tcp_server.php`. To send task, it needs to register two functions for event `task` and `finish`. And more, it needs to set the num of task worker precess according to your task amount and elapsed time.

> The callback function registered for event `finish` is optional. There is no need to set this function when the task doesn't return result

### Run program

``` bash
php server.php
```
