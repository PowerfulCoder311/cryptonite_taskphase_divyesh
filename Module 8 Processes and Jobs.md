# Processes and Jobs
- ### Listing Processes
  ps command -> by default, lists processes running in current terminal.
  Its arguements:
    - standard syntax -> '-\e' for listing every process, '-\f' for showing processes
      full format output, including arguements

    - BSD syntax -> 'a' to list processes for all users, 'x' for processes that aren't
      running in a terminal, 'u' for user readable output
    NOTE- arguements can be combined in both
```
Connected!                                                                        
hacker@processes~listing-processes:~$ ps
    PID TTY          TIME CMD
     73 pts/0    00:00:00 ssh-entrypoint
     90 pts/0    00:00:00 ps
hacker@processes~listing-processes:~$ ps a
    PID TTY      STAT   TIME COMMAND
     73 pts/0    Ss     0:00 /run/dojo/bin/ssh-entrypoint
     91 pts/0    R+     0:00 ps a
hacker@processes~listing-processes:~$ ssh-entrypoint
hacker@processes~listing-processes:~$ ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.1  0.0   1056   640 ?        Ss   17:27   0:00 /sbin/docker-init -- /nix/var/nix/prof
root           7  0.0  0.0   5052  2560 ?        S    17:27   0:00 /run/dojo/bin/sleep 6h
root          68  0.0  0.0   4132  2560 ?        S    17:27   0:00 /challenge/2128-run-17009
root          72  0.0  0.0   2744  1280 ?        S    17:27   0:00 sleep 6h
hacker        73  0.0  0.0   5372  3840 pts/0    Ss   17:27   0:00 /run/dojo/bin/ssh-entrypoint
hacker        92  0.0  0.0   5368  3840 pts/0    S    17:28   0:00 ssh-entrypoint
hacker       104  0.0  0.0   7868  3200 pts/0    R+   17:28   0:00 ps aux
hacker@processes~listing-processes:~$ /challenge/2128-run-17009
Yahaha, you found me! Here is your flag:
pwn.college{QRA05ZA5a2FOYsu1Amb0y0EGjl-.dhzM4QDLyATO0czW}
Now I will sleep for a while (so that you could find me with 'ps').
```
- ### Killing Processes
  Killing processes using 'kill' command followed by PID of the process that is to be
  stopped.
```
Connected!                                                                        
hacker@processes~killing-processes:~$ ps -e | grep dont_run
hacker@processes~killing-processes:~$ /challenge/run
Nope! /challenge/dont_run is still running! You gotta terminate it before I 
give you the flag!
hacker@processes~killing-processes:~$ ps 
    PID TTY          TIME CMD
     75 pts/0    00:00:00 ssh-entrypoint
     98 pts/0    00:00:00 ps
hacker@processes~killing-processes:~$ ps -e
    PID TTY          TIME CMD
      1 ?        00:00:00 docker-init
      7 ?        00:00:00 /run/dojo/bin/s
     71 ?        00:00:00 su
     73 ?        00:00:00 bash
     74 ?        00:00:00 sleep
     75 pts/0    00:00:00 ssh-entrypoint
     99 pts/0    00:00:00 ps
hacker@processes~killing-processes:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 17:32 ?        00:00:00 /sbin/docker-init -- /nix/var/nix/profiles/default/bi
root           7       1  0 17:32 ?        00:00:00 /run/dojo/bin/sleep 6h
root          71       1  0 17:32 ?        00:00:00 su -c /challenge/.launcher hacker
hacker        73      71  0 17:32 ?        00:00:00 /challenge/dont_run
hacker        74      73  0 17:32 ?        00:00:00 sleep 6h
hacker        75       0  0 17:32 pts/0    00:00:00 /run/dojo/bin/ssh-entrypoint
hacker       100      75  0 17:34 pts/0    00:00:00 ps -ef
hacker@processes~killing-processes:~$ kill 73
hacker@processes~killing-processes:~$ /challenge/run
Great job! Here is your payment:
pwn.college{QW-fmHVZHI48fgRBcz6LmMSGnAF.dJDN4QDLyATO0czW}
hacker@processes~killing-processes:~$ 

```
- ### Interrupting Processes
  Interrupting processes by pressing control+C while the process is running
```
Connected!                                                                        
hacker@processes~interrupting-processes:~$ /challenge/run
I could give you the flag... but I won't, until this process exits. Remember, 
you can force me to exit with Ctrl-C. Try it now!
^C
Good job! You have used Ctrl-C to interrupt this process! Here is your flag:
pwn.college{k7TjjRAW87dNh1orLDZ_82gFH2f.dNDN4QDLyATO0czW}
hacker@processes~interrupting-processes:~
```
- ### Suspending Process
  Suspending process by pressing control +Z while the process is running
```
Connected!                                                                        
hacker@processes~suspending-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running in 
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root          82      65  0 17:43 pts/0    00:00:00 bash /challenge/run
root          84      82  0 17:43 pts/0    00:00:00 ps -f

I don't see a second me!

To pass this level, you need to suspend me and launch me again! You can 
background me with Ctrl-Z or, if you're not ready to do that for whatever 
reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~suspending-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running in 
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root          82      65  0 17:43 pts/0    00:00:00 bash /challenge/run
root          89      65  0 17:44 pts/0    00:00:00 bash /challenge/run
root          91      89  0 17:44 pts/0    00:00:00 ps -f

Yay, I found another version of me! Here is the flag:
pwn.college{QguNGN-fMqHsAsl-VbL5gVP6w23.dVDN4QDLyATO0czW}
hacker@processes~suspending-processes:~$ 
```
- ### Resuming Processes
  using fs to resume the suspended command
```
Connected!                                                                        
hacker@processes~resuming-processes:~$ /challenge/run
Let's practice resuming processes! Suspend me with Ctrl-Z, then resume me with 
the 'fg' command! Or just press Enter to quit me!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~resuming-processes:~$ fg
/challenge/run
I'm back! Here's your flag:
pwn.college{Em6ghJiHol3noqfD2HU__1QwgXN.dZDN4QDLyATO0czW}
Don't forget to press Enter to quit me!
```
- ### Backgrounding Processes
  opening suspended processes in background using 'bg' command
```
Connected!                                                                        
hacker@processes~backgrounding-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and 
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root          82 S+   bash /challenge/run
root          84 R+   ps -o user=UID,pid,stat,cmd

I don't see a second me!

To pass this level, you need to suspend me, resume the suspended process in the 
background, and then launch a new version of me! You can background me with 
Ctrl-Z (and resume me in the background with 'bg') or, if you're not ready to 
do that for whatever reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~backgrounding-processes:~$ bg
[1]+ /challenge/run &
hacker@processes~backgrounding-processes:~$ 


Yay, I'm now running the background! Because of that, this text will probably 
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times 
to scroll this text out.

hacker@processes~backgrounding-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and 
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root          82 S    bash /challenge/run
root          92 S    sleep 6h
root          93 S+   bash /challenge/run
root          95 R+   ps -o user=UID,pid,stat,cmd

Yay, I found another version of me running in the background! Here is the flag:
pwn.college{gf1HsutCZWL9sQD7KvB15dpsgUR.ddDN4QDLyATO0czW}
hacker@processes~backgrounding-processes:~$ 
```
- ### foregrounding processes
  
  


