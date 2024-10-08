# File Globbing
### Matching with *
- its basically a placeholder. example ch* -> all files with ch at the start will
  it. so for referring to challenge in 4 characters we use /ch*
```
Connected!                                                                        
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
hacker@globbing~matching-with-:~$ cd /cha*
You specified the path to 'cd' to in more than 4 characters. Disallowed!
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
hacker@globbing~matching-with-:~$ cd /ch*
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{gnjpjx3qEPruSHo_lcgNlHmdi6m.dFjM4QDLyATO0czW}
```
### Matching with ?
- single character placeholder
```
Connected!                                                                        
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
hacker@globbing~matching-with-:~$ cd /?ha??enge
hacker@globbing~matching-with-:/challenge$ /challenge/flag
ssh-entrypoint: /challenge/flag: No such file or directory
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{IGDUtV7nEoYGxWzH6TC4LmGEhLa.dJjM4QDLyATO0czW}
```
### matching with []
- like ? but only matches with single characters given in bracket (no comma required)
  example- \[abc] will match with a,b and c
```
Connected!                                                                        
hacker@globbing~matching-with-:~$ /challenge/files
ssh-entrypoint: /challenge/files: Is a directory
hacker@globbing~matching-with-:~$ cd /challenge/files
hacker@globbing~matching-with-:/challenge/files$ /challenge/run file_[absh]
You got it! Here is your flag!
pwn.college{wEZ3VhKfSsgeIs6E4EBc-3n_usH.dNjM4QDLyATO0czW}
```
### matching paths with []
- using [] in absolute path
```
Connected!                                                                        
hacker@globbing~matching-paths-with-:~$ /challenge/run /challenge/files/file_[absh]
You got it! Here is your flag!
pwn.college{8IALmO5lbYKxS9wb9VD9nTC9YSU.dRjM4QDLyATO0czW}
```
### mixing globs
- fun challenge
```
Connected!                                                                        
hacker@globbing~mixing-globs:~$ cd /challenge/files
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [cep]*
You got it! Here is your flag!
pwn.college{Yynn5owgCxfeioXzaQa8nE78RKx.dVjM4QDLyATO0czW}
hacker@globbing~mixing-globs:/challenge/files$
```
### exclusionary globbing
- \[!abc]* or \[^abc]* returns the files that dont contain a, b or c
```
hacker@globbing~exclusionary-globbing:/challenge/files$ /challenge/run [^pwn]*
You got it! Here is your flag!
pwn.college{k6_LtreINXUkHsKfIq0RFarIjzW.dZjM4QDLyATO0czW}
```
  
