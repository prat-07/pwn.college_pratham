# Perceiving Permissions

## Changing File Ownership
In this level, we will practice changing the owner of the `/flag` file to the hacker user, and then read the flag. For this challenge only, I made it so that you can use `chown` to your heart's content as the hacker user (again, typically, this requires you to be root).
### Solve
**Flag:** `pwn.college{UOBTgdJnFr57Lu9KQue1-7ckzeD.QXxEjN0wyNyAzNzEzW}`
- Try to `cat` `/flag` file.
- Permission denied.
- Change ownership of the file to `hacker`.
- Run command again.
```bash
hacker@permissions~changing-file-ownership:~$ cat /flag
cat: /flag: Permission denied
hacker@permissions~changing-file-ownership:~$ chown hacker /flag
hacker@permissions~changing-file-ownership:~$ cat /flag
pwn.college{UOBTgdJnFr57Lu9KQue1-7ckzeD.QXxEjN0wyNyAzNzEzW}
```

## Groups and Files
In this level, I have made the flag readable by whatever group owns it, but this group is currently `root`. Luckily, I have also made it possible for you to invoke `chgrp` as the `hacker` user! Change the group ownership of the flag file, and read the flag!
### Solve
**Flag:** `pwn.college{Ma8iEG_cGR4WBrUD0R6VSfdVWbR.QXxcjM1wyNyAzNzEzW}`
- `ls` `/flag` permissions.
- Change its group `hacker`.
- `cat` it.
```bash
hacker@permissions~groups-and-files:~$ ls
 COLLEGE   Desktop   PWN   a   instructions   msg   myflag   not-the-flag   processes   the-flag  '~'
hacker@permissions~groups-and-files:~$ ls -l /flag
-r--r----- 1 root root 60 Sep 28 06:54 /flag
hacker@permissions~groups-and-files:~$ chgrp hacker /flag
hacker@permissions~groups-and-files:~$ cat /flag
pwn.college{Ma8iEG_cGR4WBrUD0R6VSfdVWbR.QXxcjM1wyNyAzNzEzW}
```


## Fun With Group Names
In this challenge, the my group name has been randomized. Use the `id` command to figure out the group name and change group of `/flag` file to that group.
**Flag:** `pwn.college{0EM1IJrDzkVKWDtSUceqPMgqnQ9.QXycjM1wyNyAzNzEzW}`
```bash
hacker@permissions~fun-with-groups-names:~$ ls -l /flag
-r--r----- 1 root root 60 Sep 28 07:01 /flag
hacker@permissions~fun-with-groups-names:~$ id
uid=1000(hacker) gid=1000(grp2359) groups=1000(grp2359)
hacker@permissions~fun-with-groups-names:~$ chgrp grp2359 /flag
hacker@permissions~fun-with-groups-names:~$ cat /flag
pwn.college{0EM1IJrDzkVKWDtSUceqPMgqnQ9.QXycjM1wyNyAzNzEzW}
```

## Changing Permissions
In this challenge, you must change the permissions of the `/flag` file to read it! Typically, you need to have `write` access to the file in order to change its permissions, but I have made the `chmod` command all-powerful for this level, and you can `chmod` anything you want even though you are the hacker user. This is an ultimate power. The `/flag` file is owned by `root`, and you can't change that, but you can make it readable. Go and solve this!
### Solve
**Flag:** `pwn.college{w9UqP3mkl3lVuUOJPEfbrMG5swy.QXzcjM1wyNyAzNzEzW}`
- `ls -l /flag` to find which owner and group the file belongs to.
- Since it belong to root, I need `read` permission for the `other` groups.
```bash
hacker@permissions~changing-permissions:~$ ls -l /flag
-r-------- 1 root root 60 Sep 28 07:07 /flag
hacker@permissions~changing-permissions:~$ chmod o+r /flag
hacker@permissions~changing-permissions:~$ cat /flag
pwn.college{w9UqP3mkl3lVuUOJPEfbrMG5swy.QXzcjM1wyNyAzNzEzW}
```


## Executable Files
In this challenge, the `/challenge/run` program will give you the flag, but you must first make it executable!
### Solve
**Flag:** `pwn.college{ookHtM83aqtzuzu7ZArBWRS_nn5.QXyEjN0wyNyAzNzEzW}`
- View file permissions.
- Belongs to `hacker` user and group.
- Only giving executable permission to user will suffice.
- Execute the file.
```bash
hacker@permissions~executable-files:~$ ls -l /challenge/run
-r--r--r-- 1 hacker hacker 32 Jan 14  2025 /challenge/run
hacker@permissions~executable-files:~$ chmod u+x /challenge/run
hacker@permissions~executable-files:~$ /challenge/run
Successful execution! Here is your flag:
pwn.college{ookHtM83aqtzuzu7ZArBWRS_nn5.QXyEjN0wyNyAzNzEzW}
```


## Permission Tweaking Practice
This challenge will ask you to change the permissions of the `/challenge/pwn` file in specific ways a few times in a row. If you get the permissions wrong, the game will reset and you can try again. If you get the permissions right eight times in a row, the challenge will let you `chmod` `/flag` to make it readable for yourself :-) Launch `/challenge/run` to get started!
### Solve
**Flag:** `pwn.college{0e4eWtu3Z1YeEvPP4SMi-J4Z1PD.QXwEjN0wyNyAzNzEzW}`
```
hacker@permissions~permission-tweaking-practice:~$ /challenge/run
Round 1 of 8!

Current permissions of "/challenge/pwn": rw-r--r--
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": r--r--r--
* the user does have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod u-w /challenge/pwn
You set the correct permissions!
Round 2 of 8!

Current permissions of "/challenge/pwn": r--r--r--
* the user does have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": ---r-----
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod uo-r /challenge/pwn
You set the correct permissions!
Round 3 of 8!

Current permissions of "/challenge/pwn": ---r-----
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": ---------
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod g-r /challenge/pwn
You set the correct permissions!
Round 4 of 8!

Current permissions of "/challenge/pwn": ---------
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": --------x
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
* the world does have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod o+x /challenge/pwn
You set the correct permissions!
Round 5 of 8!

Current permissions of "/challenge/pwn": --------x
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": r-xr-xr-x
* the user does have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod a+rx /challenge/pwn
You set the correct permissions!
Round 6 of 8!

Current permissions of "/challenge/pwn": r-xr-xr-x
* the user does have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": r--r-xr-x
* the user does have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod u-x /challenge/pwn
You set the correct permissions!
Round 7 of 8!

Current permissions of "/challenge/pwn": r--r-xr-x
* the user does have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": rwxr-xrwx
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
* the world does have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod u=rwx,g=rx,o=rwx /challenge/pwn
You set the correct permissions!
Round 8 of 8!

Current permissions of "/challenge/pwn": rwxr-xrwx
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": -w-r-x-w-
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod u=w,g=rx,o=w /challenge/pwn
You set the correct permissions!
You've solved all 8 rounds! I have changed the ownership
of the /flag file so that you can 'chmod' it. You won't be able to read
it until you make it readable with chmod!

Current permissions of "/flag": ---------
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
hacker@permissions~permission-tweaking-practice:~$ ls -l /flag
---------- 1 hacker hacker 60 Sep 28 07:16 /flag
hacker@permissions~permission-tweaking-practice:~$ chmod u+r /flag
hacker@permissions~permission-tweaking-practice:~$ cat /flag
pwn.college{0e4eWtu3Z1YeEvPP4SMi-J4Z1PD.QXwEjN0wyNyAzNzEzW}
```


## Permissions Setting Practice
This level extends the previous level by requesting more radical permission changes, which you will need = and ,-chaining to achieve.
### Solve
**Flag:** `pwn.college{IQqOI5ZizF73XjuMZsR_MMycJTq.QXzETO0wyNyAzNzEzW}`
```
hacker@permissions~permissions-setting-practice:~$ /challenge/run
Round 1 of 8!

Current permissions of "/challenge/pwn": rw-r--r--
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rw-r-x---
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod u=rw,g=rx,o= /challenge/pwn
You set the correct permissions!
Round 2 of 8!

Current permissions of "/challenge/pwn": rw-r-x---
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": -w--wx-w-
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod u=w,g=wx,o=w /challenge/pwn
You set the correct permissions!
Round 3 of 8!

Current permissions of "/challenge/pwn": -w--wx-w-
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": -w---x-w-
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod u=w,g=x,o=w /challenge/pwn
You set the correct permissions!
Round 4 of 8!

Current permissions of "/challenge/pwn": -w---x-w-
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rwxrw--w-
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod u=rwx,g=rw,o=w /challenge/pwn
You set the correct permissions!
Round 5 of 8!

Current permissions of "/challenge/pwn": rwxrw--w-
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": -w-r-xrw-
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
- the world doesn't have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod u=w,g=rx,o=rw /challenge/pwn
You set the correct permissions!
Round 6 of 8!

Current permissions of "/challenge/pwn": -w-r-xrw-
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": r-x----w-
* the user does have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod u=rx,g=,o=w /challenge/pwn
You set the correct permissions!
Round 7 of 8!

Current permissions of "/challenge/pwn": r-x----w-
* the user does have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rw--wx--x
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
* the world does have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod u=rw,g=wx,o=x /challenge/pwn
You set the correct permissions!
Round 8 of 8!

Current permissions of "/challenge/pwn": rw--wx--x
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": -wx-wxr-x
- the user doesn't have read permissions
* the user does have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod u=wx,g=wx,o=rx /challenge/pwn
You set the correct permissions!
You've solved all 8 rounds! I have changed the ownership
of the /flag file so that you can 'chmod' it. You won't be able to read
it until you make it readable with chmod!

Current permissions of "/flag": ---------
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod a+r /flag
hacker@permissions~permissions-setting-practice:~$ cat /flag
pwn.college{IQqOI5ZizF73XjuMZsR_MMycJTq.QXzETO0wyNyAzNzEzW}
```


## The SUID Bit
Now, we are going to let you add the `SUID` bit to the `/challenge/getroot` program in order to spawn a root shell for you to `cat` the flag yourself!
### Solve
**Flag:** `pwn.college{QS50ExnToaedmW9nmbgjhkXVV5N.QXzEjN0wyNyAzNzEzW}`
- `cat`ting `/flag` file is not permitted.
- Add SUID bit to the `/challenge/getroot` file.
- This lets us execute it.
- Executing it opens a root terminal session.
- Allowing us to cat the `/flag` file and access it contents.
```bash
hacker@permissions~the-suid-bit:~$ cat /flag
cat: /flag: Permission denied
hacker@permissions~the-suid-bit:~$ chmod u+s /challenge/getroot
hacker@permissions~the-suid-bit:~$ /challenge/getroot 
SUCCESS! You have set the suid bit on this program, and it is running as root! 
Here is your shell...
root@permissions~the-suid-bit:~# cat /flag
pwn.college{QS50ExnToaedmW9nmbgjhkXVV5N.QXzEjN0wyNyAzNzEzW}
```


### New Learnings
- `Owners vs Groups`
    - *Owner* is the user who created the file.
    - *Group* is quite literally, the group of owners who can access the file.
        - A *group* contains multiple users.
        - A *user* can be a part of *multiple* groups as well.
        - Grouping users helps in managing **Access Control** efficiently.

- `Permissions`
    - `r` - read.
    - `w` - write.
    - `x` - execute.
    - `s` - stands for SUID bit. Execute but with owner's(usually root) privileges.


