# Untangling Users

### Becoming root with su
- getting root access using 'su' operator and entering the password
```
Connected!                                                                        
hacker@users~becoming-root-with-su:~$ su
Password: 
root@users~becoming-root-with-su:/home/hacker# cat /flag
pwn.college{ImZa8qgzH__QWXf5de-CTEMFRAx.dVTN0UDLyATO0czW}
root@users~becoming-root-with-su:/home/hacker#
```
### Other users with su
- switching to users other than root using su
```
Connected!                                                                        
hacker@users~other-users-with-su:~$ su zardus
Password: 
zardus@users~other-users-with-su:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{40qb1f6hxzufDoEVyzjOnLALGkt.dZTN0UDLyATO0czW}
zardus@users~other-users-with-su:/home/hacker$
```
### Cracking Passwords
- using the john the ripper command to decrypt hashed passwords
```
Connected!                                                                        
hacker@users~cracking-passwords:~$ john /challenge/shadow-leak
Created directory: /home/hacker/.john
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Press 'q' or Ctrl-C to abort, almost any other key for status
aardvark         (zardus)
1g 0:00:00:20 100% 2/3 0.04773g/s 277.9p/s 277.9c/s 277.9C/s Johnson..buzz
Use the "--show" option to display all of the cracked passwords reliably
Session completed
hacker@users~cracking-passwords:~$ su zardus
Password: 
zardus@users~cracking-passwords:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{0OOQbbZjM2ClSpQItJkwR2AoCAW.ddTN0UDLyATO0czW}
zardus@users~cracking-passwords:/home/hacker$ 
```
### using sudo
- using sudo to get root access
```
Connected!                                                                        
hacker@users~using-sudo:~$ sudo cat /flag
pwn.college{IpzIMQZCQW8GR6IkGDLaQl0zIzH.dhTN0UDLyATO0czW}
hacker@users~using-sudo:~$ 
```

