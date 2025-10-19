# Randomly Accessed Memories

## Challenge Description
On your ascent to this floor, you hear these fragments being played back —

```
clone it, pull it, reset it, stage it, 
commit, push it, fork, rebase it. 
merge it, branch it, tag it, log it, 
add it, stash it, diff, untrack it … 
```

You look around and discover a chamber containing a vast archive of Daft Punk’s music, intertwined with cryptic commits left behind by other musicians. They seem ordinary at first glance, but not everything in the history is what it seems. The archive: https://github.com/evilcryptonite/daft-punk-archive

## Solve
**Flag:** `citadel{w3_4r3_up_4ll_n1t3_t0_g1t_lucky}`
- Clicking on the link, we are redirected to a github repo. I clone the repo.
- Since this challenge has to do something with git, I look at `git log`.
- I use the grep command to search for the keyword `flag`.
- I see 3 files. After going back to the specified commits: [56, 122, 279], I see that the flag is fragmented in these 3 files.
- Morover, they are `b64 encoded`.
- Decoding and attaching them gives the flag.
