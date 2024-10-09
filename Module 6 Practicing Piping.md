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
### Grepping Stored Results
- here we use > operator to tranfer output of /challenge/flag into a file. Now the
  output contains too much text. To find the flag, we grep for "pwn.college" since
  that is the general starting of the flag.
```
Connected!                                                                        
hacker@piping~grepping-stored-results:~$ /challenge/run > /tmp/data.txt
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /tmp/data.txt
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to a file called /tmp/data.txt. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~grepping-stored-results:~$ grep "pwn.college" /tmp/data.txt
pwn.college{IkBndQ8H5sngIkIKYzU2faGboTP.dhTM4QDLyATO0czW}
hacker@piping~grepping-stored-results:~$ 
```
### Grepping Live Output
- The piping operator ('|') is used as sort of double arrow sign. It provides the
  output of the left arguement to the input of the right. Eliminating the need
  for a temporary file when using '<' and '>'
```
Connected!                                                                        
hacker@piping~grepping-live-output:~$ /challenge/run | grep "pwn.college"
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stdout : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/xpq4yhadyhazkcsggmqd7rsgvxb3kjy4-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stdout!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{4c-hBCkIK-HdYk9oBpy5L0tsUpt.dlTM4QDLyATO0czW}
hacker@piping~grepping-live-output:~$
```
### Grepping Errors
- we use the & suffix to convert the error code of /challenge/run into output so we
  can use the pipe operator
```
Connected!                                                                        
hacker@piping~grepping-errors:~$ /challenge/run 2>& 1 | grep "pwn.college"
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stderr : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stderr to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/xpq4yhadyhazkcsggmqd7rsgvxb3kjy4-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stderr!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{EWjAC7jcoOyoNrcw2o1s5PA3WNo.dVDM5QDLyATO0czW}
hacker@piping~grepping-errors:~$ 
```
### duplicating piped data with tee
-  tee arguement splits the same output into the arguements given after it.
```
Connected!                                                                        
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn | tee intercept.txt | /challenge/college
Processing...
The input to 'college' does not contain the correct secret code! This code 
should be provided by the 'pwn' command. HINT: use 'tee' to intercept the 
output of 'pwn' and figure out what the code needs to be.
hacker@piping~duplicating-piped-data-with-tee:~$ cat intercept.txt
Usage: /challenge/pwn --secret [SECRET_ARG]

SECRET_ARG should be "sv3B8RI2"
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn --secret sv3B8RI2
Processing...
You must pipe the output of /challenge/pwn into /challenge/college (or 'tee' 
for debugging).
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/college --secret sv3B8RI2
/challenge/secret needs to the on the receiving end of the output of 
'/challenge/pwn' (or 'tee' for debugging).
hacker@piping~duplicating-piped-data-with-tee:~$ cat /challenge/pwn --secret sv3B8RI2
cat: unrecognized option '--secret'
Try 'cat --help' for more information.
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn --secret "sv3B8RI2"
Processing...
You must pipe the output of /challenge/pwn into /challenge/college (or 'tee' 
for debugging).
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn --secret sv3B8RI2 | /challenge/college
Processing...
Correct! Passing secret value to /challenge/college...
Great job! Here is your flag:
pwn.college{sv3B8RI2HAwlAXzSRxWx_3-T6Oz.dFjM5QDLyATO0czW}
hacker@piping~duplicating-piped-data-with-tee:~$
```
### writing to multiple programs
- since tee takes one command and one file, we need to use a workaround to make it
  transfer its output to 2 files:
```
hacker@piping~writing-to-multiple-programs:~$ /challenge/hack | tee >( /challenge/the ) | /challenge/planet
Congratulations, you have duplicated data into the input of two programs! Here 
is your flag:
pwn.college{cEGaSbGRs8jJ1pEcpwXYdPuN4Rm.dBDO0UDLyATO0czW}
hacker@piping~writing-to-multiple-programs:~$
```
### Split-piping stderr and stdout
- to split stderr and stdout we cant use tee so we have to use > in a specific way
```
hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/hack > >( /challenge/planet ) 2> >( /challenge/the )
Congratulations, you have learned a redirection technique that even experts 
struggle with! Here is your flag:
pwn.college{YS5esh3CckoOYr8vF9cDp9_MozU.dFDNwYDLyATO0czW}
hacker@piping~split-piping-stderr-and-stdout:~$
```






