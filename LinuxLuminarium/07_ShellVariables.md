# Shell Variables

## Printing Variables
The flag has been put into the variable called "FLAG"! Just have your shell print it out!
### Solve
**Flag:** `pwn.college{g_mJdZOzkZyfoXfELVc6ddztNRw.QX3UTN0wyNyAzNzEzW}`\
Prepending the argument given to `echo` with `$` will print out the value that variable holds.\
`$FLAG` represents the variable flag but `FLAG` represents the string "FLAG". 
```
hacker@variables~printing-variables:~$ echo $FLAG
pwn.college{g_mJdZOzkZyfoXfELVc6ddztNRw.QX3UTN0wyNyAzNzEzW}
```


## Setting Variables
To solve this level, you must set the `PWN` variable to the value `COLLEGE`.
### Solve
**Flag:** `pwn.college{QG6oNrq9pPJxUp6lGN5xlnXhOJ8.QX5UTN0wyNyAzNzEzW}`\
Do not put any whitespaces during assignment as then the shell will try to run `PWN` as a command.
```
hacker@variables~setting-variables:~$ PWN=COLLEGE
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{QG6oNrq9pPJxUp6lGN5xlnXhOJ8.QX5UTN0wyNyAzNzEzW}
```


## Multi-word Variables
In this level, you'll need to set the variable `PWN` to `COLLEGE YEAH`. Good luck!
### Solve
**Flag:** `pwn.college{AXFudDPKBok5t_YIXA-Dvwx-pHY.QXwYTN0wyNyAzNzEzW}`
```
hacker@variables~multi-word-variables:~$ PWN="COLLEGE YEAH"
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{AXFudDPKBok5t_YIXA-Dvwx-pHY.QXwYTN0wyNyAzNzEzW}
```


## Exporting Variables
In this challenge, you must invoke `/challenge/run` with the `PWN` variable exported and set to the value `COLLEGE`, and the `COLLEGE` variable set to the value `PWN` but not exported.
### Solve
**Flag:** `pwn.college{czejEwmYnM1_ekSovOlFqhWScOS.QXyYTN0wyNyAzNzEzW}`
```
hacker@variables~exporting-variables:~$ export PWN=COLLEGE
You've set the PWN variable to the proper value!
hacker@variables~exporting-variables:~$ COLLEGE=PWN
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
hacker@variables~exporting-variables:~$ /challenge/run $PWN $COLLEGE
CORRECT!
You have exported PWN=COLLEGE and set, but not exported, COLLEGE=PWN. Great 
job! Here is your flag:
pwn.college{czejEwmYnM1_ekSovOlFqhWScOS.QXyYTN0wyNyAzNzEzW}
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
```


## Printing Exported Variables
Try the `env` command: it'll print out every exported variable set in your shell, and you can look through that output to find the `FLAG` variable!
### Solve
**Flag:** `pwn.college{Ahlyu3jEFNaj3OkcuaX8IffPcoi.QX4UTN0wyNyAzNzEzW}`
```
hacker@variables~printing-exported-variables:~$ env
SHELL=/run/dojo/bin/bash
HOSTNAME=variables~printing-exported-variables
PWD=/home/hacker
MANPATH=/run/dojo/share/man:
DOJO_AUTH_TOKEN=999ee3c20b46054e246b764141b5f9127305e0e2be54b5270f505352a647880f
HOME=/home/hacker
LANG=C.UTF-8
FLAG=pwn.college{Ahlyu3jEFNaj3OkcuaX8IffPcoi.QX4UTN0wyNyAzNzEzW}
TERMINFO=/run/dojo/share/terminfo
TERM=xterm-256color
SHLVL=2
LC_CTYPE=C.UTF-8
SSL_CERT_FILE=/run/dojo/etc/ssl/certs/ca-bundle.crt
PATH=/run/challenge/bin:/run/dojo/bin:/root/.cargo/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
DEBIAN_FRONTEND=noninteractive
_=/run/dojo/bin/env
```


## Storing Command Output
Read the output of the `/challenge/run` command directly into a variable called `PWN`, and it will contain the flag!
### Solve
**Flag:** `pwn.college{k8DQMRhtwHfNBjkLgG0hNBaavoX.QX1cDN1wyNyAzNzEzW}`
- Using *Command Substitution* assign output `/challenge/run` command to `PWN` variable.
- `echo` the variable
```
hacker@variables~storing-command-output:~$ PWN=$(/challenge/run)
Congratulations! You have read the flag into the PWN variable. Now print it out 
and submit it!
hacker@variables~storing-command-output:~$ echo $PWN
pwn.college{k8DQMRhtwHfNBjkLgG0hNBaavoX.QX1cDN1wyNyAzNzEzW}
```


## Reading Input
In this challenge, your job is to use read to set the `PWN` variable to the value `COLLEGE`. Good luck!
### Solve
**Flag:** `pwn.college{UeJz3IFYzr5n9mNd1U-WWa9jwUf.QX4cTN0wyNyAzNzEzW}`\
`read` is a *builtin* to read user input.\
Use the `-p` flag to read as a prompt.
```
hacker@variables~reading-input:~$ read -p "INPUT: " PWN
INPUT: COLLEGE
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{UeJz3IFYzr5n9mNd1U-WWa9jwUf.QX4cTN0wyNyAzNzEzW}
```


## Reading Files
Read `/challenge/read_me` into the `PWN` environment variable, and we'll give you the flag! The `/challenge/read_me` will keep changing, so you'll need to read it right into the `PWN` variable with one command!
### Solve
**Flag:** `pwn.college{M-El4as6lnEyFIoV9c78EfSwKk-.QXwIDO0wyNyAzNzEzW}`
```
hacker@variables~reading-files:~$ read PWN < /challenge/read_me 
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{M-El4as6lnEyFIoV9c78EfSwKk-.QXwIDO0wyNyAzNzEzW}
```


### New Learnings
- Set shell variable using `=` operator without any whitespace in between. Acess them using `$VAR-NAME`.
- Use `" "` for multiple-words
- `export` variables to use in other shell sessions.
- `env` to look for all environment / exported variables.
- `var = $(command)` will store the output of `command` in the `var` variable - *Command Substitution*.
- `read` builtin. (*Use mentioned above*.) 
- read files into variables using `<`.

