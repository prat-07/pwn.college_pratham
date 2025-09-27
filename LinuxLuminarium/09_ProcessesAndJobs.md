# Processes And Jobs

## Listing Processes
In this level, I have once again renamed `/challenge/run` to a random filename, and this time made it so that you cannot `ls` the `/challenge` directory! But I also launched it, so you can find it in the running process list, figure out the filename, and relaunch it directly for the flag!
### Solve
**Flag:** `pwn.college{IOCHHgAyn0aaHFe_ZJftoRJRLVF.QX4MDO0wyNyAzNzEzW}`\
After running the `ps -ef` command, found a process starting with `/challenge/...`. Could be the only file.
```
hacker@processes~listing-processes:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 04:46 ?        00:00:00 /sbin/docker-init -- /nix/var/nix/profiles/dojo-workspace/bin/dojo-init /run/dojo/bin/sleep 6h
root           7       1  0 04:46 ?        00:00:00 /run/dojo/bin/sleep 6h
root         132       1  0 04:46 ?        00:00:00 /challenge/16272-run-6902
root         135     132  0 04:46 ?        00:00:00 sleep 6h
hacker       146       1  0 04:46 ?        00:00:00 /nix/store/g0q8n7xfjp7znj41hcgrq893a9m0i474-ttyd-1.7.7/bin/ttyd --port 7681 --interface 0.0.0.
hacker       150     146  0 04:46 pts/0    00:00:00 /run/dojo/bin/bash --login
hacker       164     150  0 04:46 pts/0    00:00:00 ps -ef
hacker@processes~listing-processes:~$ /challenge/16272-run-6902
Yahaha, you found me! Here is your flag:
pwn.college{IOCHHgAyn0aaHFe_ZJftoRJRLVF.QX4MDO0wyNyAzNzEzW}
Now I will sleep for a while (so that you could find me with 'ps').
```


## Killing Processes
In this challenge, `/challenge/run` will refuse to run while `/challenge/dont_run` is running! You must find the `dont_run` process and `kill` it.
### Solve
**Flag:** `pwn.college{UT7NhMy_7O63_c9XIE8P8M6V7KW.QXyQDO0wyNyAzNzEzW}`\
Remember: you kill a process using it `PID` and *not* `PPID`.



## Interrupting Processes
`/challenge/run` will refuse to give you the flag until you interrupt it.
### Solve
**Flag:** `pwn.college{odfl7sA8ztEXUNOLl56LAifZzAb.QXzQDO0wyNyAzNzEzW}`\
Commands can be interrupted using the hotkey `Ctrl-C`.
```
hacker@processes~interrupting-processes:~$ /challenge/run
I could give you the flag... but I won't, until this process exits. Remember, 
you can force me to exit with Ctrl-C. Try it now!
^C
Good job! You have used Ctrl-C to interrupt this process! Here is your flag:
pwn.college{odfl7sA8ztEXUNOLl56LAifZzAb.QXzQDO0wyNyAzNzEzW}
```


## Killing Misbehaving Processes
In this challenge, there's a decoy process that's hogging a critical resource - a named pipe (FIFO) at `/tmp/flag_fifo` into which (like in the Practicing Piping FIFO challenge) `/challenge/run` wants to write your flag. You need to `kill` this process.

Your general workflow should be:

1. Check what processes are running.
2. Find `/challenge/decoy` in the list and figure out its process ID.
3. kill it.
4. Run `/challenge/run` to get the flag without being overwhelmed by decoys (you don't need to redirect its output; it'll write to the FIFO on its own).
### Solve
**Flag:** `pwn.college{0kr4Tmw87jzEipc2U11CshSagjF.0FNzMDOxwyNyAzNzEzW}`
- List the processes.
- Two process containing the keywords `/challenge/decoy`.
- `kill` the one which is not run by `root` (wouldn't be able to kill root one anyways, since I do not have the permission).
- Run `/challenge/run` command.
- Since the command is writing to a `pipe`, it must be read to complete the read and write process.
- Open new terminal and read the pipe file.
- Found many decoy flags there.
- Since the last command - `/challenge/run` pipes the correct flag into the FIFO, the last flag should be the correct one.
```
hacker@processes~killing-misbehaving-processes:~$ ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.1  0.0   1056   640 ?        Ss   05:16   0:00 /sbin/docker-init -- /nix/var/nix/prof
root           7  0.0  0.0 231708  2560 ?        S    05:16   0:00 /run/dojo/bin/sleep 6h
root         137  0.0  0.0   4132  1280 ?        S    05:16   0:00 /bin/bash /challenge/.init
root         138  0.0  0.0   4132  1280 ?        S    05:16   0:00 /bin/bash /challenge/.init
root         139  0.0  0.0   5204  3520 ?        S    05:16   0:00 su -c exec /challenge/decoy > /tmp/fla
root         140  0.0  0.0   2744  1600 ?        S    05:16   0:00 sleep 6h
root         141  0.0  0.0   2744  1280 ?        S    05:16   0:00 sleep 6h
hacker       142  0.1  0.0  13516  9280 ?        Ss   05:16   0:00 /usr/bin/python /challenge/decoy
hacker       153  2.4  0.0 1125980 76392 ?       Sl   05:16   0:00 /nix/store/a1kxazxkgw7mjbjgisvah95p1r3
hacker       176 11.7  0.0 1348000 108356 ?      Sl   05:16   0:04 /nix/store/a1kxazxkgw7mjbjgisvah95p1r3
hacker       225  1.4  0.0 1061836 65776 ?       Sl   05:16   0:00 /nix/store/a1kxazxkgw7mjbjgisvah95p1r3
hacker       265  2.5  0.0 179964 46464 ?        S    05:16   0:00 /nix/store/nnkd8d66viqr8xg9vbiyhpjjgk2
hacker       270  0.0  0.0 230716  2880 ?        S    05:16   0:00 /nix/store/ih68ar79msmj0496pgld4r3vqfr
hacker       280  1.7  0.0 5555456 38720 ?       S    05:16   0:00 /nix/store/h097imm3w6dpx10qynrd2sz9fks
hacker       296  0.7  0.0 565332 24640 ?        Sl   05:16   0:00 /nix/store/81f2pmz7y9jz2xdh44wg4cycc6q
hacker       299  0.0  0.0   6960  2240 ?        S    05:16   0:00 /nix/store/zbydgvn9gypb3vg88mzydn88ky6
hacker       300  0.2  0.0   6092  1920 ?        Ss   05:16   0:00 /run/current-system/sw/bin/dbus-daemon
hacker       305  0.3  0.0 530780  5760 ?        Sl   05:16   0:00 /nix/store/97ycb61fb3vismhljpx5fwrgymx
hacker       314  0.0  0.0  10944  1624 ?        Ss   05:16   0:00 /run/dojo/bin/ssh-agent -s
hacker       316  1.3  0.0 511744 37120 ?        Sl   05:16   0:00 xfwm4
hacker       322  0.6  0.0 499504 24960 ?        Sl   05:16   0:00 xfsettingsd
hacker       323  0.0  0.0 232104  4160 pts/0    Ss+  05:16   0:00 /run/dojo/bin/bash --init-file /nix/st
hacker       346  0.0  0.0 156140  5120 ?        Sl   05:16   0:00 /usr/libexec/dconf-service
hacker       349  2.3  0.0 729004 38720 ?        Sl   05:16   0:00 xfce4-panel
hacker       355  0.3  0.0 639360 24960 ?        Sl   05:16   0:00 Thunar --daemon
hacker       361  2.4  0.0 705988 65208 ?        Sl   05:16   0:00 xfdesktop
hacker       368  0.3  0.0 639328 26240 ?        Sl   05:16   0:00 /nix/store/wd6r31f7cx88p1gnmfkh7yij3nl
hacker       477  2.2  0.0 5555852 25956 ?       S    05:16   0:00 /nix/store/h097imm3w6dpx10qynrd2sz9fks
hacker       480  2.9  0.0 689552 39680 ?        Sl   05:16   0:00 xfce4-terminal
hacker       486  0.0  0.0 231976  4160 pts/1    Ss   05:16   0:00 -bash
hacker       495  0.0  0.0 233604  3840 pts/1    R+   05:16   0:00 ps aux
hacker@processes~killing-misbehaving-processes:~$ kill 142
hacker@processes~killing-misbehaving-processes:~$ /challenge/run
Sending the flag to /tmp/flag_fifo!
```
```
hacker@processes~killing-misbehaving-processes:~$ cat /tmp/flag_fifo
...
...
...
pwn.college{0kr4Tmw87jzEipc2U11CshSagjF.0FNzMDOxwyNyAzNzEzW}
```


### Suspending Processes
This level's `run` wants to see another copy of itself running and using the same terminal. How? Use the terminal to launch it, then suspend it, then launch another copy while the first is suspended!
### Solve
**Flag:** `pwn.college{ohmQU6CYIwIhBn1FB5FqtXn4BfY.QX1QDO0wyNyAzNzEzW}`
```
hacker@processes~suspending-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running in 
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root         319     307  0 05:29 pts/0    00:00:00 bash /challenge/run
root         321     319  0 05:29 pts/0    00:00:00 ps -f

I don't see a second me!

To pass this level, you need to suspend me and launch me again! You can 
background me with Ctrl-Z or, if you're not ready to do that for whatever 
reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~suspending-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running in 
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root         319     307  0 05:29 pts/0    00:00:00 bash /challenge/run
root         326     307  0 05:30 pts/0    00:00:00 bash /challenge/run
root         328     326  0 05:30 pts/0    00:00:00 ps -f

Yay, I found another version of me! Here is the flag:
pwn.college{ohmQU6CYIwIhBn1FB5FqtXn4BfY.QX1QDO0wyNyAzNzEzW}
```


## Resuming Processes
This challenge's `run` needs you to suspend it, then resume it.
### Solve
**Flag:** `pwn.college{UcGeuPRKOEQbqD-6cfE2nQIXTMn.QX2QDO0wyNyAzNzEzW}`
```
hacker@processes~resuming-processes:~$ /challenge/run
Let's practice resuming processes! Suspend me with Ctrl-Z, then resume me with 
the 'fg' command! Or just press Enter to quit me!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~resuming-processes:~$ fg /challenge/run
/challenge/run
I'm back! Here's your flag:
pwn.college{UcGeuPRKOEQbqD-6cfE2nQIXTMn.QX2QDO0wyNyAzNzEzW}
Don't forget to press Enter to quit me!

Goodbye!
```


## Backgrounding Processes
This level's `run` wants to see another copy of itself running, not suspended, and using the same terminal. How? Use the terminal to launch it, then suspend it, then background it with `bg` and launch another copy while the first is running in the background!
### Solve
**Flag:** `pwn.college{MXMD7MMB3gJLT0eO8Y8rQEb0kSf.QX3QDO0wyNyAzNzEzW}`
```
I don't see a second me!

To pass this level, you need to suspend me, resume the suspended process in the 
background, and then launch a new version of me! You can background me with 
Ctrl-Z (and resume me in the background with 'bg') or, if you're not ready to 
do that for whatever reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~backgrounding-processes:~$ bg /challenge/run
[1]+ /challenge/run &
hacker@processes~backgrounding-processes:~$ 


Yay, I'm now running the background! Because of that, this text will probably 
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times 
to scroll this text out.

hacker@processes~backgrounding-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and 
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root         144 S    bash /challenge/run
root         154 S    sleep 6h
root         155 S+   bash /challenge/run
root         157 R+   ps -o user=UID,pid,stat,cmd

Yay, I found another version of me running in the background! Here is the flag:
pwn.college{MXMD7MMB3gJLT0eO8Y8rQEb0kSf.QX3QDO0wyNyAzNzEzW}
```


## Foregrounding Processes
For this challenge, run the `/challenge/run` command, suspend it, resume it in background and then swap it into foreground.
### Solve
**Flag:** `pwn.college{AdPJyrGBqRttOM0T48MU2svJ2P9.QX4QDO0wyNyAzNzEzW}`
```
hacker@processes~foregrounding-processes:~$ /challenge/run
To pass this level, you need to suspend me, resume the suspended process in the 
background, and *then* foreground it without re-suspending it! You can 
background me with Ctrl-Z (and resume me in the background with 'bg') or, if 
you're not ready to do that for whatever reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~foregrounding-processes:~$ bg /challenge/run
[1]+ /challenge/run &
hacker@processes~foregrounding-processes:~$ 

Yay, I'm now running the background! Because of that, this text will probably 
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times 
to scroll this text out. After that, resume me into the foreground with 'fg'; 
I'll wait.

hacker@processes~foregrounding-processes:~$ fg /challenge/run
/challenge/run
YES! Great job! I'm now running in the foreground. Hit Enter for your flag!

pwn.college{AdPJyrGBqRttOM0T48MU2svJ2P9.QX4QDO0wyNyAzNzEzW}
```


## Starting Background Processes
Launch `/challenge/run` backgrounded for the flag!
### Solve
**Flag:**`pwn.college{MNuGpFZu2hml0ElcX51JkULhgI4.QX5QDO0wyNyAzNzEzW}`
```
hacker@processes~starting-backgrounded-processes:~$ /challenge/run &
[1] 146
hacker@processes~starting-backgrounded-processes:~$ 


Yay, you started me in the background! Because of that, this text will probably 
overlap weirdly with the shell prompt, but you're used to that by now...

Anyways! Here is your flag!
pwn.college{MNuGpFZu2hml0ElcX51JkULhgI4.QX5QDO0wyNyAzNzEzW}

[1]+  Done                    /challenge/run
```


## Process Exit Codes
In this challenge, you must retrieve the exit code returned by `/challenge/get-code` and then run `/challenge/submit-code` with that error code as an argument.
### Solve
**Flag:** `pwn.college{k2qPgh0zQ3hhLOMtXAKpM5vFIdB.QX5YDO1wyNyAzNzEzW}`\
- `?` is a builtin variable (env variable) that holds the exit code of the last executed command.
- `echo` it using `$` to expand the `?` variable.
```bash
hacker@processes~process-exit-codes:~$ /challenge/get-code
Exiting with an error code!
hacker@processes~process-exit-codes:~$ echo $?
42
hacker@processes~process-exit-codes:~$ /challenge/submit-code 42
CORRECT! Here is your flag:
pwn.college{k2qPgh0zQ3hhLOMtXAKpM5vFIdB.QX5YDO1wyNyAzNzEzW}
```


### New Learnings
- `ps` - process status
    - list processes in terminal by default.
    - Two ways to specify arguments.
        - Standard Syntax
            1. `-e` to list *every* process.
            2. `-f` for a *full* format.
        - BSD Syntax
            1. `a` to list processes for all users.
            2. `x` to list processes that aren't running in the terminal.
            3. `u` for user readable output.
- `pid`
    - process id.
    - used to identify process and also kill them.

- `kill PID`
    - a *builtin*
    - kills the process altogether.

- `CTRL-C`
    - interrupts the process.

- `CTRL-Z`
    - suspends the process. Can be resumed later.

- `fg`
    - a *builtin*.
    - Run or resume suspended/background process in *foreground*.

- `bg`
    - stands for *background*
    - Run or resume suspended process in background.

- `&`
    - appending a command with `&` will run it in the background right off the bat.

- `exit codes`
    - every command after execution returns an exit code.
    - `0` represents the process was completed successfully.
    - a *non-zero* value (typically 1) means there was an error.
    - a specific error code may represent a particular type of error.

- Difference between suspended and backgrounded properties.
    - To see command status, use `-o` flag with the `ps` command and pass `stat` to it.
    - e.g. `ps -o user,pip,stat,cmd`
    - Various stat symobols
        - `S` Sleeping in background while waiting for input.
        - `Ss` Same as above. Extra `s` signifies it as a session leader.
        - `R` Currently running.
        - `+` In foreground.


