## Installation

### Installation

#### Install by binary releases

##### Linux users

> Swoole is available as a PECL compatible package

``` bash
pecl install swoole
```
##### MacOS X \(macOS\) users

> It is highly recommended to install Swoole on Mac OS X or macOS systems via homebrew

``` bash
brew install swoole
```

#### Building swoole from sources

##### Download link

You are recommended to download the latest stable version of swoole. You can download the source code from one of the following the links.

- [https://github.com/swoole/swoole-src/releases](https://github.com/swoole/swoole-src/releases)
- [http://pecl.php.net/package/swoole](http://pecl.php.net/package/swoole)
- [http://git.oschina.net/swoole/swoole/releases](http://git.oschina.net/swoole/swoole/releases)

##### Steps of Compilation 

The process of compile and install the swoole extension for PHP

``` bash
cd swoole          #  enter the directory of swoole source code   
phpize       	   #  prepare the build environment for a PHP extension
./configure        #  add configuration paramaters as needed
make 			   #  a successful result of make is swoole/module/swoole.so
sudo make install  #  install the swoole into the PHP extensions directory
```

### Enable swoole

After installing the swoole extension to the PHP extensions directory, you will need to edit php.ini and add an extension=swoole.so line before you can use the swoole extension.

```bash
php -i | grep php.ini                      # check the php.ini file location
sudo echo "extension=swoole.so" > php.ini  # add the extension=swoole.so to the end of php.ini
php -m | grep swoole                       # check if the swoole extension has been enabled
```

### Configuration paramaters

These configurations are used for enabling some features.

`--enable-swoole-debug` 

Enable the debug logs of swoole. Don't enable this configuration in production environment.

`--enable-sockets` 

Enable sockets support. It depends on the PHP sockets extension. If this configuration has been enabled, the function swoole_event_add() could add the connection created by the sockets extension to the event loop of swoole. And the function getSocket() depends on this configuration.  

`--enable-openssl` 

Enable openssl support. It depends on the libssl.so library given by operating system.

`--with-openssl-dir`

Set the path of openssl library, for example:`--with-openssl-dir=/opt/openssl/.`

`--enable-http2`

Enable the support of HTTP2. It depends on nghttp2 library.

`--enable-async-redis`

Enable the support of async redis client. It depends on hiredis library.

`--enable-timewheel`

Enable the support of timewheel and optimize the heartbeat algorithm.

> This is an experimental feature. Don't use this feature in production environment.

`--enable-mysqlnd`

Enable the support of mysqlnd, for example `swoole_mysql::escapse`.

`--enable-ringbuffer`

Enable the support of ringbuffer memory pool.

> This is an experimental feature. Don't use this feature in production environment


**After the installation of swoole,  try the [examples](/get-started/examples.md) written by swoole.**
