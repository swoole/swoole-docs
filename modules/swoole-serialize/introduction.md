# Swoole Serialize

Swoole provides a fast and high performance serialization module.

## Methods

### string swoole_serialize->pack(mixed $data, $is_fast = 0);

#### Illustration

Serialize the data.

#### Parameter

- `$data` the data to serialize

- `$is_fast` if enable fast mode

#### Return

If the process of serialization succeeds, it returns the binary string as the result of serialization. Otherwise, it returns false.


### mixed swoole_serialize->unpack($data);

#### Illustration

Unserialize the data.

#### Parameter

- `$data` the data to unserialize

#### Return

If the process of unserialization succeeds, it returns the unserialized data. Otherwise, it returns false.
