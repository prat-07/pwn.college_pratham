# File Globbing

## Matching with *
Starting from the home directory, change the directory to `/challenge` but the path passed to cd must be at most 4 characters long. After in the `/challenge` dir, run the `/challenge/run` command to get the flag.
### Solve
**Flag:** `pwn.college{0TXvKtoRkshmBwt4JasJ7OKpOXF.QXxIDO0wyNyAzNzEzW}`
```
hacker@globbing~matching-with-:~$ cd /cha*
You specified the path to 'cd' to in more than 4 characters. Disallowed!
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
hacker@globbing~matching-with-:~$ cd /ch*
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{0TXvKtoRkshmBwt4JasJ7OKpOXF.QXxIDO0wyNyAzNzEzW}
```


## Matching with ?
Starting from your home directory, change your directory to `/challenge`, but use the `?` character instead of `c` and `l` in the argument to cd! Once you're there, run `/challenge/run` for the flag!
### Solve
**Flag:** `pwn.college{wUrEk07wtqqIvW-2_aajVN5Mlo3.QXyIDO0wyNyAzNzEzW}`
```
hacker@globbing~matching-with-:~$ cd /?ha??enge
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{wUrEk07wtqqIvW-2_aajVN5Mlo3.QXyIDO0wyNyAzNzEzW}
```


## Matching with [ ]
We've placed a bunch of files in `/challenge/files.` Change your working directory to `/challenge/files` and run `/challenge/run` with a single argument that bracket-globs into `file_b,` `file_a,` `file_s,` and `file_h!`
### Solve
**Flag:** `pwn.college{U-rkrLnqSKgOivP7JgIg72jS1hj.QXzIDO0wyNyAzNzEzW}`
```
hacker@globbing~matching-with-:~$ cd /challenge/files
hacker@globbing~matching-with-:/challenge/files$ /challenge/run file_[bash]
You got it! Here is your flag!
pwn.college{U-rkrLnqSKgOivP7JgIg72jS1hj.QXzIDO0wyNyAzNzEzW}
```


## Matching paths with [ ]
Once more, we've placed a bunch of files in `/challenge/files.` Starting from your home directory, run `/challenge/run` with a single argument that bracket-globs into the absolute paths to the `file_b`, `file_a`, `file_s`, and `file_h` files!
### Solve
**Flag:** `pwn.college{kbbPpfwmmC-qM5D9uBeRJ3wSH7N.QX0IDO0wyNyAzNzEzW}`
```
hacker@globbing~matching-paths-with-:~$ /challenge/run /challenge/files/file_[bash]
You got it! Here is your flag!
pwn.college{kbbPpfwmmC-qM5D9uBeRJ3wSH7N.QX0IDO0wyNyAzNzEzW}
```


## Multiple globs
We put a few happy, but diversely-named files in `/challenge/files.` Go `cd` there and run `/challenge/run,` providing a single argument: a short (3 characters or less) globbed word with two `*` globs in it that covers every word that contains the letter `p`.
## Solve
**Flag:** `pwn.college{EE4xouUGNE8jNgkZc07fhthdy49.0lM3kjNxwyNyAzNzEzW}`
```
hacker@globbing~multiple-globs:~$ cd /challenge/files
hacker@globbing~multiple-globs:/challenge/files$ /challenge/run *p*
You got it! Here is your flag!
pwn.college{EE4xouUGNE8jNgkZc07fhthdy49.0lM3kjNxwyNyAzNzEzW}
```


## Mixing globs
We put a few happy, but diversely-named files in `/challenge/files.` Go `cd` there and, using the globbing you've learned, write a single, short (6 characters or less) glob that (when passed as an argument to `/challenge/run`) will match the files "challenging", "educational", and "pwning"!
### Solve
**Flag:** `pwn.college{4V2ynX4rMg0A1QcQK6brcH7VeJ8.QX1IDO0wyNyAzNzEzW}`\
I tried running the command with the argument `*[nal]` but that contained too many files so I adjusted the argument with the following one:
```
hacker@globbing~mixing-globs:~$ cd /challenge/files
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [cep]*
You got it! Here is your flag!
pwn.college{4V2ynX4rMg0A1QcQK6brcH7VeJ8.QX1IDO0wyNyAzNzEzW}
```


## Exclusionary globbing
Go forth to `/challenge/files` and run `/challenge/run` with all files that don't start with `p`, `w`, or `n`!
### Solve
**Flag:** `pwn.college{Yrq0-6GsXi1FgwfZQV2dgiDqyLr.QX2IDO0wyNyAzNzEzW}`\
Remember: `!` has a different meaning if not the first character in `[]`. If you get an unexpected output, use `^` but keep in mind that it is not compatible with older versions of bash.\
*Nobody uses older version.* :P
```
hacker@globbing~exclusionary-globbing:~$ cd /challenge/files
hacker@globbing~exclusionary-globbing:/challenge/files$ /challenge/run [^pwn]*
You got it! Here is your flag!
pwn.college{Yrq0-6GsXi1FgwfZQV2dgiDqyLr.QX2IDO0wyNyAzNzEzW}
```


## Tab completion
This challenge has copied the flag into `/challenge/pwncollege,` and you can freely cat that file. But you can't type the filename: we used some serious trickery to make sure that you must tab-complete it.
### Solve
**Flag:** `pwn.college{QF6KNcD2P3BXxx86R24qGPKrAlA.0FN0EzNxwyNyAzNzEzW}`
```
hacker@globbing~tab-completion:~$ cd /challenge/
hacker@globbing~tab-completion:/challenge$ ls
DESCRIPTION.md  pwncollege​
hacker@globbing~tab-completion:/challenge$ cat /challenge/pwncollege​ 
pwn.college{QF6KNcD2P3BXxx86R24qGPKrAlA.0FN0EzNxwyNyAzNzEzW}
```


## Multiple options for tab completion
This challenge has a `/challenge/files` directory with a bunch of files starting with `pwncollege`. Tab-complete from `/challenge/files/p` or so, and make your way to the flag!
### Solve
**Flag:** `pwn.college{MaR-FoyeBP1PAup_t9LpxlJ1lcq.0lN0EzNxwyNyAzNzEzW}`\
I listed out the multiple files in the specified directory using tab completion and `cat`ed the `pwncollege-flag` file.
```
hacker@globbing~multiple-options-for-tab-completion:~$ cat /challenge/files/pwn
pwn                    pwn-the-planet         pwncollege-flag        pwncollege-flyswatter  
pwn-college            pwncollege-family      pwncollege-flamingo    pwncollege-hacking     
hacker@globbing~multiple-options-for-tab-completion:~$ cat /challenge/files/pwncollege-flag
pwn.college{MaR-FoyeBP1PAup_t9LpxlJ1lcq.0lN0EzNxwyNyAzNzEzW}
```


## Tab completion on commands
This level has a command that starts with `pwncollege`, and it'll give you the flag. Type `pwncollege` and hit the tab key to auto-complete it!
### Solve
**Flag:** `pwn.college{4eVGEWiroUs1VvZDUHhK4jk4wtz.0VN0EzNxwyNyAzNzEzW}`\
I typed `pwncollege` and then hit `tab` as specified.
```
hacker@globbing~tab-completion-on-commands:~$ pwncollege-17918 
Correct! Here is your flag:
pwn.college{4eVGEWiroUs1VvZDUHhK4jk4wtz.0VN0EzNxwyNyAzNzEzW}
```


### New Learnings
File Globbing is the process of pattern matching file and dir names using special wildcard characters, instead of typing out exact names.\
It helps in pinpointing exact commands and files if you do not remember them exactly as they were.
- `*` - wildcard. Matches everything, even *nothing*.
- `?` - matches exactly one character.
- `[]` - matches multiple characters.
- `[^abc]` - matches everything *except* the strings containing `abc`.
- `tab` - used for autocompletion.
