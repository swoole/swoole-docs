## Configuration

### open_length_check

Open the check of package length.

If this configuration has enabled, the swoole will open the analysis of package which has fixed header and body. And the worker process will receive a whole package in the callback function `onReceive`.

This configuration should work with three other configurations.

#### package_length_type

Use some field in the header of package to stand for the length the package. The swoole supports 10 types of length. Check the full list in [the configuration of package_length_type](/modules/swoole-server/configuration/package_length_type.md)

#### package_body_offset

The offset of the package to calculate the length of package.

- `0`, the length stands for the length of header and body

- `N`, this value stands for that the length of header is N and the length of package only contains the length of body.

#### package_length_offset

The offset of value of length in the header

##### Example

```c
struct
{
    uint32_t type;
    uint32_t uid;
    uint32_t length;
    uint32_t serid;
    char body[0];
}
```
The configuration designed from the above protocol design

```php
$server->set(array(
    'open_length_check' => true,
    'package_max_length' => 81920,
    'package_length_type' => 'N',
    'package_length_offset' => 8,
    'package_body_offset' => 16,
));
```
