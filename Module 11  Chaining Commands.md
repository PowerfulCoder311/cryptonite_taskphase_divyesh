# Chaining Commands

### Chaining with Semicolons
- using semicolon (;) to chain different commands in a single line to be executed        together
```
Connected!                                                                        
hacker@chaining~chaining-with-semicolons:~$ /challenge/pwn;/challenge/college
Yes! You chained /challenge/pwn and /challenge/college! Here is your flag:
pwn.college{AlDwP4QcCvmoWE1yDyNxuXstuMA.dVTN4QDLyATO0czW}
hacker@chaining~chaining-with-semicolons:~$ 
```
### Your First Shell Script
- using bash operator to execute shell files
```
Connected!                                                                        
hacker@chaining~your-first-shell-script:~$ touch x.sh
hacker@chaining~your-first-shell-script:~$ nano x.sh
hacker@chaining~your-first-shell-script:~$ bash x.sh
Great job, you've written your first shell script! Here is the flag:
pwn.college{sdqOqweI2Vdwgbet7F6KOlHpVI7.dFzN4QDLyATO0czW}
hacker@chaining~your-first-shell-script:~$ 
```
### Redirecting Script Output
- since bash is just another command, redirecting (piping) its output into another
  command
```
Connected!                                                                        
hacker@chaining~redirecting-script-output:~$ touch x.sh
hacker@chaining~redirecting-script-output:~$ nano x.sh
hacker@chaining~redirecting-script-output:~$ bash x.sh > /challenge/solve
No shenanigans with bash options yet, please! Just run your script with 'bash 
x.sh'.
ssh-entrypoint: /challenge/solve: Permission denied
hacker@chaining~redirecting-script-output:~$ bash x.sh | /challenge/solve
Correct! Here is your flag:
pwn.college{I2OGPUOb__97_54K-bHSxuj11dl.dhTM5QDLyATO0czW}
hacker@chaining~redirecting-script-output:~$ 
```
### Executable Shell Scripts
- executing shell files by first changing default permissions and running like normal
  file.
```
Connected!                                                                        
hacker@chaining~executable-shell-scripts:~$ touch solve.sh
hacker@chaining~executable-shell-scripts:~$ nano solve.sh
hacker@chaining~executable-shell-scripts:~$ chmod a+rwx solve.sh
hacker@chaining~executable-shell-scripts:~$ /solve.sh
ssh-entrypoint: /solve.sh: No such file or directory
hacker@chaining~executable-shell-scripts:~$ ./solve.sh
Congratulations on your shell script execution! Your flag:
pwn.college{8GYM8ZKyzKhqcPKhXfH7UDqopTR.dRzNyUDLyATO0czW}
hacker@chaining~executable-shell-scripts:~$
```



