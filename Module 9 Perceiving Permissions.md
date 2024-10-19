# Perceiving Permissions
- ### Changing File Ownership
  changing file ownership using the chown command
  ```
  Connected!                                                                        
  hacker@permissions~changing-file-ownership:~$ chown hacker /flag
  hacker@permissions~changing-file-ownership:~$ cat /flag
  pwn.college{QS8pvnQ0l8-JJJ_eT8HfmkTKOwq.dFTM2QDLyATO0czW}
  hacker@permissions~changing-file-ownership:~$
  ```
### Groups and Files
  - changing group of a file using chgrp command
```
Connected!                                                                        
hacker@permissions~groups-and-files:~$ chgrp hacker /flag
hacker@permissions~groups-and-files:~$ cat /flag
pwn.college{wuIC_QH97B5JP3Oh1Jz_3D_0Rnx.dFzNyUDLyATO0czW}
hacker@permissions~groups-and-files:~$
```
### fun with group names
 - same thing
```
Connected!                                                                        
hacker@permissions~fun-with-groups-names:~$ id hacker
uid=1000(hacker) gid=1000(grp11704) groups=1000(grp11704)
hacker@permissions~fun-with-groups-names:~$ chgrp grp11704 /flag
hacker@permissions~fun-with-groups-names:~$ cat /flag
pwn.college{QutPivtqLooMGt7GmvW1cOwqi4m.dJzNyUDLyATO0czW}
hacker@permissions~fun-with-groups-names:~$ 
```
### Changing Permissions
 - using the chmod command to change permissions
```
Connected!                                                                        
hacker@permissions~changing-permissions:~$ chmod a+r /flag
hacker@permissions~changing-permissions:~$ cat flag
cat: flag: No such file or directory
hacker@permissions~changing-permissions:~$ cat /flag
pwn.college{0vAHpt0pDNQS8w4UpOu5dYet6ZN.dNzNyUDLyATO0czW}
hacker@permissions~changing-permissions:~$
```
### executing files
 - same thing
```
Connected!                                                                        
hacker@permissions~executable-files:~$ chmod a+x /challenge/run
hacker@permissions~executable-files:~$ /challenge/run
Successful execution! Here is your flag:
pwn.college{0qBClngMNK15iYlNXkBbCnE0lv6.dJTM2QDLyATO0czW}
hacker@permissions~executable-files:~$ 

```

