# Natas wargame writeups

Home page: https://overthewire.org/wargames/natas/

## Connect the game

```
http://natas<level>.natas.labs.overthewire.org
```
with `<level>` is your level's room

+ no SSH login
+ all passwords are also stored in `/etc/natas_webpass/`

## Notes for game

+ view source, devtools
+ Burpsuite skills

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

## Level 4-

> topic: burpsuite

```
open BurpSuite, catch requests
click Refresh
change Referer: http://natas5.natas.labs.overthewire.org/
```

| Username | Password |
| :--- | :--- |
| natas5 | Z0NsrtIkJoKALBCLi5eqFfcRN82Au2oD |

```
open BurpSuite, catch requests
change Cookie: loggedin=1
```

| Username | Password |
| :--- | :--- |
| natas6 | fOIvE0MDtPTgRhqmmvvAOt2EfXR6uQgR |

```
check sourcecode
http://natas6.natas.labs.overthewire.org/includes/secret.inc
input FOEIUWGHFEEUHOFUOIU
```

| Username | Password |
| :--- | :--- |
| natas7 | jmxSiH3SP6Sonf8dv66ng8v1cIEdjXWr |























































