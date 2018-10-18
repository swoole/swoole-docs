## Configuration

### open_eof_split

Enable the split of data to package.

Once the configuration `open_eof_check` has been set, the worker process will receive the data ending with the specified string. This data may contain one or serval whole package. In this situation, you can enable the `open_eof_split` to split the data to package automatically. And then the callback function `onReceive` will receive a whole package.
