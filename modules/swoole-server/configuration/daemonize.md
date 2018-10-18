## Configuration

### daemonize

Daemonize the swoole server process.

If the value of `daemonize` is more than 1, the swoole server will be daemonized.

The program which wants to run long time must enable this configuration.

If the `daemonize` has been enabled, the standard output and error of the program will be redirected to [logfile](/modules/swoole-server/configuration/log_file.md). And if the configuration of `log_file` hasn't been set, the standard output and error of the program will be redirected to `/dev/null`.

> After daemonizing the processes, the value of `CWD` will change and the relative path of file will be different. So it must use absolute path in the program.
