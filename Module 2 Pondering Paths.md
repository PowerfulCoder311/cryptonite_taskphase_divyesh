# Pondering Paths
### The Root
- absolute path starts from the home directory
```
hacker@paths~the-root:~$ /pwn
BOOM!!!
Here is your flag:
pwn.college{I8qbNprB8QAF_Ce3S7h2LxA04w5.dhzN5QDLyATO0czW}
hacker@paths~the-root:~$
```
### Program and absolute paths
- absolute path to traverse another directory for finding the file
```
Connected!                                                                        
hacker@paths~program-and-absolute-paths:~$ /challenge/run
Correct!!!
/challenge/run is an absolute path! Here is your flag:
pwn.college{oMWIxjPvEgr12NHTzVzlYjwSYgP.dVDN1QDLyATO0czW}
hacker@paths~program-and-absolute-paths:~$ 
```
### Position thy self
- cd (change directory) to change directories
```
Connected!                                                                        
hacker@paths~position-thy-self:~$ /challenge/run
Incorrect...
You are not currently in the /var/log directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-thy-self:~$ cd /
hacker@paths~position-thy-self:/$ /challenge/run
Incorrect...
You are not currently in the /var/log directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-thy-self:/$ cd /var/log
hacker@paths~position-thy-self:/var/log$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{kzoEoEFmyxIp8zQaPe2meL6wg3P.dZDN1QDLyATO0czW}
hacker@paths~position-thy-self:/var/log$ 
```
### Position elsewhere
- same thing
```
Connected!                                                                        
hacker@paths~position-elsewhere:~$ /challenge/run
Incorrect...
You are not currently in the /home directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-elsewhere:~$ cd /home
hacker@paths~position-elsewhere:/home$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{MMWu1nP1xGlaRrbJqeN_wFG3Sb2.ddDN1QDLyATO0czW}
hacker@paths~position-elsewhere:/home$ 
```

