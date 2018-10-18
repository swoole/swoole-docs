## Configuration

### message_queue_key

Set the key of message queue.

This configuration only works if [the configuration of task_ipc_mode](/modules/swoole-server/configuration/task_ipc_mode.md) has been set to `2` or `3`.

The default value of `message_queue_key` is calculated by `ftok($php_script_file, 1)`.
