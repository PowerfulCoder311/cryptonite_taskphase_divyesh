# Shell Variables 🚀
 - ### Printing Variables
   We can use echo to print variables by adding '$' before the name of the variable to
   tell the shell its a variable.
   ```
   Connected!                                                                        
    hacker@variables~printing-variables:~$ echo $FLAG
    pwn.college{QYeH3SajQVe4Cgm_qIrZ4MsbeLy.ddTN1QDLyATO0czW}
    hacker@variables~printing-variables:~$
   ```
- ### Setting Variables
  using '=' to assign values to variables (Note: no spaces)
```
Connected!                                                                        
hacker@variables~setting-variables:~$ PWN=COLLEGE
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{Inkukmwc4yWG8BfUKhWJ-ZQuxpG.dlTN1QDLyATO0czW}
hacker@variables~setting-variables:~$
```
- ### Multi-Word Variables
  To assign a value that contains spaces, we must use quotes ("")
```
hacker@variables~multi-word-variables:~$ PWN="COLLEGE YEAH"
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{EG6tv5hJ9aDQImcRfiirP62LVsK.dBjN1QDLyATO0czW}
hacker@variables~multi-word-variables:~$
```
- ### Exporting Variables
  by default, the variables defined in main shell process can't be called from child
  processes. we use export command to make it callable🙂
```
Connected!                                                                        
hacker@variables~exporting-variables:~$ PWN=COLLEGE
You've set the PWN variable to the proper value!
hacker@variables~exporting-variables:~$ export PWN
You've set the PWN variable to the proper value!
hacker@variables~exporting-variables:~$ COLLEGE=PWN
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
hacker@variables~exporting-variables:~$ /challenge/run PWN
CORRECT!
You have exported PWN=COLLEGE and set, but not exported, COLLEGE=PWN. Great 
job! Here is your flag:
pwn.college{cmL6sv5LHC97RiQYsCSGzqSO-Xy.dJjN1QDLyATO0czW}
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
hacker@variables~exporting-variables:~$
```
- ### Printing Exported Variables
  


