# Terminal Multiplexing

## Launching Screen
For this challenge, we've hooked things up so that just launching `screen` will get you the flag.
### Solve
**Flag:** `pwn.college{IliC7qKwAqKlJ65i_Rx4KK9PMXh.0VN4IDOxwyNyAzNzEzW}`
- Type `screen`
- Hit `enter` to return back to terminal
```
Congratulations! You're inside a screen session!
Here's your flag:
pwn.college{IliC7qKwAqKlJ65i_Rx4KK9PMXh.0VN4IDOxwyNyAzNzEzW}
hacker@terminal-multiplexing~launching-screen:~$
```


## Detaching and Attaching
For this challenge, you'll need to:
- Launch `screen`
- Detach from it.
- Run `/challenge/run` (this will secretly send the flag to your detached session!)
- Reattach to see your prize

### Solve
**Flag:** `pwn.college{oqhjBgxLFRPFwD-b2cMlC_IBkXC.0lN4IDOxwyNyAzNzEzW}`
- run `screen`
- detach using `(Ctrl+a) + d`
- run `/challenge/run` in normal terminal
- reattach using `screen -r`


## Finding Sessions
In this challenge, we've created three screen sessions for you. One of them contains the flag. The other two are decoys! You'll need to check each one until you find it.
### Solve
**Flag:** `pwn.college{crsfTk8hBdllDwHXfbqmGsIdFXD.01N4IDOxwyNyAzNzEzW}`\
Fortunately, the first session itself contained the flag.
> terminal output
```
hacker@terminal-multiplexing~finding-sessions:~$ screen -ls
There are screens on:
        158.pts-0.terminal-multiplexing~launching-screen        (Remote or dead)
        147.pts-0.terminal-multiplexing~detaching-and-attaching (Remote or dead)
        145.session_49918054b4a5687a    (Detached)
        148.session_b79f8cf9a81a4738    (Detached)
        151.session_cd3b33c52fcabf98    (Detached)
5 Sockets in /home/hacker/.screen.
hacker@terminal-multiplexing~finding-sessions:~$ screen -r 145
```
> screen output
```
hacker@terminal-multiplexing~finding-sessions:~$  echo 'Congratulations! You found the right session!'
Congratulations! You found the right session!
hacker@terminal-multiplexing~finding-sessions:~$  echo pwn.college{crsfTk8hBdllDwHXfbqmGsIdFXD.01N4IDOxwyNyAzNzEzW}
pwn.college{crsfTk8hBdllDwHXfbqmGsIdFXD.01N4IDOxwyNyAzNzEzW}
hacker@terminal-multiplexing~finding-sessions:~$
```


## Switching Windows
For this challenge, we've set up a screen session with two windows:

- Window 0 has... well, you'll have to switch there to find out!
- Window 1 has a welcome message

Attach to the session with screen -r, then use one of the key combinations above to switch to Window 1. Go get that flag!
### Solve
**Flag:** `pwn.college{4c6qcvLg_KpG_nmvPPFGLHJnozN.0FO4IDOxwyNyAzNzEzW}`
> terminal
```
hacker@terminal-multiplexing~switching-windows:~$ screen -ls
There are screens on:
        158.pts-0.terminal-multiplexing~launching-screen        (Remote or dead)
        147.pts-0.terminal-multiplexing~detaching-and-attaching (Remote or dead)
        145.session_49918054b4a5687a    (Remote or dead)
        148.session_b79f8cf9a81a4738    (Remote or dead)
        151.session_cd3b33c52fcabf98    (Remote or dead)
        135.challenge_session   (Detached)
6 Sockets in /home/hacker/.screen.
hacker@terminal-multiplexing~switching-windows:~$ screen -r
[detached from 135.challenge_session]
```
> screen window 1
```
hacker@terminal-multiplexing~switching-windows:~$  cat <<MSG
> Welcome to the window switching challenge!
> You are currently in window 1.
> The flag is hidden in window 0.
> Use Ctrl-A 0 to switch to window 0!
> MSG
Welcome to the window switching challenge!
You are currently in window 1.
The flag is hidden in window 0.
Use Ctrl-A 0 to switch to window 0!
```
> screeen window 2
```
hacker@terminal-multiplexing~switching-windows:~$  cat <<MSG
> Excellent work! You found window 0!
> Here is your flag: pwn.college{4c6qcvLg_KpG_nmvPPFGLHJnozN.0FO4IDOxwyNyAzNzEzW}
> MSG
Excellent work! You found window 0!
Here is your flag: pwn.college{4c6qcvLg_KpG_nmvPPFGLHJnozN.0FO4IDOxwyNyAzNzEzW}
```


## Detaching and Attaching (tmux)
For this challenge:

- Launch tmux
- Detach from it.
- Run /challenge/run (this will send the flag to your detached session!)
- Reattach to see your prize
### Solve
**Flag:** `pwn.college{4DbkogbaY7F3LhtEuL9tDg8riip.0VO4IDOxwyNyAzNzEzW}`
> terminal
```
hacker@terminal-multiplexing~detaching-and-attaching-tmux:~$  echo Congratulations, here is your flag: pwn.college{4DbkogbaY7F3LhtEuL9tDg8riip.0VO4IDOxwyNyAzNzEzW}
Congratulations, here is your flag: pwn.college{4DbkogbaY7F3LhtEuL9tDg8riip.0VO4IDOxwyNyAzNzEzW}
```
> tmux
```
hacker@terminal-multiplexing~detaching-and-attaching-tmux:~$  echo Congratulations, here is your flag: pwn.college{4DbkogbaY7F3LhtEuL9tDg8riip.0VO4IDOxwyNyAzNzEzW}
Congratulations, here is your flag: pwn.college{4DbkogbaY7F3LhtEuL9tDg8riip.0VO4IDOxwyNyAzNzEzW}
```


## Switching Windows (tmux)
We've created a tmux session with two windows:

- Window 0 has the flag!
- Window 1 has your warm welcome.

Go get that flag!
### Solve
**Flag:** `pwn.college{Mpr6xAqa4WtBplpSiZx0n5Hua9h.0FM5IDOxwyNyAzNzEzW}`
> terminal
```
hacker@terminal-multiplexing~switching-windows-tmux:~$ tmux ls
challenge_session: 2 windows (created Mon Sep 29 03:27:32 2025)
hacker@terminal-multiplexing~switching-windows-tmux:~$ tmux a
[detached (from session challenge_session)]
```
> window 1
```
 cat <<MSG
Welcome to the tmux window switching challenge!
You are currently in window 1.
The flag is hidden in window 0.
Use Ctrl-B 0 to switch to window 0!
MSG
hacker@terminal-multiplexing~switching-windows-tmux:~$  cat <<MSG
> Welcome to the tmux window switching challenge!
> You are currently in window 1.
> The flag is hidden in window 0.
> Use Ctrl-B 0 to switch to window 0!
> MSG
Welcome to the tmux window switching challenge!
You are currently in window 1.
The flag is hidden in window 0.
Use Ctrl-B 0 to switch to window 0!
```
> window 0
```
hacker@terminal-multiplexing~switching-windows-tmux:~$  cat <<MSG
> Excellent work! You found window 0!
> Here is your flag: pwn.college{Mpr6xAqa4WtBplpSiZx0n5Hua9h.0FM5IDOxwyNyAzNzEzW}
> MSG
Excellent work! You found window 0!
Here is your flag: pwn.college{Mpr6xAqa4WtBplpSiZx0n5Hua9h.0FM5IDOxwyNyAzNzEzW}
```


### New Learnings
`Terminal Multiplexing`
- It is like splitting one physical terminal into many virtual ones.
- What?
    - A terminal multiplexer like `tmux` or `screen` lets you run multiple shells inside a single terminal window or remote SSH session. Each shell can be openned, closed or switched between without leaving the session. Screen can also be split into panes.
- Why?
    - Manage multiple tasks without opening many terminal windows.
    - Keeps your work alive if you disconnect (important for SSH).

