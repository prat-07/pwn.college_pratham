# Comprehending Commands

## cat: not the pet, but the command
The flag is copied to the `flag` file in the home directory. Read it with cat.

### Solve
**Flag:** `pwn.college{AuoiR2xV_iZabjZNBpHtWcmhh6Z.QXxcTN0wyNyAzNzEzW}`\
Simply execute the `cat` command with the `flag` argument.
```
hacker@commands~cat-not-the-pet-but-the-command:~$ cat flag
pwn.college{AuoiR2xV_iZabjZNBpHtWcmhh6Z.QXxcTN0wyNyAzNzEzW}
```


## catting absolute paths
Read the flag file using `cat` at its absolute path : `/flag`.
### Solve
**Flag:** `pwn.college{gRtYap99BffeogxlnG2vFL0jELV.QX5ETO0wyNyAzNzEzW`
```
hacker@commands~catting-absolute-paths:~$ cat /flag
pwn.college{gRtYap99BffeogxlnG2vFL0jELV.QX5ETO0wyNyAzNzEzW}
```


## more catting practice
Retrive the flag with the `cat` command without changing directories.
### Solve
**Flag:** `pwn.college{MTOYQENET8_7eERtBm8ISelZqCC.QXwITO0wyNyAzNzEzW}`\
Pass the absolute path mentioned as an argument to the `cat` command.
```
You cannot use the 'cd' command in this level, and must retrieve the flag by 
absolute path. Plus, I hid the flag in a different directory! You can find it 
in the file /usr/include/capstone/flag. Go cat it out **without** cding into 
that directory!
hacker@commands~more-catting-practice:~$ cat /usr/include/capstone/flag
pwn.college{MTOYQENET8_7eERtBm8ISelZqCC.QXwITO0wyNyAzNzEzW}
```


## grepping for a needle in a haystack
`grep` the `data.txt` file in the `/challenge` directory to find the flag.
### Solve
**Flag:** `pwn.college{khHHKRUu8X7NY3rjqDI436vLYrn.QX3EDO0wyNyAzNzEzW}`\
Since the flag is in the format `pwn.college{random-string}`, pass `pwn.college` as an argument to the `grep` command with the absolute file path.
```
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep pwn.college /challenge/data.txt
pwn.college{khHHKRUu8X7NY3rjqDI436vLYrn.QX3EDO0wyNyAzNzEzW}
```


## comparing files
There are two files in `/challenge` directory:
- `/challenge/decoys_only.txt` contains 100 fake flags
- `/challenge/decoys_and_real.txt` contains all 100 fake flags plus the one real flag.

Use diff to find the flag.
### Solve
**Flag:** `pwn.college{Auzpwvp7rXM9iTdQfL82HV6CJ6P.01MwMDOxwyNyAzNzEzW}`
```
hacker@commands~comparing-files:~$ diff /challenge/decoys_only.txt /challenge/decoys_and_real.txt 
24a25
> pwn.college{Auzpwvp7rXM9iTdQfL82HV6CJ6P.01MwMDOxwyNyAzNzEzW}
```


## listing files
List the files in `/challenge` to find the `/challenge/run` file. It is given a random name.
### Solve
**Flag:** `pwn.college{khBzU_U875SoyrWULWC-hYIolBy.QX4IDO0wyNyAzNzEzW}`\
Use the `ls` command to list the files. Since a markdown file cannot be run, run the other file.
```
hacker@commands~listing-files:~$ ls /challenge
4499-renamed-run-19904  DESCRIPTION.md
hacker@commands~listing-files:~$ /challenge/4499-renamed-run-19904 
Yahaha, you found me! Here is your flag:
pwn.college{khBzU_U875SoyrWULWC-hYIolBy.QX4IDO0wyNyAzNzEzW}
```


## touching files
Create two files: `/tmp/pwn` and `/tmp/college`, and run `/challenge/run` to get the flag!
## Solve
**Flag:** `pwn.college{o5jBQM_jV6jBHYwlB9ikKaH4e8d.QXwMDO0wyNyAzNzEzW}`
```
hacker@commands~touching-files:~$ touch /tmp/pwn /tmp/college
hacker@commands~touching-files:~$ /challenge/run 
Success! Here is your flag:
pwn.college{o5jBQM_jV6jBHYwlB9ikKaH4e8d.QXwMDO0wyNyAzNzEzW}
```


## removing files
Delete the `delete_me` file in the home dir and run `/challenge/check` command.
### Solve
**Flag:** `pwn.college{QYgKkGV4TzBudhmAO6dq03EX5jI.QX2kDM1wyNyAzNzEzW}`
```
hacker@commands~removing-files:~$ rm delete_me 
hacker@commands~removing-files:~$ /challenge/check 
Excellent removal. Here is your reward:
pwn.college{QYgKkGV4TzBudhmAO6dq03EX5jI.QX2kDM1wyNyAzNzEzW}
```


## moving files
Move the `/flag` file into `/tmp/hack-the-planet`. When done, run `/challenge/check` command to get the flag.
### Solve
**Flag:** `pwn.college{QEhPOeVkQoAQgLWemKciAkfn-FX.0VOxEzNxwyNyAzNzEzW}`\
One thing to keep in mind. `mv` command is also used to rename a file. So, what the specified command does is move the `flag` file in the `/` directory into `/tmp` directory with the new name `hack-the-planet`.
```
hacker@commands~moving-files:~$ mv /flag /tmp/hack-the-planet
Correct! Performing 'mv /flag /tmp/hack-the-planet'.
hacker@commands~moving-files:~$ /challenge/check
Congrats! You successfully moved the flag to /tmp/hack-the-planet! Here it is:
pwn.college{QEhPOeVkQoAQgLWemKciAkfn-FX.0VOxEzNxwyNyAzNzEzW}
```


## hidden files
Find the flag, hidden as a dot-prepended file in `/`.
### Solve
**Flag:** `pwn.college{8vwGtFgq0BYtvmZMHSAHeiV1-6x.QXwUDO0wyNyAzNzEzW}`\
Since files prepended with `.` cannot be run as a command we need to `cat` its contents.
```
hacker@commands~hidden-files:~$ cd /
hacker@commands~hidden-files:/$ ls -a
.   .dockerenv            bin   challenge  etc   lib    lib64   media  nix  proc  run   srv  tmp  var
..  .flag-55152328624153  boot  dev        home  lib32  libx32  mnt    opt  root  sbin  sys  usr
hacker@commands~hidden-files:/$ cat .flag-55152328624153 
pwn.college{8vwGtFgq0BYtvmZMHSAHeiV1-6x.QXwUDO0wyNyAzNzEzW}
```


## An Epic Filesystem Quest
The `flag` file is hidden. Make use of `ls` and `cat` command and follow the leads provided.

- Your first clue is in `/`. Head on over there.
- Look around with ls. There'll be a file named HINT or CLUE or something along those lines!
- `cat` that file to read the clue!
- Depending on what the clue says, head on over to the next directory (or don't!).
- Follow the clues to the flag!
### Solve
**Flag:** `pwn.college{sFWJgYIaBI95vOMLXNh2UIdIzDj.QX5IDO0wyNyAzNzEzW}`\
As mentioned, I just followed the steps. A quick note, I did not `cd` into every directory. I just used the `ls` command on the path provided and used the `cat` command with the filename appended to the path to read the contents of the file. I did not `cd` into the directory unless mentioned otherwise.
```
hacker@commands~an-epic-filesystem-quest:~$ cd /
hacker@commands~an-epic-filesystem-quest:/$ ls
WHISPER  boot       dev  flag  lib    lib64   media  nix  proc  run   srv  tmp  var
bin      challenge  etc  home  lib32  libx32  mnt    opt  root  sbin  sys  usr
hacker@commands~an-epic-filesystem-quest:/$ cat WHISPER 
Great sleuthing!
The next clue is in: /opt/linux/linux-5.4/arch/powerpc/perf
hacker@commands~an-epic-filesystem-quest:/$ ls /opt/linux/linux-5.4/arch/powerpc/perf
8xx-pmu.c    core-book3s.c         hv-24x7-catalog.h  hv-common.h         internal.h       power5+-pmu.c         power8-events-list.h  req-gen
Makefile     core-fsl-emb.c        hv-24x7-domains.h  hv-gpci-requests.h  isa207-common.c  power5-pmu.c          power8-pmu.c
TEASER       e500-pmu.c            hv-24x7.c          hv-gpci.c           isa207-common.h  power6-pmu.c          power9-events-list.h
bhrb.S       e6500-pmu.c           hv-24x7.h          hv-gpci.h           mpc7450-pmu.c    power7-events-list.h  power9-pmu.c
callchain.c  generic-compat-pmu.c  hv-common.c        imc-pmu.c           perf_regs.c      power7-pmu.c          ppc970-pmu.c
hacker@commands~an-epic-filesystem-quest:/$ cat /opt/linux/linux-5.4/arch/powerpc/perf/TEASER 
Lucky listing!
The next clue is in: /opt/linux/linux-5.4/Documentation/devicetree/bindings/soc/dove

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:/$ ls -a /opt/linux/linux-5.4/Documentation/devicetree/bindings/soc/dove
.  ..  .BRIEF  pmu.txt
hacker@commands~an-epic-filesystem-quest:/$ ls -a /opt/linux/linux-5.4/Documentation/devicetree/bindings/soc/dove/.BRIEF 
/opt/linux/linux-5.4/Documentation/devicetree/bindings/soc/dove/.BRIEF
hacker@commands~an-epic-filesystem-quest:/$ cat /opt/linux/linux-5.4/Documentation/devicetree/bindings/soc/dove/.BRIEF 
Congratulations, you found the clue!
The next clue is in: /opt/linux/linux-5.4/include/config/have/acpi

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/$ cd /opt/linux/linux-5.4/include/config/have/acpi
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/include/config/have/acpi$ ls
NUGGET  apei  apei.h
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/include/config/have/acpi$ cat NUGGET 
Lucky listing!
The next clue is in: /usr/share/sphinx/themes/nonav

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/include/config/have/acpi$ cd /usr/share/sphinx/themes/nonav
hacker@commands~an-epic-filesystem-quest:/usr/share/sphinx/themes/nonav$ ls
INSIGHT  layout.html  static  theme.conf
hacker@commands~an-epic-filesystem-quest:/usr/share/sphinx/themes/nonav$ cat INSIGHT 
Yahaha, you found me!
The next clue is in: /usr/share/perl/5.30.0/Test

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:/usr/share/sphinx/themes/nonav$ ls -a /usr/share/perl/5.30.0/Test
.  ..  .MEMO  Builder  Builder.pm  Harness.pm  More.pm  Simple.pm  Tester  Tester.pm  Tutorial.pod  use
hacker@commands~an-epic-filesystem-quest:/usr/share/sphinx/themes/nonav$ cat /usr/share/perl/5.30.0/Test/.MEMO
Tubular find!
The next clue is in: /opt/pwndbg/.venv/lib/python3.8/site-packages/pwn/__pycache__

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:/usr/share/sphinx/themes/nonav$ ls -a /opt/pwndbg/.venv/lib/python3.8/site-packages/pwn/__pycache__
.  ..  .TIP  __init__.cpython-38.pyc  toplevel.cpython-38.pyc
hacker@commands~an-epic-filesystem-quest:/usr/share/sphinx/themes/nonav$ cat /opt/pwndbg/.venv/lib/python3.8/site-packages/pwn/__pycache__/.TIP 
Tubular find!
The next clue is in: /opt/linux/linux-5.4/arch/arm/kvm/hyp
hacker@commands~an-epic-filesystem-quest:/usr/share/sphinx/themes/nonav$ ls /opt/linux/linux-5.4/arch/arm/kvm/hyp
BLUEPRINT  Makefile  banked-sr.c  cp15-sr.c  entry.S  hyp-entry.S  s2-setup.c  switch.c  tlb.c  vfp.S
hacker@commands~an-epic-filesystem-quest:/usr/share/sphinx/themes/nonav$ cat /opt/linux/linux-5.4/arch/arm/kvm/hyp/BLUEPRINT 
Congratulations, you found the clue!
The next clue is in: /usr/local/lib/python3.8/dist-packages/websocket

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/usr/share/sphinx/themes/nonav$ ls /usr/local/lib/python3.8/dist-packages/websocket
DOSSIER-TRAPPED  __pycache__  _app.py        _core.py        _handshake.py  _logging.py  _ssl_compat.py  _utils.py   py.typed
__init__.py      _abnf.py     _cookiejar.py  _exceptions.py  _http.py       _socket.py   _url.py         _wsdump.py  tests
hacker@commands~an-epic-filesystem-quest:/usr/share/sphinx/themes/nonav$ cat /usr/local/lib/python3.8/dist-packages/websocket/DOSSIER-TRAPPED 
CONGRATULATIONS! Your perserverence has paid off, and you have found the flag!
It is: pwn.college{sFWJgYIaBI95vOMLXNh2UIdIzDj.QX5IDO0wyNyAzNzEzW}
```


## making directories
Create a `/tmp/pwn` directory and make a `college` file in it. Then run `/challenge/check` command to get the flag.
### Solve
**Flag:** `pwn.college{c-pRgbaTuhK5R5if1AEoomN4gTB.QXxMDO0wyNyAzNzEzW}`\
I directly passed the path of the file to be created as an argument to the `touch` command rather that first `cd`ing into it and then creating the file.
```
hacker@commands~making-directories:~$ mkdir /tmp/pwn
hacker@commands~making-directories:~$ touch /tmp/pwn/college
hacker@commands~making-directories:~$ /challenge/run
Success! Here is your flag:
pwn.college{c-pRgbaTuhK5R5if1AEoomN4gTB.QXxMDO0wyNyAzNzEzW}
```


## finding files
The `flag` file is hidden in a random directory on the filesystem.
### Solve
**Flag:** `pwn.college{oRnmhDMpcqQGbMtLHMUdIPAEq9U.QXyMDO0wyNyAzNzEzW}`\
Things to keep in mind while using `find`:
- The format is : `find <criterea-folder> -name(if want to search a specific filename) <filename>`
- `find` command can take a while.
- More files on the system with same name but stored in the folder where non-root user is not allowed - hence the `permission denied`.
- `cat` each result patiently.
```
hacker@commands~finding-files:~$ find -name flag
hacker@commands~finding-files:~$ find / -name flag
find: ‘/root’: Permission denied
find: ‘/proc/1/task/1/fd’: Permission denied
find: ‘/proc/1/task/1/fdinfo’: Permission denied
find: ‘/proc/1/task/1/ns’: Permission denied
find: ‘/proc/1/fd’: Permission denied
find: ‘/proc/1/map_files’: Permission denied
find: ‘/proc/1/fdinfo’: Permission denied
find: ‘/proc/1/ns’: Permission denied
find: ‘/proc/7/task/7/fd’: Permission denied
find: ‘/proc/7/task/7/fdinfo’: Permission denied
find: ‘/proc/7/task/7/ns’: Permission denied
find: ‘/proc/7/fd’: Permission denied
find: ‘/proc/7/map_files’: Permission denied
find: ‘/proc/7/fdinfo’: Permission denied
find: ‘/proc/7/ns’: Permission denied
find: ‘/var/log/private’: Permission denied
find: ‘/var/log/apache2’: Permission denied
find: ‘/var/log/mysql’: Permission denied
find: ‘/var/cache/ldconfig’: Permission denied
find: ‘/var/cache/apt/archives/partial’: Permission denied
find: ‘/var/cache/private’: Permission denied
find: ‘/var/lib/apt/lists/partial’: Permission denied
find: ‘/var/lib/php/sessions’: Permission denied
find: ‘/var/lib/mysql-files’: Permission denied
find: ‘/var/lib/private’: Permission denied
find: ‘/var/lib/mysql-keyring’: Permission denied
find: ‘/var/lib/mysql’: Permission denied
find: ‘/tmp/tmp.TpSOPGOVKK’: Permission denied
find: ‘/run/mysqld’: Permission denied
find: ‘/run/sudo’: Permission denied
find: ‘/etc/ssl/private’: Permission denied
/usr/local/lib/python3.8/dist-packages/pwnlib/flag
/usr/share/icons/Humanity/mimes/64/flag
/opt/pwndbg/.venv/lib/python3.8/site-packages/pwnlib/flag
/nix/store/7ns27apnvn4qj4q5c82x0z1lzixrz47p-radare2-5.9.8/share/radare2/5.9.8/flag
/nix/store/5z3sjp9r463i3siif58hq5wj5jmy5m98-python3.12-pwntools-4.13.1/lib/python3.12/site-packages/pwnlib/flag
/nix/store/5n5lp1m8gilgrsriv1f2z0jdjk50ypcn-rizin-0.7.3/share/rizin/flag
/nix/store/bnlabj2vsbljhp597ir29l51nrqhm89w-rizin-0.7.4/share/rizin/flag
/nix/store/s8b49lb0pqwvw0c6kgjbxdwxcv2bp0x4-radare2-5.9.8/share/radare2/5.9.8/flag
/nix/store/1hyxipvwpdpcxw90l5pq1nvd6s6jdi5m-python3.12-pwntools-4.14.1/lib/python3.12/site-packages/pwnlib/flag
/nix/store/h88mxp2mbgyj06vypwmqpy05idhwimnp-python3.13-pwntools-4.14.1/lib/python3.13/site-packages/pwnlib/flag
/nix/store/5qz6hgb1qzpvjrsw20wyiylx5zw8b9bk-pwntools-4.14.0/lib/python3.13/site-packages/pwnlib/flag
hacker@commands~finding-files:~$ /usr/local/lib/python3.8/dist-packages/pwnlib/flag
bash: /usr/local/lib/python3.8/dist-packages/pwnlib/flag: Is a directory
hacker@commands~finding-files:~$ cat /usr/local/lib/python3.8/dist-packages/pwnlib/flag
cat: /usr/local/lib/python3.8/dist-packages/pwnlib/flag: Is a directory
hacker@commands~finding-files:~$ /usr/local/lib/python3.8/dist-packages/pwnlib/flag
bash: /usr/local/lib/python3.8/dist-packages/pwnlib/flag: Is a directory
hacker@commands~finding-files:~$ cat /usr/share/icons/Humanity/mimes/64/flag
pwn.college{oRnmhDMpcqQGbMtLHMUdIPAEq9U.QXyMDO0wyNyAzNzEzW}
```


## linking files
The flag is as always in `/flag`, but it only accessible to the root user. Also, `/challenge/catflag` will read out the `/home/hacker/not-the-flag` file. Use symbolic link to trick it into giving you the password.
### Solve
**Flag:** `pwn.college{wLHh9RNYNF5SljJFbevkZa4HMra.QX5ETN1wyNyAzNzEzW}`\
Since `/flag` file cannot be run directly and `/challenge/catflag` will read out the `/home/hacker/not-the-flag` file (which does not exist yet), we can create a link named `not-the-flag` in the `/home/hacker` directory and link it to `/flag`. Then if we run the `/challenge/catflag` command, it should read out the `not-the-flag` file bypassing the root permissions.
```
hacker@commands~linking-files:~$ ln -s /flag /home/hacker/not-the-flag
hacker@commands~linking-files:~$ /challenge/catflag 
About to read out the /home/hacker/not-the-flag file!
pwn.college{wLHh9RNYNF5SljJFbevkZa4HMra.QX5ETN1wyNyAzNzEzW}
```


### New Learnings
***What are links?***
*Links are files referencing to other files. They are of 2 types - symbolic/soft links and hard links. They are created using the command: `ln path/to/org/file path/to/link/file`. They can contain **relative** as well as **absolute** paths. They can also point to a directory. (Everything in linux is a file - even a directory.)*

**Soft Links**
- Uses the `-s` flag.
- Analogous to a *shortcut* in Windows.

**Hard Links**
- Uses no flag.
- An actual copy of the original file. Even contains the same *inode*.


### References
[Hard vs Soft Links in Linux by Ahmed Alkabary](https://youtu.be/4-vye3QFTFo?si=SwBKcu-P3gXF8e69)
