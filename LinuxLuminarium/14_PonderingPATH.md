# Pondering PATH

## The PATH Variable
In this level, you will disrupt the operation of the `/challenge/run` program. This program will DELETE the flag file using the `rm` command. However, if it can't find the `rm` command, the flag will not be deleted, and the challenge will give it to you! Thus, you must make it so that `/challenge/run` also can't find the `rm` command!
### Solve
**Flag:** `pwn.college{wzdxdoXUWNi-kpTSI0hd37lJKlM.QX2cDM1wyNyAzNzEzW}`
- reassign `PATH` as an empty variable.
- this way, it'll not find any system commands including `rm`.
```bash
hacker@path~the-path-variable:~$ PATH=""
hacker@path~the-path-variable:~$ /challenge/run
Trying to remove /flag...
/challenge/run: line 4: rm: No such file or directory
The flag is still there! I might as well give it to you!
pwn.college{wzdxdoXUWNi-kpTSI0hd37lJKlM.QX2cDM1wyNyAzNzEzW}
```


## Setting PATH
Let's practice. This level's `/challenge/run` will run the `win` command via its bare name, but this command exists in the `/challenge/more_commands/` directory, which is not initially in the `PATH.` The win command is the only thing that `/challenge/run` needs, so you can just overwrite `PATH` with that one directory.
### Solve
**Flag:** `pwn.college{AHZqld6o44s-RgoDvT6v8wluaqz.QX1cjM1wyNyAzNzEzW}`
```
hacker@path~setting-path:~$ PATH="/challenge/more_commands/"
hacker@path~setting-path:~$ /challenge/run
Invoking 'win'....
Congratulations! You properly set the flag and 'win' has launched!
pwn.college{AHZqld6o44s-RgoDvT6v8wluaqz.QX1cjM1wyNyAzNzEzW}
```


## Finding Commands
In this challenge, we added a `win` command somewhere in your `$PATH`, but it won't give you the flag. Instead, it's in the same directory as a `flag` file that we made readable by you! You must find `win` (with the `which` command), and `cat` the flag out of that directory!
### Solve
**Flag:** `pwn.college{E28nrJl7Xcaola7meaMnjWuAxFL.01NzEzNxwyNyAzNzEzW}`
```
hacker@path~finding-commands:~$ which win
/challenge/paths/2424/win
hacker@path~finding-commands:~$ ls /challenge/paths/2424
flag  win
hacker@path~finding-commands:~$ cat /challenge/paths/2424/flag
pwn.college{E28nrJl7Xcaola7meaMnjWuAxFL.01NzEzNxwyNyAzNzEzW}
```


## Adding Commands
Previously, the `win` command that `/challenge/run` executed was stored in `/challenge/more_commands.` This time, `win` does not exist! Recall the final level of `Chaining Commands`, and make a shell script called `win`, add its location to the `PATH`, and enable `/challenge/run` to find it!
### Solve
**Flag:** `pwn.college{YA5lVPnLsA7iJfoZQJMu4lh5eIS.QX2cjM1wyNyAzNzEzW}`\
Things to keep in mind:
- Create the file `win` and not `win.sh`
- Add both paths to `PATH` variable, of `cat` as well as `win`.
- Make `win` file executable.
> `win` content
```bash
#!/bin/bash

cat /flag
```
> Output
```
hacker@path~adding-commands:~$ echo $PATH
/run/challenge/bin:/run/dojo/bin:/root/.cargo/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
hacker@path~adding-commands:~$ pwd
/home/hacker
hacker@path~adding-commands:~$ ls
 COLLEGE   Desktop   PWN   a   instructions   msg   myflag   not-the-flag   processes   solve.sh   the-flag   win.sh   x.sh  '~'
hacker@path~adding-commands:~$ vim win.sh
hacker@path~adding-commands:~$ which cat
/run/dojo/bin/cat
hacker@path~adding-commands:~$ PATH="/home/hacker:/run/dojo/bin"
hacker@path~adding-commands:~$ /challenge/run
Invoking 'win'....
/challenge/run: line 4: win: command not found
It looks like that did not work... Did you set PATH correctly?
hacker@path~adding-commands:~$ echo $PATH
/home/hacker:/run/dojo/bin
hacker@path~adding-commands:~$ mv win.sh win
hacker@path~adding-commands:~$ /challenge/run
Invoking 'win'....
/challenge/run: line 4: /home/hacker/win: Permission denied
It looks like that did not work... Did you set PATH correctly?
hacker@path~adding-commands:~$ chmod a+x win
hacker@path~adding-commands:~$ /challenge/run
Invoking 'win'....
pwn.college{YA5lVPnLsA7iJfoZQJMu4lh5eIS.QX2cjM1wyNyAzNzEzW}
```


## Hijacking Commands
Armed with your knowledge, you can now carry out some shenanigans. This challenge is almost the same as the first challenge in this module. Again, this challenge will delete the flag using the `rm` command. But unlike before, it will not print anything out for you.

How can you solve this? You know that `rm` is searched for in the directories listed in the `PATH` variable. You have experience creating the `win` command when the previous challenge needed it. What else can you create?
### Solve
**Flag:** `pwn.college{gzIDHbazS5GSSVesJyqhBY5koy6.QX3cjM1wyNyAzNzEzW}`\
*Facts:*
- `/challenge/run` makes use of the command `rm /flag`.
- `/challenge/run` is executed as root.
- `cat` and `rm` both exist in the same directory.
- `cat` is a symbolic link pointing to another file.

*Approach:*
- create another `rm` file in `/home/hacker` directory which simply prints the content of `flag` file.
- make it executable.
- create another symbolic link `cat` in `/home/hacker` dir and point it where the original `cat` was pointing.
- it has same permissions as the file it points to.
- update the `PATH` variable such it only contains the path `/home/hacker`.
- run the `/challenge/run` command.

> new `rm` content
```bash
#!/bin/bash

cat /flag
```
> output
```
hacker@path~hijacking-commands:~$ ls
 COLLEGE   Desktop   PWN   a   cat   instructions   msg   myflag   not-the-flag   processes   rm   solve.sh   the-flag   win   x.sh  '~'
hacker@path~hijacking-commands:~$ echo $PATH
/run/challenge/bin:/run/dojo/bin:/root/.cargo/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
hacker@path~hijacking-commands:~$ ls -l cat
lrwxrwxrwx 1 hacker hacker 65 Sep 29 05:24 cat -> /nix/store/mp7ba85zcqdj2sqwa29pql02s6nqpcxy-coreutils-9.7/bin/cat
hacker@path~hijacking-commands:~$ PATH="/home/hacker"
hacker@path~hijacking-commands:~$ /challenge/run
Trying to remove /flag...
pwn.college{gzIDHbazS5GSSVesJyqhBY5koy6.QX3cjM1wyNyAzNzEzW}
```


### New Learnings
- the `PATH` variable
    - `PATH` in Linux is an environment variable that tells the shell where to look for executables when you type a command.

        - It’s a colon-separated list of directories (e.g., `/usr/bin:/bin:/usr/local/bin`).
        - When you run `ls`, the shell searches these directories in order until it finds the `ls` program.
        - You can add custom paths (e.g., `export PATH=$PATH:/home/user/bin`) to run your own scripts without giving full paths.

- `builtins` don't require the `PATH` variable.

- `which` command shows the full path of the executable that will run when you type a command.
