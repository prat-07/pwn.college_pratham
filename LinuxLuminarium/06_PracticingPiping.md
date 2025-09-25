# Practicing Piping

## Redirecting output
In this challenge, you must use this output redirection to write the word `PWN` (all uppercase) to the filename `COLLEGE` (all uppercase).
### Solve
**Flag:** `pwn.college{c4lw-Fwqvw4SaZYLJmVd41qfi8f.QX0YTN0wyNyAzNzEzW}`
```
hacker@piping~redirecting-output:~$ echo PWN > COLLEGE
Correct! You successfully redirected 'PWN' to the file 'COLLEGE'! Here is your 
flag:
pwn.college{c4lw-Fwqvw4SaZYLJmVd41qfi8f.QX0YTN0wyNyAzNzEzW}
```


## Redirecting more output
In this level, `/challenge/run` will once more give you a flag, but only if you redirect its output to the file `myflag`. Your flag will, of course, end up in the `myflag` file!
### Solve
**Flag:** `pwn.college{wMXNG4WSUOHJnJmCgDdbicdG3ZC.QX1YTN0wyNyAzNzEzW}`\
It is important that we cat the `myflag` after redirecting output to it.
```
hacker@piping~redirecting-more-output:~$ /challenge/run > myflag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : myflag
[INFO] - the challenge will output a reward file if all the tests pass : /flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /flag file.

[TEST] You should have redirected my stdout to a file called myflag. Checking...

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~redirecting-more-output:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{wMXNG4WSUOHJnJmCgDdbicdG3ZC.QX1YTN0wyNyAzNzEzW}
```



## Appending output
To practice, run `/challenge/run` with an append-mode redirect of the output to the file `/home/hacker/the-flag.` The practice will write the first half of the flag to the file, and the second half to stdout if stdout is redirected to the file. If you properly redirect in append-mode, the second half will be appended to the first, but if you redirect in truncation mode (>), the second half will overwrite the first and you won't get the flag!
### Solve
**Flag:** `pwn.college{8FcTDLco6Otylg9ArlKvnCn0fmC.QX3ATO0wyNyAzNzEzW}`\
I had to run the command `/challenge/run` 2 times to get two parts of the flag. First redirect the `stdout` to the `the-flag` file in `~` dir, then the next time by appending to the same file using `>>` instead of `>`.
```
hacker@piping~appending-output:~$ /challenge/run > ~/the-flag
hacker@piping~appending-output:~$ /challenge/run  >> ~/the-flag
hacker@piping~appending-output:~$ cat ~/the-flag 
 | 
\|/ This is the first half:
 v 
pwn.college{8FcTDLco6Otylg9ArlKvnCn0fmC.QX3ATO0wyNyAzNzEzW}
                              ^
     that is the second half /|\
                              |

If you only see the second half above, you redirected in *truncate* mode (>) 
rather than *append* mode (>>), and so the write of the second half to stdout 
overwrote the initial write of the first half directly to the file. Try append 
mode!
```


## Redirecting errors
In this challenge, you will need to redirect the output of `/challenge/run,` like before, to `myflag`, and the "errors" (in our case, the instructions) to `instructions`.
### Solve
**Flag:** `pwn.college{IhGY2rrS4eoSpd2T8SAcKhWB6UA.QX3YTN0wyNyAzNzEzW}`
```
hacker@piping~redirecting-errors:~$ /challenge/run > myflag 2> instructions
hacker@piping~redirecting-errors:~$ cat myflag 

[FLAG] Here is your flag:
[FLAG] pwn.college{IhGY2rrS4eoSpd2T8SAcKhWB6UA.QX3YTN0wyNyAzNzEzW}
```


## Redirecting input
You can redirect input *to* programs using the `<` symbol.\
In this level, we will practice using `/challenge/run,` which will require you to redirect the `PWN` file to it and have the `PWN` file contain the value `COLLEGE`! 
### Solve
**Flag:** `pwn.college{4eKbTirUQ99wxU0CdoeRJ-A54Nt.QXwcTN0wyNyAzNzEzW}`\
First redirect output of `echo COLLEGE` to `PWN` file and pass that file as an input to the specified command.
```
hacker@piping~redirecting-input:~$ echo COLLEGE > PWN
hacker@piping~redirecting-input:~$ /challenge/run < PWN
Reading from standard input...
Correct! You have redirected the PWN file into my standard input, and I read 
the value 'COLLEGE' out of it!
Here is your flag:
pwn.college{4eKbTirUQ99wxU0CdoeRJ-A54Nt.QXwcTN0wyNyAzNzEzW}
```


## Grepping stored results
1. Redirect the output of `/challenge/run` to `/tmp/data.txt.`
2. This will result in a hundred thousand lines of text, with one of them being the flag, in `/tmp/data.txt.`
3. `grep` that for the flag!
### Solve
**Flag:** `pwn.college{kKTQ22Ox6ucHTAnDVz-eKvhlQnm.QX4EDO0wyNyAzNzEzW}`\
Since the flag has the format `pwn.college{random-string}`, we simply pass the argument `pwn.college{` to the grep command and the file-path.
```
hacker@piping~grepping-stored-results:~$ /challenge/run > /tmp/data.txt
hacker@piping~grepping-stored-results:~$ grep pwn.college{ /tmp/data.txt
pwn.college{kKTQ22Ox6ucHTAnDVz-eKvhlQnm.QX4EDO0wyNyAzNzEzW}
```


## Grepping live output
You can pass the output of command directly to another command using the pipe `|` operator.
`/challenge/run` will output a hundred thousand lines of text, including the flag. `grep` for the flag!
### Solve
**Flag:** `pwn.college{kdd2YG_yKG5OHEjIQnxPxcYw6gk.QX5EDO0wyNyAzNzEzW}`
```
hacker@piping~grepping-live-output:~$ /challenge/run | grep "pwn.college"
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stdout : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/8b4vn1iyn6kqiisjvlmv67d1c0p3j6wj-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stdout!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{kdd2YG_yKG5OHEjIQnxPxcYw6gk.QX5EDO0wyNyAzNzEzW}
```


## Grepping errors
 Like the last level, this level will overwhelm you with output, but this time on standard error. `grep` through it to find the flag!
 ### Solve
 **Flag:** `pwn.college{YN8EJIowXhAlT2pk6tQxMU33ZqC.QX1ATO0wyNyAzNzEzW}`\
- `2>` means redirect the stderr.
- `>&` will redirect one file descriptor to another.
- Thus, we use `2>& 1` which will redirect the stderr to stdout.
```
hacker@piping~grepping-errors:~$ /challenge/run 2>& 1 | grep "pwn.college"
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stderr : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stderr to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/8b4vn1iyn6kqiisjvlmv67d1c0p3j6wj-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stderr!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{YN8EJIowXhAlT2pk6tQxMU33ZqC.QX1ATO0wyNyAzNzEzW}
```


## Filtering with grep -v
In this challenge, `/challenge/run` will output the flag to stdout, but it will also output over 1000 decoy flags (containing the word `DECOY` somewhere in the flag) mixed in with the real flag. You'll need to filter out the decoys while keeping the real flag!
### Solve
**Flag:** `pwn.college{4M-8rt2cWyWEKs5swrkV8gyXqg4.0FOxEzNxwyNyAzNzEzW}`\
```
hacker@piping~filtering-with-grep-v:~$ /challenge/run | grep -v "DECOY"
pwn.college{4M-8rt2cWyWEKs5swrkV8gyXqg4.0FOxEzNxwyNyAzNzEzW}
```


## Duplicating piped data with tee
This process' `/challenge/pwn` must be piped into `/challenge/college,` but you'll need to intercept the data to see what pwn needs from you!
### Solve
**Flag:** `pwn.college{ITSBR4aE2DmorwzrzY04ZjuL0Hq.QXxITO0wyNyAzNzEzW}`
- Intercept stdout of `/challenge/pwn` by `tee`.
- `cat` the file.
- Pass the `--secret [secret-value]` argument to the `/challenge/pwn` command as specified while piping the output to `/challenge/college`.
```
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn | tee msg | /challenge/college 
Processing...
WARNING: you are overwriting file msg with tee's output...
The input to 'college' does not contain the correct secret code! This code 
should be provided by the 'pwn' command. HINT: use 'tee' to intercept the 
output of 'pwn' and figure out what the code needs to be.
hacker@piping~duplicating-piped-data-with-tee:~$ cat msg
Usage: /challenge/pwn --secret [SECRET_ARG]

SECRET_ARG should be "ITSBR4aE"
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn --secret ITSBR4aE | /challenge/college 
Processing...
Correct! Passing secret value to /challenge/college...
Great job! Here is your flag:
pwn.college{ITSBR4aE2DmorwzrzY04ZjuL0Hq.QXxITO0wyNyAzNzEzW}
```


## Process substitution for input
Now, you'll diff two sets of command outputs: `/challenge/print_decoys`, which will print a bunch of decoy flags, and `/challenge/print_decoys_and_flag` which will print those same decoys plus the real flag.\
Use process substitution with `diff` to compare the outputs of these two programs and find your flag!
### Solve
**Flag:** `pwn.college{srS-x3SXSQWfrKeXVo7HMt1DHaQ.0lNwMDOxwyNyAzNzEzW}`\
- `<(command)` will create a temp file and simultaneously return its path. The file is connected to the stdin of the `command` command.
- Thus, we `diff` these two files to find the flag.
```
hacker@piping~process-substitution-for-input:~$ diff <(/challenge/print_decoys) <(/challenge/print_decoys_and_flag)
63a64
> pwn.college{srS-x3SXSQWfrKeXVo7HMt1DHaQ.0lNwMDOxwyNyAzNzEzW}
```


## Writing to multiple programs
In this challenge, we have `/challenge/hack`, `/challenge/the`, and `/challenge/planet.` Run the `/challenge/hack` command, and duplicate its output as input to both the `/challenge/the` and the `/challenge/planet` commands! Scroll back through the previous challenges "Duplicating piped data with tee" and "Process substitution for input" if you need a refresher on this method.
### Solve
**Flag:** `pwn.college{cZf52fhh-NWBA0tozzzKVjprCts.QXwgDN1wyNyAzNzEzW}`\
```
hacker@piping~writing-to-multiple-programs:~$ /challenge/hack | tee >(/challenge/the) | tee >(/challenge/planet)
This secret data must directly and simultaneously make it to /challenge/the and 
/challenge/planet. Don't try to copy-paste it; it changes too fast.
1198923354221444444
Congratulations, you have duplicated data into the input of two programs! Here 
is your flag:
pwn.college{cZf52fhh-NWBA0tozzzKVjprCts.QXwgDN1wyNyAzNzEzW}
```


## Split-piping stderr and stdout
In this challenge, you have:
- `/challenge/hack` : this produces data on stdout and stderr
- `/challenge/the` : you must redirect hack's stderr to this program
- `/challenge/planet` : you must redirect hack's stdout to this program
### Solve
**Flag:** `pwn.college{Qs59dZfNSIcGWhNyTnY_6xQrKe0.QXxQDM2wyNyAzNzEzW}`\
- Pass stderr of first command to second one and stdout of first command to stdout of second one. I did this by using knowledge of previous challenge - *File Descriptors*.
- And since I had to pass it to two commands, I made use of *Process Substitution*.
```
hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/hack 2> >(/challenge/the) > >(/challenge/planet)
Congratulations, you have learned a redirection technique that even experts 
struggle with! Here is your flag:
pwn.college{Qs59dZfNSIcGWhNyTnY_6xQrKe0.QXxQDM2wyNyAzNzEzW}
```


## Named pipes
This challenge will be a simple introduction to FIFOs. You'll need to create a `/tmp/flag_fifo` file and redirect the stdout of `/challenge/run` to it. If you're successful, `/challenge/run` will write the flag into the FIFO! Go do it!
### Solve
**Flag:** `pwn.college{cU0UqHCIzE8kZUoxmWY9CkGUSaz.01MzMDOxwyNyAzNzEzW}`\
- Create the FIFO.
- Redirect output of `/challenge/run` to it.
- Proccesses paused until *read* action is completed.
- Open new terminal and read the FIFO.
```
hacker@piping~named-pipes:~$ mkfifo /tmp/flag_fifo
mkfifo: cannot create fifo '/tmp/flag_fifo': File exists
hacker@piping~named-pipes:~$ /challenge/run > /tmp/flag_fifo
You're successfully redirecting /challenge/run to a FIFO at /tmp/flag_fifo! 
Bash will now try to open the FIFO for writing, to pass it as the stdout of 
/challenge/run. Recall that operations on FIFOs will *block* until both the 
read side and the write side is open, so /challenge/run will not actually be 
launched until you start reading from the FIFO!

hacker@piping~named-pipes:~$ cat /tmp/flag_fifo 
You've correctly redirected /challenge/run's stdout to a FIFO at 
/tmp/flag_fifo! Here is your flag:
pwn.college{cU0UqHCIzE8kZUoxmWY9CkGUSaz.01MzMDOxwyNyAzNzEzW}
```


### New Learnings
- `>` passes the stdout of the command left to it to the file right of it.
    - will create a new file if it does not exist yet.
    - if the same file used, will always delete its old contents.
- `>>` will append to the file rather than rewriting it everytime.
- `File Descriptors`
    - `0` - stdin.
    - `1` - stdout.
    - `2` - stderr.

- `|` is used to pass the stdout of one command as stdin to other.
- `>&` is used to pass different File Descriptors as arguments to one another.
- `grep -v` will return all results *except* matching the string to its right.
- `tee` duplicates data flowing through pipes.
- ***Process Substitution*** is a shell feature that lets you treat output or input of a command as if it were a file.
    - `<(command)` gives a file-like input containing the output of command.
    - `>(command)` sends output into the stdin of `command`.
- ***FIFO pipe*** are persistent pipes unlike files created by process-substitution which are temp.
    - One process can open FIFO for reading and other for writing.
    - Process incomplete until both of them are done.
    - Can be used in either order - read and write or - write and read.
    - Advantages:
        - No disk storage.
        - Data gone once read.

