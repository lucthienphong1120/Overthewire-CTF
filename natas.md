# Natas wargame writeups

Home page: https://overthewire.org/wargames/natas/

## Connect the game

```http
http://natas<level>.natas.labs.overthewire.org
```
with `<level>` is your level's room

+ no SSH login
+ all passwords are also stored in `/etc/natas_webpass/`
+ 

## Notes for game

+ most useful command is `ls -la`
+ useful resources are `man`, `help`, `--help`, `-h`, google search, wiki
+ directory store password 's room is `/etc/bandit_pass/bandit<level>` (can see, but can't open)
+ directory store file 's room is `/home/bandit<level>`
+ can't work on [~] (/home/user) because of restricted permissions
+ you should create a new folder for each level in /tmp/ to work because you will have full control with it

## Level 0-3

> topic: basic

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

## Level 4-

> topic: burpsuite

```
open BurpSuite, catch requests
click Refresh
change Referer header to http://natas5.natas.labs.overthewire.org/
```

| Username | Password |
| :--- | :--- |
| natas4 | Z0NsrtIkJoKALBCLi5eqFfcRN82Au2oD |







