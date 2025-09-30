# Untangling Users

## Becoming root with su
In this challenge, switch to `root` user and provide the root password `hack-the-planet` and gain the root priviledges to get the flag.
### Solve
**Flag:** `pwn.college{A8huuM6-TkiasHcikDJ0p8Bhcys.QX1UDN1wyNyAzNzEzW}`
- Run the `ls` command to see all the files.
- `cat` the `not-the-flag` link.
- Permission denied
- Switch user to `root` using the `su` command.
- Write the password `hack-the-planet`.

```
hacker@users~becoming-root-with-su:~$ ls
 COLLEGE   Desktop   PWN   a   instructions   msg   myflag   not-the-flag   processes   the-flag  '~'
hacker@users~becoming-root-with-su:~$ cat not-the-flag 
cat: not-the-flag: Permission denied
hacker@users~becoming-root-with-su:~$ su
Password: 
root@users~becoming-root-with-su:/home/hacker# cat not-the-flag 
pwn.college{A8huuM6-TkiasHcikDJ0p8Bhcys.QX1UDN1wyNyAzNzEzW}
```


## Other users with su
In this level, you must switch to the `zardus` user and then run `/challenge/run.` Zardus' password is `dont-hack-me`.
### Solve
**Flag:** `pwn.college{UrwI13hWfGZFPNDcvTihvR_q-ke.QX2UDN1wyNyAzNzEzW}`
```
hacker@users~other-users-with-su:~$ /challenge/run
You are the hacker user... You MUST become the zardus user before executing 
this command.
hacker@users~other-users-with-su:~$ su zardus
Password: 
zardus@users~other-users-with-su:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{UrwI13hWfGZFPNDcvTihvR_q-ke.QX2UDN1wyNyAzNzEzW}
```


## Cracking passwords
This level simulates this story, giving you a leak of `/etc/shadow` (in `/challenge/shadow-leak`). Crack it (this could take a few minutes), `su` to `zardus`, and run `/challenge/run` to get the flag!
### Solve
**Flag:** `pwn.college{sFiHGOSN196jN2uPAI1aH4XJVM3.QX3UDN1wyNyAzNzEzW}`
- Run the `john` command on `/challenge/shadow-leak` file.
- Using this, I acquired `zardus`' password.
- `su` into `zardus` using the password acquired.
- run `/challenge/run` to get the flag.
```
hacker@users~cracking-passwords:~$ john /challenge/shadow-leak
Created directory: /home/hacker/.john
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Press 'q' or Ctrl-C to abort, almost any other key for status
0g 0:00:00:06 69% 1/3 0g/s 283.7p/s 283.7c/s 283.7C/s Z99999E..1z999991
aardvark         (zardus)
1g 0:00:00:20 100% 2/3 0.04852g/s 282.5p/s 282.5c/s 282.5C/s Johnson..buzz
Use the "--show" option to display all of the cracked passwords reliably
Session completed
hacker@users~cracking-passwords:~$ su zardus
Password: 
zardus@users~cracking-passwords:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{sFiHGOSN196jN2uPAI1aH4XJVM3.QX3UDN1wyNyAzNzEzW}
```


## Using sudo
In this level, we will give you `sudo` access, and you will use it to read the flag.
### Solve
**Flag:** `pwn.college{QgeD6EpeqCEIKZ5Ed9Hs4Ap48sc.QX4UDN1wyNyAzNzEzW}`
- `ls` in long format in the current dir.
- Saw the `not-the-flag` link.
- Tried to `cat` it.
- Permission denied.
- Run the last command again but with `sudo`.
```
hacker@users~using-sudo:~$ ls -l
total 40
-rw-r--r-- 1 hacker hacker    4 Sep 25 15:21  COLLEGE
drwxr-xr-x 1 hacker hacker    0 Sep 21 16:55  Desktop
-rw-r--r-- 1 hacker hacker    8 Sep 25 17:11  PWN
-rw-r--r-- 1 root   hacker   60 Sep 22 05:20  a
-rw-r--r-- 1 hacker hacker  829 Sep 25 17:06  instructions
-rw-r--r-- 1 root   hacker   77 Sep 25 17:54  msg
-rw-r--r-- 1 hacker hacker   95 Sep 25 17:06  myflag
lrwxrwxrwx 1 hacker hacker    5 Sep 23 13:57  not-the-flag -> /flag
-rw-r--r-- 1 hacker hacker 2313 Sep 27 05:15  processes
-rw-r--r-- 1 hacker hacker  437 Sep 25 15:52  the-flag
-rw-r--r-- 1 root   hacker   60 Sep 22 16:40 '~'
hacker@users~using-sudo:~$ cat not-the-flag 
cat: not-the-flag: Permission denied
hacker@users~using-sudo:~$ sudo cat not-the-flag 
pwn.college{QgeD6EpeqCEIKZ5Ed9Hs4Ap48sc.QX4UDN1wyNyAzNzEzW}
```



### New Learnings
- `sudo` vs `su`
    - `su` (substitute user): Switches current shell to another user(default: root). Once entered target user's password, all commands run as that user until exited.
    - `sudo` (superuser do): Runs a single command with elevated privileges. Get temp root powers. You enter your own password if you're in the `sudoers` list.

- Comparing passwords
    - Earlier passwords were stored in `/etc/passwd` but it was globally readable.
    - Later switched to `/etc/shadow`.
    - Format : `username : # password_encrypted_by_hash`
        - `#` can be either:
            1. `*` or `!` which means password login for that account is disabled.
            2. *`blank`* means no password.

- `john` command
    - *john the ripper* command.
    - Converts the hash back into normal string.
    - Can be used to crack passwords since they are stored as hashes as mentioned previously.
