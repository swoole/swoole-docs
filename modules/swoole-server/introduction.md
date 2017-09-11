## Swoole server

Swoole server provides the API for developers to write TCP, UDP, Unix Socket asynchronous servers. It supports IPv4, IPv6, one Way, two Way SSL and TLS Encryption. Developers do not have to know the internal implementations, only have to write the logics of the server in the callback functions.

> Swoole server apis only can be used in the php cli mode.

### Table of Contents

* [Quick Start](/modules/swoole-server/quick-start.md)

* [Methods List](/modules/swoole-server/methods.md)

* [Properties List](/modules/swoole-server/properties.md)

* [Configurations List](/modules/swoole-server/configuration.md)

* [Predefined Constants](/modules/swoole-server/predefined-constants.md)

* [Callback functions](/modules/swoole-server/callback-functions.md)

* [Listening On Multiple Ports](/modules/swoole-server/multiple_ports.md)

* [Performance testing](/modules/swoole-server/performance-testing.md)

### Swoole Working Flow Chart(for SWOOLE_PROCESS mode)
![Swoole Flow](https://github.com/yannsun/swoole-docs/blob/master/static/img/swoole_process.png)

### Swoole Process/Thread Structure Chart(for SWOOLE_PROCESS mode)
![Swoole Structure](https://github.com/yannsun/swoole-docs/blob/master/static/img/swoole_structure.png)
