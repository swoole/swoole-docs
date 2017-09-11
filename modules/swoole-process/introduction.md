# Swoole Process Manager

Swoole process manager can be used to replace PHP *pcntl* extension. Compare with PHP pcntl, Swoole process manager provides more features:

* Interprocess communication based on unixsock, with read/write or push/pop API.
* Redirect standard input and output
* The child process can use swoole_event callbacks.
* Exec API enable the child process execute Linux applications and communicate with parent process

## Table of Contents

* [Methods List](/modules/swoole-process/methods.md)
