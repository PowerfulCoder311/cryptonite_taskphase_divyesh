# Digesting Documentation
- ### Missing Documentation
  for this we pass the arguement --giveflag to /challenge/challenge
```
Connected!                                                                        
hacker@man~learning-from-documentation:~$ /challenge/challenge --giveflag
Correct argument! Here is your flag:
pwn.college{IiSLjbVxGBhSXmsHKR5jQPGq7HY.dRjM5QDLyATO0czW}
```
- ### Learning Complex Usage
  basically arguements that require arguements. --printfile requires the file path,
  but file path isnt explicitly mentioned. so we ls the files and find the file.
```
hacker@man~learning-complex-usage:~$ ls
catfile  i  not-the-flag
hacker@man~learning-complex-usage:~$ /challenge/challenge --printfile catfile
Correct argument! Here is the catfile file:
pwn.college{Ue2wNPVi2wqYxYo6NFfU1ZCyHHY.dVjM5QDLyATO0czW}
hacker@man~learning-complex-usage:~$
```
- ### reading manuals
  man (name of command) gives the manual page for that command from centralised
  database
```
Connected!                                                                        
hacker@man~reading-manuals:~$ man challenge

CHALLENGE(1)                              Challenge Commands                              CHALLENGE(1)

NAME
       /challenge/challenge - print the flag!

SYNOPSIS
       challenge OPTION

DESCRIPTION
       Output the flag when called with the right arguments.

       --fortune
              read a fortune

       --version
              output version information and exit

       --byxtks NUM
              print the flag if NUM is 823

AUTHOR
       Written by Zardus.

REPORTING BUGS
       The repository for this dojo: <https://github.com/pwncollege/linux-luminarium/>

SEE ALSO
       man(1) bash-builtins(7)

pwn.college                                    May 2024                                   CHALLENGE(1)
hacker@man~reading-manuals:~$ /challenge/challenge - print the flag!
Incorrect usage! Please read the challenge man page!
hacker@man~reading-manuals:~$ /challenge/challenge --byxtks 823
Correct usage! Your flag: pwn.college{8b2yQxt39GFNksTPxwMW4AG_R3s.dRTM4QDLyATO0czW}
hacker@man~reading-manuals:~$
```
### searching manuals
- scrolled using arrow keys and searched 1600 lines of code for finding the right
  arguement
```
Connected!                                                                        
hacker@man~searching-manuals:~$ man challenge
hacker@man~searching-manuals:~$ /challenge/challenge --pwhqcqk
Initializing...
Correct usage! Your flag: pwn.college{I1cTnllct3MPc0imt-RqWPAc53l.dVTM4QDLyATO0czW}
```
### searching for manuals
- used man man -> found -k command that searches with the given arguement -> found the
  command, man that command to number (491) which finally gave the flag
```
hacker@man~searching-for-manuals:~$ /challenge/challenge --ohwboo 491
Correct usage! Your flag: pwn.college{ohwbOooqvpNpiwW4ryJO9z1cX6D.dZTM4QDLyATO0czW}
hacker@man~searching-for-manuals:~$ 
```
- ### helpful programs
```
Connected!                                                                        
hacker@man~helpful-programs:~$ --help
ssh-entrypoint: --help: command not found
hacker@man~helpful-programs:~$ /challenge/challenge --help
usage: a challenge to make you ask for help [-h] [--fortune] [-v] [-g GIVE_THE_FLAG] [-p]

optional arguments:
  -h, --help            show this help message and exit
  --fortune             read your fortune
  -v, --version         get the version number
  -g GIVE_THE_FLAG, --give-the-flag GIVE_THE_FLAG
                        get the flag, if given the correct value
  -p, --print-value     print the value that will cause the -g option to give you the flag
hacker@man~helpful-programs:~$ /challenge/challenge -g GIVE_THE_FLAG
usage: a challenge to make you ask for help [-h] [--fortune] [-v] [-g GIVE_THE_FLAG] [-p]
a challenge to make you ask for help: error: argument -g/--give-the-flag: invalid int value: 'GIVE_THE_FLAG'
hacker@man~helpful-programs:~$ /challenge/challenge -p
The secret value is: 504
hacker@man~helpful-programs:~$ /challenge/challenge -g GIVE_THE_FLAG 504
usage: a challenge to make you ask for help [-h] [--fortune] [-v] [-g GIVE_THE_FLAG] [-p]
a challenge to make you ask for help: error: argument -g/--give-the-flag: invalid int value: 'GIVE_THE_FLAG'
hacker@man~helpful-programs:~$ /challenge/challenge -g 504
Correct usage! Your flag: pwn.college{oB5gAu0-bPXaTXXLPeDnsSToeYE.ddjM4QDLyATO0czW}
hacker@man~helpful-programs:~$
```
- ### Help for builtins
  used the help builtin to get information of challenge command and then found the
  required arguement and value to get the flag.
```
Connected!                                                                        
hacker@man~help-for-builtins:~$ help challenge
challenge: challenge [--fortune] [--version] [--secret SECRET]
    This builtin command will read you the flag, given the right arguments!
    
    Options:
      --fortune		display a fortune
      --version		display the version
      --secret VALUE	prints the flag, if VALUE is correct

    You must be sure to provide the right value to --secret. That value
    is "EO05dQob".
hacker@man~help-for-builtins:~$ /challenge/challenge --secret EO05dQob
ssh-entrypoint: /challenge/challenge: No such file or directory
hacker@man~help-for-builtins:~$ challenge --secret EO05dQob
Correct! Here is your flag!
pwn.college{EO05dQobr3esEWspn52RP9lFA4_.dRTM5QDLyATO0czW}
```

