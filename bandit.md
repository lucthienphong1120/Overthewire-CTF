# Bandit wargame writeups

Home page: https://overthewire.org/wargames/bandit/

## Connect the game

```bash
ssh bandit<level>@bandit.labs.overthewire.org -p 2220
```
with `<level>` is your level 's room

```bash
ssh bandit<level>@localhost
```
to connect to next level (if you already in the game)

## Notes for game

+ most useful command is `ls -la`
+ useful resources are `man`, `help`, `--help`, `-h`, google search, wiki
+ directory store password 's room is `/etc/bandit_pass/bandit<level>` (can see, but can't open)
+ directory store file 's room is `/home/bandit<level>`
+ can't work on [~] (/home/user) because of restricted permissions
+ you should create a new folder for each level in /tmp/ to work because you will have full control with it

## Level 0-6

> topic: file and folder

| Username | Password |
| :--- | :--- |
| bandit0 | bandit0 |

```bash
cat readme
```

| Username | Password |
| :--- | :--- |
| bandit1 | boJ9jbbUNNfktd78OOpsqOltutMc3MY1 |

```bash
cat ./- # or cat < -
```

| Username | Password |
| :--- | :--- |
| bandit2 | CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9 |

```bash
cat "spaces in this filename"
```

| Username | Password |
| :--- | :--- |
| bandit3 | UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK |

```bash
cd inhere
cat .hidden
```

| Username | Password |
| :--- | :--- |
| bandit4 | pIwrPrtPN36QITSp3EQaw936yaFoFgAB |

```bash
cd inhere/
file ./*	# show all file type
cat ./-file07   # or cat < -file07
```

| Username | Password |
| :--- | :--- |
| bandit5 | koReBOKuIDDepwhWk7jZC0RTdopnAYKh |

```bash
find -type f -size 1033c ! -executable
cat ./maybehere07/.file2
```

| Username | Password |
| :--- | :--- |
| bandit6 | DXjZPULLxYr17uwoI01bNLQbtFemEgo7 |

```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null	# turn error log into /dev/null
cat /var/lib/dpkg/info/bandit7.password
```
## Level 7-12

> topic: handle file data

| Username | Password |
| :--- | :--- |
| bandit7 | HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs |

```bash
grep "millionth" data.txt
```

| Username | Password |
| :--- | :--- |
| bandit8 | cvX2JJa4CFALtqS87jk27qwqGhBM9plV |

```bash
sort data.txt | uniq -u	# sort to use uniq and -u to find the line appear once
```

| Username | Password |
| :--- | :--- |
| bandit9 | UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR |

```bash
strings data.txt | grep "=="	# output strings available and grep ==
```

| Username | Password |
| :--- | :--- |
| bandit10 | truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk |

```bash
base64 -d data.txt	# -d mean decode
```

| Username | Password |
| :--- | :--- |
| bandit11 | IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR |

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'	# see rot13 on wikipedia
```

| Username | Password |
| :--- | :--- |
| bandit12 | 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu |

```bash
mkdir /tmp/hello12
cp data.txt /tmp/hello12
cd /tmp/hello12	# must work at this place, because home don't have permission
file data.txt
xxd -r data.txt > crack.out
file crack.out
mv crack.out crack.gz
gzip -d crack.gz
file crack
bzip2 -d crack
file crack.out
mv crack.out crack.gz
gzip -d crack.gz
tar -xvf crack
file data5.bin
tar -xvf data5.bin
file data6.bin
bzip2 -d data6.bin
file data6.bin.out
tar -xvf file data6.bin.out
file data8.bin
mv data8.bin data8.gz
gzip -d data8.gz
file data8
cat data8
```

# Level 13-20

> topic: network protocol

| Username | Password |
| :--- | :--- |
| bandit13 | 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL |

```bash
ssh -i sshkey.private bandit14@localhost
cat /etc/bandit_pass/bandit14
```

| Username | Password |
| :--- | :--- |
| bandit14 | 4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e |

```bash
cat /etc/bandit_pass/bandit14 | nc localhost 30000	# submitting the password of the current level to port 30000 on localhost
```

| Username | Password |
| :--- | :--- |
| bandit15 | BfMYroe26WYalil77FoDi9qh59eK5xNr |

```bash
openssl s_client -ign_eof -connect localhost:30001
BfMYroe26WYalil77FoDi9qh59eK5xNr	# type password and enter
```

| Username | Password |
| :--- | :--- |
| bandit16 | cluFn7wTiGryunymYOu4RcffSxQluehd |

```bash
nmap -sV -p 31000-32000 localhost	# -p is range of ports, -sV is service
openssl s_client --connect localhost:31790
cluFn7wTiGryunymYOu4RcffSxQluehd	# type password and enter
echo key > key.private
ssh -i key.private bandit17@localhost
cat /etc/bandit_pass/bandit17
```

| Username | Password |
| :--- | :--- |
| bandit17 | xLYVMN9WE5zQ5vHacb0sZEVqbrp7nBTn |

```bash
diff passwords.old passwords.new
```

| Username | Password |
| :--- | :--- |
| bandit18 | kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd |

```bash
ssh bandit18@localhost -t /bin/sh	# run pseudo-terminal on target machine
cat readme
```

| Username | Password |
| :--- | :--- |
| bandit19 | IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x |

```bash
ls -la
./bandit20-do
./bandit20-do cat /etc/bandit_pass/bandit20
```

| Username | Password |
| :--- | :--- |
| bandit20 | GbKksEFF4yrVs6il55v6gwY5aVje5f0j |

```bash
echo 'GbKksEFF4yrVs6il55v6gwY5aVje5f0j' | nc -l -p 1234 &	# send password to server port 1234 (-l is listen mode)
./suconnect 1234	# conect to our netcat server
```

# Level 21-26

> topic: cron jobs & shell script

| Username | Password |
| :--- | :--- |
| bandit21 | gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr |

```bash
ls /etc/cron.d
cat /etc/cron.d/cronjob_bandit22
cat /usr/bin/cronjob_bandit22.sh
cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

| Username | Password |
| :--- | :--- |
| bandit22 | Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI |

```bash
ls /etc/cron.d
cat /etc/cron.d/cronjob_bandit23
cat /usr/bin/cronjob_bandit23.sh
echo I am user bandit23 | md5sum | cut -d ' ' -f 1	# use hash to file mytarget
cat /tmp/8ca319486bfbbc3663ea0fbe81326349
```

| Username | Password |
| :--- | :--- |
| bandit23 | jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n |

```bash
ls /etc/cron.d
cat /etc/cron.d/cronjob_bandit24
cat /usr/bin/cronjob_bandit24.sh
mkdir /tmp/hello23
cd /tmp/hello23
echo "#!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/hello23/password" > level23.sh	# bandit 24 will run this file each 60s
chmod 777 level23.sh
touch password
chmod 777 password
cp level23.sh /var/spool/bandit24
# wait 1 min for cron job run
ls -la
cat password
```

| Username | Password |
| :--- | :--- |
| bandit24 | UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ |

```bash
nc localhost 30002	# connect to port 30002
mkdir /tmp/hello24
cd /tmp/hello24
vi level24.sh
```
```
#!/bin/bash

for i in {0000..9999};

do

    echo "UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ $i"
    
done | nc localhost 30002"
```
```bash
bash level24.sh
```

| Username | Password |
| :--- | :--- |
| bandit25 | uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG |

```bash
ls
ssh -i bandit26.sshkey bandit26@localhost
cat /etc/passwd
```
```
bandit0:x:11000:11000:bandit level 0:/home/bandit0:/bin/bash
bandit1:x:11001:11001:bandit level 1:/home/bandit1:/bin/bash
bandit10:x:11010:11010:bandit level 10:/home/bandit10:/bin/bash
bandit11:x:11011:11011:bandit level 11:/home/bandit11:/bin/bash
bandit12:x:11012:11012:bandit level 12:/home/bandit12:/bin/bash
bandit13:x:11013:11013:bandit level 13:/home/bandit13:/bin/bash
bandit14:x:11014:11014:bandit level 14:/home/bandit14:/bin/bash
bandit15:x:11015:11015:bandit level 15:/home/bandit15:/bin/bash
bandit16:x:11016:11016:bandit level 16:/home/bandit16:/bin/bash
bandit17:x:11017:11017:bandit level 17:/home/bandit17:/bin/bash
bandit18:x:11018:11018:bandit level 18:/home/bandit18:/bin/bash
bandit19:x:11019:11019:bandit level 19:/home/bandit19:/bin/bash
bandit2:x:11002:11002:bandit level 2:/home/bandit2:/bin/bash
bandit20:x:11020:11020:bandit level 20:/home/bandit20:/bin/bash
bandit21:x:11021:11021:bandit level 21:/home/bandit21:/bin/bash
bandit22:x:11022:11022:bandit level 22:/home/bandit22:/bin/bash
bandit23:x:11023:11023:bandit level 23:/home/bandit23:/bin/bash
bandit24:x:11024:11024:bandit level 24:/home/bandit24:/bin/bash
bandit25:x:11025:11025:bandit level 25:/home/bandit25:/bin/bash
bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext
bandit27:x:11027:11027:bandit level 27:/home/bandit27:/bin/bash
bandit28:x:11028:11028:bandit level 28:/home/bandit28:/bin/bash
bandit29:x:11029:11029:bandit level 29:/home/bandit29:/bin/bash
bandit3:x:11003:11003:bandit level 3:/home/bandit3:/bin/bash
bandit30:x:11030:11030:bandit level 30:/home/bandit30:/bin/bash
bandit31:x:11031:11031:bandit level 31:/home/bandit31:/bin/bash
bandit32:x:11032:11032:bandit level 32:/home/bandit32:/home/bandit32/uppershell
bandit33:x:11033:11033:bandit level 33:/home/bandit33:/bin/bash
bandit4:x:11004:11004:bandit level 4:/home/bandit4:/bin/bash
bandit5:x:11005:11005:bandit level 5:/home/bandit5:/bin/bash
bandit6:x:11006:11006:bandit level 6:/home/bandit6:/bin/bash
bandit7:x:11007:11007:bandit level 7:/home/bandit7:/bin/bash
bandit8:x:11008:11008:bandit level 8:/home/bandit8:/bin/bash
bandit9:x:11009:11009:bandit level 9:/home/bandit9:/bin/bash
bandit27-git:x:11527:11527::/home/bandit27-git:/usr/bin/git-shell
bandit28-git:x:11528:11528::/home/bandit28-git:/usr/bin/git-shell
bandit29-git:x:11529:11529::/home/bandit29-git:/usr/bin/git-shell
bandit30-git:x:11530:11530::/home/bandit30-git:/usr/bin/git-shell
bandit31-git:x:11531:11531::/home/bandit31-git:/usr/bin/git-shell
```
```bash
cat /usr/bin/showtext
? resize terminal to use more mode on linux ?
ssh -i bandit26.sshkey bandit26@localhost	# enterd more mode
v	# open vim
```
```
:set shell=/bin/bash
:shell
```
```bash
cat /etc/bandit_pass/bandit26
```

| Username | Password |
| :--- | :--- |
| bandit26 | 5czgV9L3Xx8JPOyRbXh6lQbmIOWvPT6Z |

```bash
# login in more mode
v	# open vim
:set shell=/bin/bash
:shell
ls
cat text.txt
./bandit27-do
./bandit27-do cat /etc/bandit_pass/bandit27
```

## Level 27-31

> topic: git

| Username | Password |
| :--- | :--- |
| bandit27 | 3ba3118a22e93127a4ed485be72ef5ea |

```bash
mkdir /tmp/hello27
cd /tmp/hello27
git clone ssh://bandit27-git@localhost/home/bandit27-git/repo
3ba3118a22e93127a4ed485be72ef5ea    # type password and enter
cd repo
ls
cat README
```

| Username | Password |
| :--- | :--- |
| bandit28 | 0ef186ac70e04ea33b4c1853d2526fa2 |

```bash
mkdir /tmp/hello28
cd /tmp/hello28
git clone ssh://bandit28-git@localhost/home/bandit28-git/repo
0ef186ac70e04ea33b4c1853d2526fa2    # type password and enter
cd repo
ls
cat README.md
git log
git diff c086d11a00c0648d095d04c089786efef5e01264
```

| Username | Password |
| :--- | :--- |
| bandit29 | bbc96594b4e001778eee9975372716b2 |

```bash
mkdir /tmp/hello29
cd /tmp/hello29
git clone ssh://bandit29-git@localhost/home/bandit29-git/repo
bbc96594b4e001778eee9975372716b2    # type password and enter
cd repo
ls
cat README.md
git log
git branch -a
git diff remotes/origin/dev
git diff ...	# try to find other useful info
```

| Username | Password |
| :--- | :--- |
| bandit30 | 5b90576bedb2cc04c86a9e924ce42faf |

```bash
mkdir /tmp/hello30
cd /tmp/hello30
git clone ssh://bandit30-git@localhost/home/bandit30-git/repo
5b90576bedb2cc04c86a9e924ce42faf    # type password and enter
cd repo
ls
cat README.md
git log
git branch -a
git diff ...	# try to find other useful info
ls -la
cd .git
cat packed-refs
ls refs
ls refs/tags
ls -la refs/tags
git tag
git show secret
```

| Username | Password |
| :--- | :--- |
| bandit31 | 47e603bb428404d265f59c42920d81e5 |

```bash
mkdir /tmp/hello31
cd /tmp/hello31
git clone ssh://bandit31-git@localhost/home/bandit31-git/repo
47e603bb428404d265f59c42920d81e5    # type password and enter
cd repo
ls
cat README.md
ls -la
cat .gitignore
rm .gitignore
echo 'May I come in?' > key.txt
git add .
git commit -m "hello"
git push
47e603bb428404d265f59c42920d81e5    # type password and enter
```

## Level 32-33

> topic: other

| Username | Password |
| :--- | :--- |
| bandit32 | 56a9bf19c63d650ce78e6ec0354ee45e |

```bash
# all convert to uppercase but can use $ to see variable
Ctrl+C    # return bandit31
ls -la /home/bandit32/
# login again
$0	# name of script (run it)
ls -la
cat /etc/bandit_pass/bandit33
```

| Username | Password |
| :--- | :--- |
| bandit33 | c9c3199ddf4121b10cf581a98d51caee |

```bash
ls
cat README.txt
```
```
Congratulations on solving the last level of this game!

At this moment, there are no more levels to play in this game. However, we are constantly working
on new levels and will most likely expand this game with more levels soon.
Keep an eye out for an announcement on our usual communication channels!
In the meantime, you could play some of our other wargames.

If you have an idea for an awesome new level, please let us know!
```

This is last level for now

**^^ finished ^^ thank you ^^**

## Author

+ [Facebook](https://www.facebook.com/profile.php?id=100045406261491)
+ [Github](https://github.com/lucthienphong1120)
