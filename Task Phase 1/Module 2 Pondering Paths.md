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
### Position yet elsewhere
Connected!                                                                        
hacker@paths~position-yet-elsewhere:~$ /challenge/run
Incorrect...
You are not currently in the /var directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-yet-elsewhere:~$ cd /var
hacker@paths~position-yet-elsewhere:/var$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{gjXsaP9hzVcjKmGTXYq-_FtThfE.dhDN1QDLyATO0czW}
hacker@paths~position-yet-elsewhere:/var$ 

### implicit relative paths, from /
- running the files from current working directory and not using absolute path
```
Connected!                                                                        
hacker@paths~implicit-relative-paths-from-:~$ /challenge/run
Incorrect...
You are not currently in the / directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~implicit-relative-paths-from-:~$ cd /
hacker@paths~implicit-relative-paths-from-:/$ challenge/run
Correct!!!
challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{IsUwHIDmKGASGPgDnEQI-2dqWxB.dlDN1QDLyATO0czW}
hacker@paths~implicit-relative-paths-from-:/$
```
### explicit relative paths, from /
- '.' refers to the same directory. therefore './' means execute from the same directory
```
Connected!                                                                        
hacker@paths~explicit-relative-paths-from-:~$ /challenge/run
Incorrect...
You are not currently in the / directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~explicit-relative-paths-from-:~$ cd /
hacker@paths~explicit-relative-paths-from-:/$ ./challenge/run
Correct!!!
./challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{gHDuNDqXlzdrCW0LGdJVzBceLYr.dBTN1QDLyATO0czW}
hacker@paths~explicit-relative-paths-from-:/$
```

