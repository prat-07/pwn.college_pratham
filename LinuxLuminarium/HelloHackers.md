# Command Line Basics

## Terminologies

**1. Terminal/Terminal Emulator :** Pedantically speaking, the terminal on the linux machine is an emulator which allows us to use the functionalities of a physical terminal on our system. Traditionally, a terminal was a system which you can interact with using text based commands. A terminal emulator lets you achieve that locally on your system.

**2. Shell :** A shell is a command line interpreter. Lets us interact with the operating system. When we type commands in the terminal, shell interprets and executes that command and display the output on the terminal. Traditionally, unix used the Bourne shell. Now it uses the bash(Bourne Again Shell) shell. Windows uses the powershell and Mac - zsh.

**3. Components of a prompt:** When you launch a terminal session, the very first thing you see is a prompt something like `hacker@dojo:~$`. Here, `hacker` is the name of the user currently using the system. `dojo` is the name of the machine user is on. `~` is an alias for home directory. Anything after *colon* represents the present working directory(pwd). Default workspace is `/home/user' where the first `/` represents the **root** directory. The root directory contains *all* the system files. And, `$` means that the shell is ready to take input but not as a **root** user. In unix systems, root is the user with admin privileges. If you are logged in as a root user, you will see a `#` symbol instead of `$`.

## Commands Used
`whoami` : prints the user's username.
`hello` : not a real command, used to obtain the flag: `pwn.college{wanBCzS7U8XdRHRDKhPZPjQ9_FA.QX3YjM1wyNyAzNzEzW}`
`echo` : simply prints the input back to the terminal. Anything written after echo is an *argument* to the echo command(any command in general) which it prints back to the terminal.
`hello hackers` : not a real command, used to obtain the flag: `pwn.college{ou2K4x11qpXePcq1hEWGr4kwMTx.QX4YjM1wyNyAzNzEzW}`
**command history** : use up arrow to browse back to previous commands used, down arrow to go forward. Key obtained using up arrow: `pwn.college{MM2PsSWwmwtUGIUmYd6JgkGzZFw.0lNzEzNxwyNyAzNzEzW}`

# Summary of module 1: Hello Hackers
-Learning Terminologies
-Learning Basic Commands
-Arguments to commands
-Scrolling through history using up and down arrow.

***Note: There are additional paramaters that can be passed to a command known as flags. It gives additional functionality to the command.***
e.g. `rm` removes a file but `rm -r` removes a file(folder) recursively i.e. a folder and all the contents within it.


