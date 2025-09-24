# Digesting Documentation

## Learning from Documentation
This module teaches us how and where to look for help in order to use an unfamiliar command properly.\
The program for this challenge is `/challenge/challenge` and we need to pass the argument `--giveflag` to it.
### Solve
**Flag:** `pwn.college{oX7P_sTeV-RvRfaJemKJdUfwiWi.QX0ITO0wyNyAzNzEzW}`
```
hacker@man~learning-from-documentation:~$ /challenge/challenge --giveflag
Correct argument! Here is your flag:
pwn.college{oX7P_sTeV-RvRfaJemKJdUfwiWi.QX0ITO0wyNyAzNzEzW}
```


## Learning Complex Usage
This program i.e. `/challenge/challenge` print arbitrary files to the terminal, when given the `--printfile` argument. Furthermore, the argument to the `--printfile` is the path of the flag to read.
### Solve
**Flag:** `pwn.college{c2MX0LQPdaizFH0nourVtibiVls.QX1ITO0wyNyAzNzEzW}`\
As specified, pass the `--printfile` argument to the `/challenge/challenge` command. And since, the flag is always in `/flag`, I passed that pass as an argument to the `--printfile` argument.
```
hacker@man~learning-complex-usage:~$ /challenge/challenge --printfile /flag
Correct argument! Here is the /flag file:
pwn.college{c2MX0LQPdaizFH0nourVtibiVls.QX1ITO0wyNyAzNzEzW}
```


## Reading Manuals
Learn the secret option of `challenge` command using man. Doing it correctly will give you the flag.
### Solve
**Flag:** `pwn.college{8EYDKEmG-MuC9tCkWeXAu5jWVNR.QX0EDO0wyNyAzNzEzW}`\
After using the `man challenge` command, under the **SYNOPSIS** section, there was a flag mentioned `--mutkeu NUM` with the description that *it will return the flag if the value of `NUM` is **895***.
```
hacker@man~reading-manuals:~$ man challenge
hacker@man~reading-manuals:~$ /challenge/challenge --mutkeu 895
Correct usage! Your flag: pwn.college{8EYDKEmG-MuC9tCkWeXAu5jWVNR.QX0EDO0wyNyAzNzEzW}
```


## Searching Manuals
Use the `vim` keybindings to browse the `man` page.\
Find the option that will give you the flag by reading the `challenge` man page.
### Solve
**Flag:** `pwn.college{AKWUH12qto4Ap-WZTVOOG0oo0AU.QX1EDO0wyNyAzNzEzW}`\
I had to search an option which will return the flag. Therefore, naturally I searched for the keyword *flag* with the command `/flag` inside the `man` page and then forwarded the results with `n` key - same as `vim` keybindings. Then I found the argument `--ycxyojt` with the description that it will return the flag when passed to the `/challenge/challenge` command.
```
hacker@man~searching-manuals:~$ man challenge

gzip: stdout: Broken pipe
hacker@man~searching-manuals:~$ /challenge/challenge --ycxyojt
Initializing...
Correct usage! Your flag: pwn.college{AKWUH12qto4Ap-WZTVOOG0oo0AU.QX1EDO0wyNyAzNzEzW}
```


## Searching For Manuals
In this challenge, the manpage for `challenge` command is randomized. But, all the manpages are gathered in a searchable database so you'll be able to search the database to find the challenge's hidden manpage. To figure out how to search for the right manpage, read the manual of `man` command by executing `man man` command.
- HINT 1: `man man` teaches you advanced usage of the man command itself, and you must use this knowledge to figure out how to search for the hidden manpage that will tell you how to use `/challenge/challenge`

- HINT 2: though the manpage is randomly named, you still actually use `/challenge/challenge` to get the flag!
### Solve
**Flag:** `pwn.college{U6GWWZMQv_bKbqcYop7xHpQ0Aa_.QX2EDO0wyNyAzNzEzW}`
- Use the `man man` command to look up the `man` manpage.
- Since I have to look up for something that helps me search a string in a manpage, I find the word ***searching*** by typing `/searching` in the `man` window.
- Was brought to the `man -k <keyword>` command. This searches the short despcriptions (the one-line summaries) of all *available* man pages.
- Typed `man -k challenge` since I wanted `man` to lookup every manual entry containing the word `challenge`.
- > vbbqcopxpa (1)       - print the flag!
- `man vbbqcopxpa` to learn about the given command.
- `--vbbqco NUM` returns the flag when `NUM = 670`.
- And since, we were to run the `/challenge/challenge` command, I ran it with the provided parameters to find the flag.
```
hacker@man~searching-for-manuals:~$ man man
hacker@man~searching-for-manuals:~$ man -k challenge
vbbqcopxpa (1)       - print the flag!
hacker@man~searching-for-manuals:~$ man vbbqcopxpa
hacker@man~searching-for-manuals:~$ /challenge/challenge --vbbqco 670
Correct usage! Your flag: pwn.college{U6GWWZMQv_bKbqcYop7xHpQ0Aa_.QX2EDO0wyNyAzNzEzW}
```


## Helpful Programs
Programs not having a manpage might still tell you how to use them if invoked with the flag `--flag`. Practice reading a program's documentation with `--help`.
### Solve
**Flag:** `pwn.college{QIGRZ3VlSbCJF6O33OaGLrTrPzc.QX3IDO0wyNyAzNzEzW}`
- Ran the `/challenge/challenge --help` command to read about the `challenge` command.
- `-g GIVE_THE_FLAG` will give the flag if correct value of `GIVE_THE_FLAG` is passed.
- `-p` will print the correct value to pass into the `-g` command.
```
hacker@man~helpful-programs:~$ /challenge/challenge --help
usage: a challenge to make you ask for help [-h] [--fortune] [-v] [-g GIVE_THE_FLAG] [-p]

optional arguments:
  -h, --help            show this help message and exit
  --fortune             read your fortune
  -v, --version         get the version number
  -g GIVE_THE_FLAG, --give-the-flag GIVE_THE_FLAG
                        get the flag, if given the correct value
  -p, --print-value     print the value that will cause the -g option to give you the flag
hacker@man~helpful-programs:~$ /challenge/challenge -p
The secret value is: 363
hacker@man~helpful-programs:~$ /challenge/challenge -g 363
Correct usage! Your flag: pwn.college{QIGRZ3VlSbCJF6O33OaGLrTrPzc.QX3IDO0wyNyAzNzEzW}
```


## Help for Builtins
Some commands, rather than being program with manpages and help options, are built into the shell itself. They are called *builtins*. They are invoked just like commands, but the shell handles them internally instead of launching other programs. One such builtin is `help`. Using it without any argument will give a list of available builtins.\
In this challenge, `challenge` is a builtin rather than a command. Lookup its help to figure out the flag.
### Solve
**Flag:** `pwn.college{c5Al2h891UqSkoxeeoG5PD5ZAt3.QX0ETO0wyNyAzNzEzW}`\
Use the provided secret value with the `--secret` flag to get the flag.



## Helpful Programs
Programs not having a manpage might still tell you how to use them if invoked with the flag `--flag`. Practice reading a program's documentation with `--help`.
### Solve
**Flag:** `pwn.college{c5Al2h891UqSkoxeeoG5PD5ZAt3.QX0ETO0wyNyAzNzEzW}`
- Ran the `/challenge/challenge --help` command to read about the `challenge` command.
- `-g GIVE_THE_FLAG` will give the flag if correct value of `GIVE_THE_FLAG` is passed.
- `-p` will print the correct value to pass into the `-g` command.
```
pwn.college{c5Al2h891UqSkoxeeoG5PD5ZAt3.QX0ETO0wyNyAzNzEzW}
```


## Help for Builtins
Some commands, rather than being program with manpages and help options, are built into the shell itself. They are called *builtins*. They are invoked just like commands, but the shell handles them internally instead of launching other programs. One such builtin is `help`. Using it without any argument will give a list of available builtins.\
In this challenge, `challenge` is a builtin rather than a command. Lookup its help to figure out the flag.
### Solve
**Flag:** `pwn.college{c5Al2h891UqSkoxeeoG5PD5ZAt3.QX0ETO0wyNyAzNzEzW}`\
Use the provided secret value with the `--secret` argument to get the flag.
```
hacker@man~help-for-builtins:~$ help challenge
challenge: challenge [--fortune] [--version] [--secret SECRET]
    This builtin command will read you the flag, given the right arguments!
    
    Options:
      --fortune         display a fortune
      --version         display the version
      --secret VALUE    prints the flag, if VALUE is correct

    You must be sure to provide the right value to --secret. That value
    is "c5Al2h89".
hacker@man~help-for-builtins:~$ challenge --secret c5Al2h89
Correct! Here is your flag!
pwn.college{c5Al2h891UqSkoxeeoG5PD5ZAt3.QX0ETO0wyNyAzNzEzW}
```


### New Learnings
- `man`'s `-k` argument is a blessing.
- About *builtins*.



### References
Used the SENSAI - the builtin AI help assistant to get a hint on how to proceed with the `Searching For Manuals` challenge.
