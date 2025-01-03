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
### Adding Commands
- first creating shell file, making it executable then adding the directory of the
  file to PATH without overwriting it and using /challenge/run to get the flag
```
Connected!                                                                        
hacker@path~adding-commands:~$ touch win.sh
hacker@path~adding-commands:~$ nano win.sh
hacker@path~adding-commands:~$ mv win.sh win
hacker@path~adding-commands:~$ chmod a+rwx win
hacker@path~adding-commands:~$ PATH=$PATH:/home/hacker
hacker@path~adding-commands:~$ /challenge/run
Invoking 'win'....
pwn.college{kOyn0SBhdmXxdFCcsMzKHTLTTUs.dZzNyUDLyATO0czW}
hacker@path~adding-commands:~$ 
```

