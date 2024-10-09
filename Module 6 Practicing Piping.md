# Practicing Piping

### Redirecting Output
- using '>' operator to redirect the output into a file
```
tutu@Divyeshs-MacBook-Pro .ssh % ssh -i ./key hacker@dojo.pwn.college
Connected!                                                                        
hacker@piping~redirecting-output:~$ echo PWN > COLLEGE
Correct! You successfully redirected 'PWN' to the file 'COLLEGE'! Here is your 
flag:
pwn.college{s33YoZvRWV8mD6R3C6LgcIfdWiN.dRjN1QDLyATO0czW}
```
### Redirecting more output
- same thing
```
hacker@piping~redirecting-more-output:~$ /challenge/run > myflag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : myflag
[INFO] - the challenge will output a reward file if all the tests pass : /flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /flag file.

[TEST] You should have redirected my stdout to a file called myflag. Checking...

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~redirecting-more-output:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{8qrqFHA2EXW3mb6S7Gn2gcu4kKS.dVjN1QDLyATO0czW}

hacker@piping~redirecting-more-output:~$
```
### Appending Output
- using >> we append the output into the file and not overwrite like > operator does
```
Connected!                                                                        
hacker@piping~appending-output:~$ /challenge/run >> /home/hacker/the-flag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /home/hacker/the-flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] Good luck!

[TEST] You should have redirected my stdout to a file called /home/hacker/the-flag. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
I will write the flag in two parts to the file /home/hacker/the-flag! I'll do 
the first write directly to the file, and the second write, I'll do to stdout 
(if it's pointing at the file). If you redirect the output in append mode, the 
second write will append to (rather than overwrite) the first write, and you'll 
get the whole flag!
hacker@piping~appending-output:~$ cat /home/hacker/the-flag
 | 
\|/ This is the first half:
 v 
pwn.college{U6DHGE1AK3ZIaqknvfzXpd2VCTr.ddDM5QDLyATO0czW}
                              ^
     that is the second half /|\
                              |

If you only see the second half above, you redirected in *truncate* mode (>) 
rather than *append* mode (>>), and so the write of the second half to stdout 
overwrote the initial write of the first half directly to the file. Try append 
mode!
hacker@piping~appending-output:~$ 
```
### Redirecting Errors
- 0 refers to input, 1 refers to output and 2 refers to errors
- > operator by default redirects output therefore its equivalent to 1>
- similarly 2> redirects errors
```
Connected!                                                                        
hacker@piping~redirecting-errors:~$ /challenge/run > myflag 2> instructions
hacker@piping~redirecting-errors:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{gz4K6btgtKHUzbPloVWPGDJ0G6b.ddjN1QDLyATO0czW}

hacker@piping~redirecting-errors:~$
```
### Redirecting Inputs
- < operator can be used to insert the arguement given on the right to the arguement
  given on the left
```
Connected!                                                                        
hacker@piping~redirecting-input:~$ echo COLLEGE > PWN
hacker@piping~redirecting-input:~$ /challenge/run < PWN
Reading from standard input...
Correct! You have redirected the PWN file into my standard input, and I read 
the value 'COLLEGE' out of it!
Here is your flag:
pwn.college{ULqWkSJIL1SuwCxptJY1ZrSIAcG.dBzN1QDLyATO0czW}
```



