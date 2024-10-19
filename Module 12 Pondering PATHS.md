# Pondering PATHS
### The Path variable
- we get to know that the PATH variable in linux stores all the key positions of the
  files on the system, without which, any command cant get location of the files.
```
Connected!                                                                        
hacker@path~the-path-variable:~$ PATH=''
hacker@path~the-path-variable:~$ /challenge/run
Trying to remove /flag...
/challenge/run: line 4: rm: No such file or directory
The flag is still there! I might as well give it to you!
pwn.college{ARLxS-sp7f3A25T71j0UaWW_MAr.dZzNwUDLyATO0czW}
hacker@path~the-path-variable:~$
```
### Setting Path
- setting path to a directory to make the files in that directory accessible by
  barename
```
Connected!                                                                        
hacker@path~setting-path:~$ PATH='/challenge/more_commands/'
hacker@path~setting-path:~$ /challenge/run
Invoking 'win'....
Congratulations! You properly set the flag and 'win' has launched!
pwn.college{cb8_PtKeN3vDqGZImSwi0rjNwVl.dVzNyUDLyATO0czW}
hacker@path~setting-path:~$ 
```
