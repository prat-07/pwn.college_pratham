# Chaining Commands

## Chaining with Semicolons
In this level, you must run `/challenge/pwn` and then /challenge/college, chaining them with a semicolon.
### Solve
**Flag:** `pwn.college{46Hv88IIbsL-dUcWUk2YsDq2SNb.QX1UDO0wyNyAzNzEzW}`
```bash
hacker@chaining~chaining-with-semicolons:~$ /challenge/pwn ; /challenge/college
Yes! You chained /challenge/pwn and /challenge/college! Here is your flag:
pwn.college{46Hv88IIbsL-dUcWUk2YsDq2SNb.QX1UDO0wyNyAzNzEzW}
```


## Building on Success
In this challenge, you need to chain the programs `/challenge/first-success` and `/challenge/second` using the `&&` operator. Try running each command separately first to see what happens (which is that you will not get the flag). But if you chain them with `&&,` the flag will appear!
### Solve
**Flag:** `pwn.college{0Ah2GIGVEWvlS5Ca8_Y6vQUM0PO.0lM0MDOxwyNyAzNzEzW}`
```bash
hacker@chaining~building-on-success:~$ /challenge/first-success 
hacker@chaining~building-on-success:~$ /challenge/second 
Error: /challenge/first-success must be successfully chained with 
/challenge/second using &&
hacker@chaining~building-on-success:~$ /challenge/first-success && /challenge/second 
Nice chaining! Flag: pwn.college{0Ah2GIGVEWvlS5Ca8_Y6vQUM0PO.0lM0MDOxwyNyAzNzEzW}
```


## Handling Failure
In this challenge, you need to chain `/challenge/first-failure` and `/challenge/second` using the `||` operator.
### Solve
**Flag:** `pwn.college{sGL9mAF731vxWHnnrNJ4fDHDUE9.01M0MDOxwyNyAzNzEzW}`
```
hacker@chaining~handling-failure:~$ /challenge/first-failure || /challenge/second 
Nice chaining! Flag: pwn.college{sGL9mAF731vxWHnnrNJ4fDHDUE9.01M0MDOxwyNyAzNzEzW}
```


## Your First Shell Script
Same as last level, run `/challenge/pwn` and then `/challenge/college,` but this time in a shell script called `x.sh`, then run it with `bash`!
### Solve
**Flag:** `pwn.college{worRmigPAta2OC5vNW1BNGcO0qE.QXxcDO0wyNyAzNzEzW}`
- Create `x.sh` using `touch`.
- Edit the file using `vim` text editor.
- Write changes and quit
- Execute the script.

> Script content:
```
/challenge/pwn
/challenge/college
```
>Output
```
hacker@chaining~your-first-shell-script:~$ touch x.sh
hacker@chaining~your-first-shell-script:~$ vim x.sh
hacker@chaining~your-first-shell-script:~$ bash x.sh
Great job, you've written your first shell script! Here is the flag:
pwn.college{worRmigPAta2OC5vNW1BNGcO0qE.QXxcDO0wyNyAzNzEzW}
```


## Redirecting Script Output
Like before, you need to create a script that calls the `/challenge/pwn` command followed by the `/challenge/college` command, and pipe the output of the script into a single invocation of the `/challenge/solve` command!
### Solve
**Flag:** `pwn.college{QyBJWryoGDGwykhlrmKe30nfbO3.QX4ETO0wyNyAzNzEzW}`
```
hacker@chaining~redirecting-script-output:~$ touch x.sh
hacker@chaining~redirecting-script-output:~$ code x.sh
[2025-09-28T14:26:56.608Z] info  Wrote default config file to /home/hacker/.config/code-server/config.yaml
hacker@chaining~redirecting-script-output:~$ bash x.sh | /challenge/solve
Correct! Here is your flag:
pwn.college{QyBJWryoGDGwykhlrmKe30nfbO3.QX4ETO0wyNyAzNzEzW}
```


## Executable Shell Scripts
Make a shellscript that will invoke `/challenge/solve,` make it executable, and run it without explicitly invoking `bash!`
### Solve
**Flag:** `pwn.college{QzYP5rWkRgqv-uCHXeeNf1TqUTq.QX0cjM1wyNyAzNzEzW}`

> Script content
```
/challenge/solve
```
> Output
```
hacker@chaining~executable-shell-scripts:~$ touch x.sh
hacker@chaining~executable-shell-scripts:~$ vim x.sh
hacker@chaining~executable-shell-scripts:~$ chmod +x x.sh
hacker@chaining~executable-shell-scripts:~$ ./x.sh
Congratulations on your shell script execution! Your flag:
pwn.college{QzYP5rWkRgqv-uCHXeeNf1TqUTq.QX0cjM1wyNyAzNzEzW}
```


## Understanding Shebangs
For this challenge, create a script at `/home/hacker/solve.sh` that has a proper *shebang* and outputs "hack the planet". Remember to make it executable, then run `/challenge/run` to verify your script works correctly!

> Script content
```bash
#!/bin/bash

echo "hack the planet"
```
> Output
```
hacker@chaining~understanding-shebangs:~$ touch solve.sh
hacker@chaining~understanding-shebangs:~$ vim solve.sh
hacker@chaining~understanding-shebangs:~$ chmod a+x solve.sh
hacker@chaining~understanding-shebangs:~$ /challenge/run
Testing your script...
Perfect! Your flag:
Flag: pwn.college{YUXGDjdPEDmo2lpsniaHg4r_lkB.0VOzMDOxwyNyAzNzEzW}
```


## Scripting with Arguments
For this challenge, you need to write a script at `/home/hacker/solve.sh` that:

- Takes two arguments
- Outputs them in REVERSE order (second argument first, then the first argument)

Then run `/challenge/run` command to get the flag.
### Solve
**Flag:** `pwn.college{MHVkxJRG1lCYi_5aGGW1P7yOvts.0VNzMDOxwyNyAzNzEzW}`
> Script content
```bash
#!/bin/bash

echo $2 $1
```
> Output
```
hacker@chaining~scripting-with-arguments:~$ touch solve.sh
hacker@chaining~scripting-with-arguments:~$ code solve.sh
hacker@chaining~scripting-with-arguments:~$ bash solve.sh pwn college
college pwn
hacker@chaining~scripting-with-arguments:~$ /challenge/run
Correct! Your script properly reversed the arguments.
Here's your flag:
pwn.college{MHVkxJRG1lCYi_5aGGW1P7yOvts.0VNzMDOxwyNyAzNzEzW}
```


## Scripting with Conditionals
For this challenge, write a script at `/home/hacker/solve.sh` that:

- Takes one argument
- If the argument is "pwn", output "college"
- For any other input, output nothing

Once the script runs correctly, run `/challenge/run` to get the flag.
### Solve
**Flag:** `pwn.college{8BzEe5aPQ4C-hBWM6pdDQesUjpa.0lNzMDOxwyNyAzNzEzW}`
> Script content
```bash
#!/bin/bash

if [ "$1" == "pwn" ]
then
    echo "college"
fi
```
> Output
```
hacker@chaining~scripting-with-conditionals:~$ bash solve.sh pwn
college
hacker@chaining~scripting-with-conditionals:~$ bash solve.sh asdfj
hacker@chaining~scripting-with-conditionals:~$ /challenge/run
Correct! Your script properly handles all the conditions.
Here's your flag:
pwn.college{8BzEe5aPQ4C-hBWM6pdDQesUjpa.0lNzMDOxwyNyAzNzEzW}
```


## Scripting with Default Cases
For this challenge, write a script at /home/hacker/solve.sh that:

- Takes one argument
- If the argument is "pwn", output "college"
- For any other input, output "nope"

Once the script works, run `/challenge/run` to get the flag.
### Solve
**Flag:** `pwn.college{k_ggiQn4oGuqA0lOnorky-zkdxb.01NzMDOxwyNyAzNzEzW}`
> Script content
```bash
#!/bin/bash

if [ "$1" == "pwn" ]
then
    echo "college"
else
    echo "nope"
fi
```
> Output
```
hacker@chaining~scripting-with-default-cases:~$ ls
 COLLEGE   Desktop   PWN   a   instructions   msg   myflag   not-the-flag   processes   solve.sh   the-flag   x.sh  '~'
hacker@chaining~scripting-with-default-cases:~$ bash solve.sh pwn
college
hacker@chaining~scripting-with-default-cases:~$ bash solve.sh alkj
nope
hacker@chaining~scripting-with-default-cases:~$ /challenge/run
Correct! Your script properly handles the if/else conditions.
Here's your flag:
pwn.college{k_ggiQn4oGuqA0lOnorky-zkdxb.01NzMDOxwyNyAzNzEzW}
```


## Scripting with Multiple Conditions
For this challenge, write a script at /home/hacker/solve.sh that:

- Takes one argument
- If the argument is "hack", output "the planet"
- If the argument is "pwn", output "college"
- If the argument is "learn", output "linux"
- For any other input, output "unknown"

Once the script runs correctly, run `/challenge/run` to get the flag.
### Solve
**Flag:** `pwn.college{8lfW790Aq802-6yGmCTGH96wKVl.0FOzMDOxwyNyAzNzEzW}`
> Script content
```bash
#!/bin/bash

if [ "$1" == "hack" ]
then
    echo "the planet"
elif [ "$1" == "pwn" ]
then
    echo "college"
elif [ "$1" == "learn" ]
then
    echo "linux"
else
    echo "unknown"
fi
```
> Output
```
hacker@chaining~scripting-with-multiple-conditions:~$ /challenge/run
Correct! Your script properly handles all the conditions with elif.
Here's your flag:
pwn.college{8lfW790Aq802-6yGmCTGH96wKVl.0FOzMDOxwyNyAzNzEzW}
```

## Reading Shell Scripts
In this level, we will learn to read shell scripts. `/challenge/run` is a shell script that requires you to put in a secret password, but that password is hardcoded into the script iself! Read the script (using, say, `cat`), figure out the password, and get the flag!
### Solve
**Flag:** `pwn.college{UR4vKquAHS46SSgog3sk1j8xICS.0lMwgDOxwyNyAzNzEzW}`\
Something to be careful about. This file seems to take input after running it and not as an argument.
> Script content
```bash
#!/opt/pwn.college/bash

read GUESS
if [ "$GUESS" == "hack the PLANET" ]
then
        echo "CORRECT! Your flag:"
        cat /flag
else
        echo "Read the /challenge/run file to figure out the correct password!"
fi
```
> Output
```
hacker@chaining~reading-shell-scripts:~$ /challenge/run
hack the PLANET
CORRECT! Your flag:
pwn.college{UR4vKquAHS46SSgog3sk1j8xICS.0lMwgDOxwyNyAzNzEzW}
```



### New Learnings
- `;`
    - Run multiple commands in succession after one another.
- `&&`
    - Runs the second command only if the first one is executed successfully.
- `||`
    - Runs the second command only if the first one is *NOT* executed successfully.
- `bash` command 
    - Running scripts as an arugument to `bash` command means it reads commands from file rather from input.
- `shebang`
    - first line of the script
    - tells the system which interpreter to use.
    - e.g. `#!/bin/bash` tell the system to run the script with bash no matter the default shell.

