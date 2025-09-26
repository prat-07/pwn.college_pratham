# Data Manipulation

## Translating Characters
In this level, `/challenge/run` will print the flag but will swap the casing of all characters (e.g., A will become a and vice-versa). Can you undo it with `tr` and get the flag?
### Solve
**Flag:** `pwn.college{EJBNKobh_qJoale9d47jQQ1alnd.01MxEzNxwyNyAzNzEzW}`
- Run the `/challenge/run` command.
- Pipe the output to `tr`.
- Pass arguments `[a..zA..A]` `[A..Za..z].`
```
hacker@data~translating-characters:~$ /challenge/run | tr abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz
yOUR CASE-SWAPPED FLAG:
pwn.college{EJBNKobh_qJoale9d47jQQ1alnd.01MxEzNxwyNyAzNzEzW}
```


## Deleting characters
Running `/challenge/run` command will give you the flag but it will be interspersed with decoy characters. Delete them using `tr -d` and get the flag.
### Solve
**Flag:** `pwn.college{wj-xk3mnD_CF4iIopQRv4P1COei.0FNxEzNxwyNyAzNzEzW}`
- run the `/challenge/run` command to see the raw flag.
- decoy characters are `%` and `^` specifically.
- remove them.
```
hacker@data~deleting-characters:~$ /challenge/run
Your character-stuffed flag:
p%w^n%.%col^l%e^%g%e%{^%w^%j%-^x^%k%3%m%n^%D_^%C%F^%4^%i^%I%o%p^%Q%R^%v%4%P1^%C^O^e^%i^%.^0^%F^%N^%xE^%z^N^xw%y^%N%y^A^z^%N%zE^%z^W^%}^%^
hacker@data~deleting-characters:~$ /challenge/run | tr -d %^
Your character-stuffed flag:
pwn.college{wj-xk3mnD_CF4iIopQRv4P1COei.0FNxEzNxwyNyAzNzEzW}
```


## Deleting newlines
In this challenge, we'll inject a bunch of newlines into the flag. Delete them with `tr's -d` flag and the *escaped newline* specification!
### Solve
**Flag:** `pwn.college{g4mR7TL1Q-Ba18eXuyHUtfmxb9i.0VNxEzNxwyNyAzNzEzW}`
- *escape sequence* represent characters that are usually hard to type using keyboard. 
- start with `\` typically. e.g. `\n` is escape sequence for a new-line character.
- they must be passed in *double quotes* to the `tr` command.
```
hacker@data~deleting-newlines:~$ /challenge/run | tr -d "\n"
Your line-split flag: pwn.college{g4mR7TL1Q-Ba18eXuyHUtfmxb9i.0VNxEzNxwyNyAzNzEzW}
```


## Extracting first lines with head
This challenge's `/challenge/pwn` outputs a bunch of data, and you'll need to pipe it through head to grab just the first 7 lines and then pipe them onwards to `/challenge/college,` which will give you the flag if you do this right! Your solution will be a long composite command with two pipes connecting three commands.
### Solve
**Flag:** `pwn.college{4U9lJzzemW9sYljo3BLxW11WExI.0lNxEzNxwyNyAzNzEzW}`
```
hacker@data~extracting-the-first-lines-with-head:~$ /challenge/pwn | head -n 7 | /challenge/college
Congratulations, you piped the right codes!
pwn.college{4U9lJzzemW9sYljo3BLxW11WExI.0lNxEzNxwyNyAzNzEzW}
```


## Extracting specific sections of text
In this challenge, the `/challenge/run` program will give you a bunch of lines with random numbers and single characters (characters of the flag) as columns. Use cut to extract the flag characters, then pipe them to `tr -d "\n"` (like the previous level!) to join them together into a single line. Your solution will look something like `/challenge/run | cut ??? | tr ???`, with the `???` filled out.
### Solve
**Flag:** `pwn.college{QeC2ThVKfNieaJBo1qbnaayyodd.01NxEzNxwyNyAzNzEzW}`
- run `/challenge/run` to see what the raw flag looks like.
- has 2 columns seperated by whitespace.
- first column is random numbers and second one letter of the flag.
- extract second row using `cut`.
- remove *new-line* character using `tr`.
```
hacker@data~extracting-specific-sections-of-text:~$ /challenge/run | cut -d " " -f 2 | tr -d "\n"
pwn.college{QeC2ThVKfNieaJBo1qbnaayyodd.01NxEzNxwyNyAzNzEzW}
```


## Sorting data
In this challenge, there's a file at `/challenge/flags.txt` containing 100 fake flags, with the real flag mixed among them. When sorted alphabetically, the real flag will be at the end (we made sure of this when generating fake flags). Go get it!
### Solve
**Flag:** `pwn.college{0z1p8Emhj8Rk7s_nWRiLOS3Fp6U.0FM0MDOxwyNyAzNzEzW}`
```
hacker@data~sorting-data:~$ sort /challenge/flags.txt
```


### New Learnings
- `tr`
    - *translates* the characters provided in the first argument witht he ones provided in the second one.
    - use `-d` flag followed by characters to delete them.

- `head`
    - by default prints the first 10 lines of the file.
    - `-n NUM` prints the first *NUM* lines.

- `tail`
    - similar to `head`.
    - prints the last lines.

- `cut`
    - extract specific columns
    - `-d` delimiter for column separation.
    - `-f` field number (which column number to extract).

- `sort`
    - orders line alphabetically by default.
    - `-r` to print in reverse order.
    - `-n` for numbers.
    - `-u` prints unique lines only. Remove duplicates.
    - `-R` prints in random order.
