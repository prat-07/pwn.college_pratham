# Pondering Paths

## The Root
Invoke the `pwn` program using the absolute path and capture the flag.
### Solve
**Flag:** `pwn.college{sTMkxizDOnV4Kro1P8Eik_y1K7Q.QX4cTO0wyNyAzNzEzW}`
Typed `/pwn` in the terminal since any path starting with `/` signifies an absolute path.
```
hacker@paths~the-root:~$ /pwn
BOOM!!!
Here is your flag:
pwn.college{sTMkxizDOnV4Kro1P8Eik_y1K7Q.QX4cTO0wyNyAzNzEzW}
```


## Program and Absolute Paths
Execute the `run` file that is in the `challenge` directory, which is, in turn, in the `/` directory.
### Solve
**Flag:** `pwn.college{wZuWje4u0M1rK3Rm4BEwvgSrsDL.QX1QTN0wyNyAzNzEzW}`
As specified, I ran the command `/challenge/run` in the terminal.
```
hacker@paths~program-and-absolute-paths:~$ /challenge/run
Correct!!!
/challenge/run is an absolute path! Here is your flag:
pwn.college{wZuWje4u0M1rK3Rm4BEwvgSrsDL.QX1QTN0wyNyAzNzEzW}
```


## Position Thyself
Execute the `/challenge/run` program from a specific path. `cd` into the path before re-running the command.
### Solve
**Flag:** `pwn.college{oDlRA0h-Ntv-b3x9Y20cxc1bPLJ.QX2QTN0wyNyAzNzEzW}`
After running the `/challenge/run` command I was prompted the path `/usr/aarch64-linux-gnu/include/gnu`. After `cd`ing into it, I re-ran the `/challenge/run` command.
```
hacker@paths~position-thy-self:~$ /challenge/run
Incorrect...
You are not currently in the /usr/aarch64-linux-gnu/include/gnu directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-thy-self:~$ cd /usr/aarch64-linux-gnu/include/gnu
hacker@paths~position-thy-self:/usr/aarch64-linux-gnu/include/gnu$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{oDlRA0h-Ntv-b3x9Y20cxc1bPLJ.QX2QTN0wyNyAzNzEzW}
```


## Position Elsewhere
Execute the `/challenge/run` program from a specific path. `cd` into the path before re-running the command.
### Solve
**Flag:** `pwn.college{E7E93sSSCTRS8Ie__V7jvzwpKA7.QX3QTN0wyNyAzNzEzW}`
After running the `/challenge/run` command I was prompted the path `/var/lib/apt/lists`. After `cd`ing into it, I re-ran the `/challenge/run` command.
```
hacker@paths~position-elsewhere:~$ /challenge/run
Incorrect...
You are not currently in the /var/lib/apt/lists directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-elsewhere:~$ cd /var/lib/apt/lists
hacker@paths~position-elsewhere:/var/lib/apt/lists$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{E7E93sSSCTRS8Ie__V7jvzwpKA7.QX3QTN0wyNyAzNzEzW}
```


## Position Yet Elsewhere
Execute the `/challenge/run` program from a specific path. `cd` into the path before re-running the command.
### Solve
**Flag:** `pwn.college{gGhKjEHP6UVsHv_piVuIydJxKwo.QX4QTN0wyNyAzNzEzW}`
After running the `/challenge/run` command I was prompted the path `/proc/138/fd`. After `cd`ing into it, I re-ran the `/challenge/run` command.
```
hacker@paths~position-yet-elsewhere:~$ /challenge/run
Incorrect...
You are not currently in the /proc/138/fd directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-yet-elsewhere:~$ cd /proc/138/fd
hacker@paths~position-yet-elsewhere:/proc/138/fd$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{gGhKjEHP6UVsHv_piVuIydJxKwo.QX4QTN0wyNyAzNzEzW}
```


## Implicit Relative Paths, from /
Run the `/challenge/run` command using a relative path while having a current directory of `/`.
### Solve
**Flag:** `pwn.college{cb3tOCaHssUEjqhYWAKuFPHJ6pa.QX5QTN0wyNyAzNzEzW}`
After running the `/challenge/run` command I was prompted to go to the `root` directory. And since, I am already in the root directory, I can simply use the relative path to run the `run` command using `challenge/run`.
```
hacker@paths~implicit-relative-paths-from-:~$ /challenge/run
Incorrect...
You are not currently in the / directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~implicit-relative-paths-from-:~$ cd /
hacker@paths~implicit-relative-paths-from-:/$ challenge/run
Correct!!!
challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{cb3tOCaHssUEjqhYWAKuFPHJ6pa.QX5QTN0wyNyAzNzEzW}
```


## Explicit Relative Paths, from /
Using `.` in the relative path.
### Solve
**Flag:** `pwn.college{MEc5o1rkId5S8XSwwePbp9Sqt7j.QXwUTN0wyNyAzNzEzW}`
`.` is an alias for the current directory.
```
hacker@paths~explicit-relative-paths-from-:~$ /challenge/run
Incorrect...
You are not currently in the / directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~explicit-relative-paths-from-:~$ cd /
hacker@paths~explicit-relative-paths-from-:/$ /challenge/run
Incorrect...
You invoked this challenge with an absolute path. This challenge needs a relative path!
hacker@paths~explicit-relative-paths-from-:/$ challenge/run
Incorrect...
This challenge must be called with a relative path that explicitly starts with a `.`!
hacker@paths~explicit-relative-paths-from-:/$ ./challenge/run
Correct!!!
./challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{MEc5o1rkId5S8XSwwePbp9Sqt7j.QXwUTN0wyNyAzNzEzW}
```


## Implicit Relative Path
Run the `/challenge/run` command from `/challenge` directory using `./`.
### Solve
**Flag:** `pwn.college{8KCQhMaIiL_mhyqfEPlxYC2fLcC.QXxUTN0wyNyAzNzEzW}`
Since running a command, runs it globally, to run the `run` command inside the `/challenge/` folder, I need to explicitly mention that I need to run the `run` command which is inside the mentioned directory using the `./` alias.
```
hacker@paths~implicit-relative-path:~$ /challenge/run
Incorrect...
You are not currently in the /challenge directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~implicit-relative-path:~$ cd /challenge
hacker@paths~implicit-relative-path:/challenge$ ./run
Correct!!!
./run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{8KCQhMaIiL_mhyqfEPlxYC2fLcC.QXxUTN0wyNyAzNzEzW}
hacker@paths~implicit-relative-path:/challenge$ run
bash: run: command not found
```


## Home Sweet Home
Execute the `/challenge/run` with a path provided. It will copy the flag to that path and read it back to you.<br>
**Constraints:**<br>
- The path must be an absolute path.
- The path must be inside the `home` directory.
- The path must be exactly *3 characters* long.
### Solve
**Flag:** `pwn.college{47mBbjcnObwcMkr-B2E6EQtQWgw.QXzMDO0wyNyAzNzEzW}`
Executed the command `/challenge/run ~/~`.\
`~` is an alias for `/home/<user-name>` directory (and since the path starts from `/`, it means the path is absolute). Also, only the first `~` is expanded. Anything after (like in this case) is simply treated as a string. Thus, the expanded path is `/home/hacker/~`.
```
hacker@paths~home-sweet-home:~$ /challenge/run ~/~
Writing the file to /home/hacker/~!
... and reading it back to you:
pwn.college{47mBbjcnObwcMkr-B2E6EQtQWgw.QXzMDO0wyNyAzNzEzW}
```


### New Learnings
- `~/~` expanded is `/home/<user-name>/~` and not `/home/<user-name>/home/<user-name>/`.
- The filesystem
    1. `/bin` - stands for **binaries**. Contains all the command files.
    2. `/sbin` - stands for **system binaries**. Contains commands accessible to the root user.
    3. `/boot` - ***Do NOT*** play around in this folder. Contains the files essential for booting the linux OS.
    4. `/dev` - stands for **devices**. This is where all the devices like ram, sda, sdb etc live. *Everything in linux is a file. Commands, printers, network setting - everything.*
    5. `/etc` - stands for **et cetera**. Contains system-wide applications like `apt`.
    6. `/lib, /lib32 and /lib66` - stands for **libraries**. Libraries are files required by applications to perform various functions. Used by files in `/bin` and `/sbin` folders.
    7. `/mnt and /media` - the former stands for **mount**. Here, all the devices such as pen-drive, floppy, hard disk etc lives. *In case of dual boot or `WSL`, the `C:` drive is also present here as `c/`.*
    8. `/opt` - **Optional** folder. Usually, here the manually installed programs from the vendor resides.
    9. `/proc` - stands for **processes**. Contains the files managed by the kernel.
    10. `/root` - this is the root user's home directory. Need root permissions to access this.
    11. `/run` - contains the runtime process files. All of this files are gone when the system shutsdown. RAM files basically.
    12. `/sys` - **system** directory. Used to interact with the kernel. Similar to the `/run` dir, the contents are deleted after shutdown.
    13. `/tmp` - **temporary**. Stores the copy of the files for current session of a program in case it crashes.
    14. `/usr` - **User** or **Unix System Resource**. Contains files not used by the system, but by the user.
    15. `/var` - stands for **variable**. Contains the files that are expected to grow in size. e.g. `/var/logs/` and `/var/crash/`.
    16. `/home` - contains the users mounted to the device. Every user's personal files go into their folder in the `/home` dir.


### References
[Linux File System/Structure Explained by DorianDotSlash](https://youtu.be/HbgzrKJvDRw?si=4pF5tDcFD-cyh1m3)
