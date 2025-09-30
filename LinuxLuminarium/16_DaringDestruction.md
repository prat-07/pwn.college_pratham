# Daring Destruction

## The Fork Bomb
- make a script
- make it executable
- make it launch two more instances of itself in the background

Run the `/challenge/check` command in another terminal before executing the script.
### Solve
**Flag:** `pwn.college{8UbfspcKlBBxWA-k1mVUrwGUGGn.0VMyEzNxwyNyAzNzEzW}`
- create a script named `fork-bomb`
- add the commands where the script runs itself
- make it executable
- run `/challenge/check` in another terminal
- run the script
- wait for the process table to fill up and get the flag.
> script content
```bash
#!/bin/bash

bash fork-bomb.sh &
bash fork-bomb.sh &
```


## Disk-Space Doomsday
This challenge forces you to fill the disk and then clean up. The process:

- Fill your disk.
 - Run `/challenge/check`. It will attempt to create a *1 megabyte* temporary file. If that fails, you pass the first stage and the checker will ask you to free the space.
  - Delete the file you made (with `rm`) to clear up the space.
   - Run `/challenge/check` a second time. If it can now create the temporary file (i.e., you successfully cleaned up your home directory), you’ll receive the flag.

### Solve
**Flag:** `pwn.college{8oHAUib8DSUqobPnIqfTP2w7wqw.0lMyEzNxwyNyAzNzEzW}`
> command used
```
yes >> doomsday
```
> output
```
hacker@destruction~disk-space-doomsday:~$ /challenge/check
Well done, you clogged the disk. Now free that space (remove the file you created) and run /challenge/check again to prove you cleaned up!
hacker@destruction~disk-space-doomsday:~$ /challenge/check
Disk space restored. Here is your flag:
pwn.college{8oHAUib8DSUqobPnIqfTP2w7wqw.0lMyEzNxwyNyAzNzEzW}
hacker@destruction~disk-space-doomsday:~$
```

## rm -rf /
Wipe the slate clean with the command `rm -rf /`. But, make sure to run `/challenge/check` file to check if the task has been completed to receive the flag.
### Solve
**Flag:** `pwn.college{4Qokvrx-IqVumM7d1u6opPqB_0W.0lMzEzNxwyNyAzNzEzW}`
> command used
```
rm -rf / --no-preserve-root
```
***The flag `--no-preserve-root` is a failsafe mechanism***



## Life after rm -rf /
After you `rm` everything, your previously-launched `/challenge/check` will restore the `/flag` file and make it readable. Then you can `read` it!
### Solve
**Flag:** `pwn.college{IpWVCivy9evybXvCn3ErSH-ZSZj.01MzEzNxwyNyAzNzEzW}`
- run `/challenge/check`
- in another terminal wipe off the system using the previous command.
- when done, `/challenge/check` will restore the `/flag` file.
- use `read` to input the content of the file into a variable.
- echo the variable to get the flag.



## Finding meaning after rm -rf /
This time, `/challenge/check` will restore the flag to a randomly-named file. You'll need to find it without reaching for your `ls` command.

There are a lot of ways to solve this challenge. `echo` is a `builtin`, and you can File Glob an argument to it to expand to all files! For example, `echo *` will print out the names of all of the files in the current directory. Similarly, you can use tab-completion (hit tab a few times) of an argument to have the shell list possible files for you.

Whatever route you use, find the randomly-named file that `/challenge/check` makes in `/` after you `rm`, read it, and get the flag!
### Solve
**Flag:** `pwn.college{4QUkqlF6ZJbX7bmox_AHwZpiD5P.0FNzEzNxwyNyAzNzEzW}`
- run `/challenge/check` command
- open another terminal and remove the `/` folder altogether
- `/challenge/check` commands restores the flag in `/` dir with a random name
- type `read temp < /` and press `tab` twice to list all the possible files it can take as argument
- saw a file named `06ea96a6` which seemed pretty random to me
- read it into a variable and echo the variable to get the flag.
```
hacker@destruction~finding-meaning-after-rm-rf-:~$ read temp < /
06ea96a6  dev/      etc/      home/     nix/      proc/     run/      sys/      usr/
hacker@destruction~finding-meaning-after-rm-rf-:~$ read temp < /06ea96a6
hacker@destruction~finding-meaning-after-rm-rf-:~$ echo $temp
pwn.college{4QUkqlF6ZJbX7bmox_AHwZpiD5P.0FNzEzNxwyNyAzNzEzW}
```


### New Learnings
- ***Creating processes faster what the kernel can handle can make everything grind to a halt.***
- **Fork Bombs**
    - A fork bomb is a small program that rapidly replicates itself by creating child processes, causing process count to grow exponentially until the system’s process table and CPU are exhausted. The result: new processes can’t start, services stall, and the machine becomes unresponsive.
- **The `yes` command**
    - Repeatedly outputs a string (by default `y`) until it is stopped. Usually used to pass confirmation to commands/scripts automatically.
- **`builtins` and `read`**
    - `builtins` will work even after you delete your entire system since they are not files stored inside the system.
    - `read` builtin can be used to read files and `echo` inturn can print those files to the terminal.
    - `echo *` will print out the names of all the files in the current directory.
