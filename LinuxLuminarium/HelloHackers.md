# Hello Hackers

## Intro to Commands
Invoke the `hello` command to obtain the flag.

### Solve
**Flag:** `pwn.college{wanBCzS7U8XdRHRDKhPZPjQ9_FA.QX3YjM1wyNyAzNzEzW}`</br>
Entered the `hello` command in the pwn.college terminal.
```
hacker@hello~intro-to-commands:~$ hello
Success! Here is your flag:
pwn.college{wanBCzS7U8XdRHRDKhPZPjQ9_FA.QX3YjM1wyNyAzNzEzW}
```


## Intro to Arguments
Run the `hello` command with the single argument of `hackers` in the terminal.

### Solve
**Flag:** `pwn.college{ou2K4x11qpXePcq1hEWGr4kwMTx.QX4YjM1wyNyAzNzEzW}`</br>
Entered the `hello hackers` command in the pwn.college terminal.
```
hacker@hello~intro-to-arguments:~$ hello hackers
Success! Here is your flag:
pwn.college{ou2K4x11qpXePcq1hEWGr4kwMTx.QX4YjM1wyNyAzNzEzW}
```


## Command History
Bring up a terminal and hit the `up arrow` key to get the flag.

### Solve

**Flag:** `pwn.college{MM2PsSWwmwtUGIUmYd6JgkGzZFw.0lNzEzNxwyNyAzNzEzW}`</br>
Hit the `up arrow` in the pwn.college terminal.

```
hacker@hello~command-history:~$ the flag is pwn.college{MM2PsSWwmwtUGIUmYd6JgkGzZFw.0lNzEzNxwyNyAzNzEzW}
```


## New Learnings

**1. Terminal/Terminal Emulator :** Pedantically speaking, the terminal on the linux machine is an emulator which allows us to use the functionalities of a physical terminal on our system. Traditionally, a terminal was a system which you can interact with using text based commands. A terminal emulator lets you achieve that locally on your system.

**2. Shell :** A shell is a command line interpreter. Lets us interact with the operating system. When we type commands in the terminal, shell interprets and executes that command and display the output on the terminal. Traditionally, unix used the Bourne shell. Now it uses the bash(Bourne Again Shell) shell. Windows uses the powershell and Mac - zsh.

**3. Components of a prompt:** When you launch a terminal session, the very first thing you see is a prompt something like `hacker@dojo:~$`. Here, `hacker` is the name of the user currently using the system. `dojo` is the name of the machine user is on. `~` is an alias for home directory. Anything after *colon* represents the present working directory(pwd). Default workspace is `/home/user` where the first `/` represents the *root* directory. The root directory contains *all* the system files. `$` signifies that the shell is ready to take input but not as the *root* user. In unix systems, root is the user with admin privileges. If you are logged in as a root user, you will see a `#` sign.



***Note: There are additional paramaters that can be passed to a command known as flags. It gives additional functionality to the command.***
e.g. `rm` removes a file but `rm -r` removes a file(folder) recursively i.e. a folder and all the contents within it.
