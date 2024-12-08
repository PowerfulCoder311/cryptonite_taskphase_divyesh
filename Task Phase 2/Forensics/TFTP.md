# Trivial File Transfer Protocol
### First Approach
We see about 4 files being transferred over the network. 1 program, and 3 images. My first approach was to export each of these files by filtering the pull requests and moving from there. I successfully retrieved the 3 images and 1 program, however it was in hexdump. Tried multiple methods of converting it to bmp, but none worked. Therefore, I looked for another way.
### Second Approach
While going through the menus of wireshark, I found that it has a option to directly export TFTP objects. I saved that onto my computer and got 3 pictures, 2 txt files (plan and instructions) and 1 program (which i was able to characterise earlier from looking at the packets)
Both of the text files are encrypted. So I got the indication decrypting these 2 text files would tell me the next steps.

Unsuccessful decryption methods:
- Hill Cipher
- playfair cipher
- foursquare cypher
  
Successful method: Shift Cipher
Decrypted message:

Instructions.txt -> TFTPDOESNTENCRYPTOURTRAFFICSOWEMUSTDISGUISEOURFLAGTRANSFER.FIGUREOUTAWAYTOHIDETHEFLAGANDIWILLCHECKBACKFORTHEPLAN

Plan.txt -> IUSEDTHEPROGRAMANDHIDITWITH-DUEDILIGENCE.CHECKOUTTHEPHOTOS

We see that the file has been hidden using the program and hidden inside the pictures. 
Since the program is in deb and I use a apple silicon mac without the dpkg package installed, I have to install it first.
attempts to unpack the file:
```
Use 'apt' or 'aptitude' for user-friendly package management.
tutu@Divyeshs-MacBook-Pro ~ % dpkg --unpack /Users/tutu/Desktop/Forensics TFTP/program.deb
dpkg: error: requested operation requires superuser privilege
tutu@Divyeshs-MacBook-Pro ~ % sudo dpkg --unpack /Users/tutu/Desktop/Forensics TFTP/program.deb
Password:
dpkg: error: cannot access archive '/Users/tutu/Desktop/Forensics': No such file or directory
tutu@Divyeshs-MacBook-Pro ~ % sudo dpkg --unpack /Users/tutu/Downloads/Forensics TFTP/program.deb
dpkg: error: cannot access archive '/Users/tutu/Downloads/Forensics': No such file or directory
tutu@Divyeshs-MacBook-Pro ~ % /downloads 
zsh: no such file or directory: /downloads
tutu@Divyeshs-MacBook-Pro ~ % cd downloads
tutu@Divyeshs-MacBook-Pro downloads % sudo dpkg --unpack /Forensics TFTP/ prgram.deb
dpkg: error: cannot access archive '/Forensics': No such file or directory
tutu@Divyeshs-MacBook-Pro downloads % downloads % sudo dpkg --unpack /Forensics/ program.deb
zsh: command not found: downloads
tutu@Divyeshs-MacBook-Pro downloads % cd /
tutu@Divyeshs-MacBook-Pro / % cd
tutu@Divyeshs-MacBook-Pro ~ % sudo dpkg --unpack /Users/tutu/Downloads/Forensics/program.deb
dpkg: error processing archive /Users/tutu/Downloads/Forensics/program.deb (--unpack):
 package architecture (amd64) does not match system (darwin-arm64)
Errors were encountered while processing:
 /Users/tutu/Downloads/Forensics/program.deb
tutu@Divyeshs-MacBook-Pro ~ %
```
finally got the error package architecture is different from system architecture
Instead, I tried just inspecting the file and got the following result:

```
dpkg: error: requested operation requires superuser privilege
tutu@Divyeshs-MacBook-Pro Forensics % sudo dpkg -c program.deb
Password:
drwxr-xr-x root/root         0 2014-10-15 05:32 ./
drwxr-xr-x root/root         0 2014-10-15 05:32 ./usr/
drwxr-xr-x root/root         0 2014-10-15 05:32 ./usr/share/
drwxr-xr-x root/root         0 2014-10-15 05:32 ./usr/share/doc/
drwxr-xr-x root/root         0 2014-10-15 05:32 ./usr/share/doc/steghide/
-rw-r--r-- root/root      6066 2014-10-15 05:32 ./usr/share/doc/steghide/ABOUT-NLS.gz
-rw-r--r-- root/root      2771 2014-10-15 05:32 ./usr/share/doc/steghide/LEAME.gz
-rw-r--r-- root/root      2488 2003-09-28 21:00 ./usr/share/doc/steghide/README.gz
-rw-r--r-- root/root      1763 2014-10-15 05:31 ./usr/share/doc/steghide/changelog.Debian.gz
-rw-r--r-- root/root       215 2014-10-15 05:31 ./usr/share/doc/steghide/changelog.Debian.amd64.gz
-rw-r--r-- root/root       860 2003-10-11 14:33 ./usr/share/doc/steghide/changelog.gz
-rw-r--r-- root/root      1088 2014-10-15 05:31 ./usr/share/doc/steghide/copyright
-rw-r--r-- root/root       787 2003-05-03 18:11 ./usr/share/doc/steghide/TODO
-rw-r--r-- root/root      1957 2003-10-11 14:33 ./usr/share/doc/steghide/HISTORY
-rw-r--r-- root/root       895 2003-10-11 14:34 ./usr/share/doc/steghide/CREDITS
-rw-r--r-- root/root       598 2003-09-27 13:10 ./usr/share/doc/steghide/BUGS
drwxr-xr-x root/root         0 2014-10-15 05:32 ./usr/share/man/
drwxr-xr-x root/root         0 2014-10-15 05:32 ./usr/share/man/man1/
-rw-r--r-- root/root      3760 2014-10-15 05:32 ./usr/share/man/man1/steghide.1.gz
drwxr-xr-x root/root         0 2014-10-15 05:32 ./usr/share/locale/
drwxr-xr-x root/root         0 2014-10-15 05:32 ./usr/share/locale/ro/
drwxr-xr-x root/root         0 2014-10-15 05:32 ./usr/share/locale/ro/LC_MESSAGES/
-rw-r--r-- root/root     30028 2014-10-15 05:32 ./usr/share/locale/ro/LC_MESSAGES/steghide.mo
drwxr-xr-x root/root         0 2014-10-15 05:32 ./usr/share/locale/fr/
drwxr-xr-x root/root         0 2014-10-15 05:32 ./usr/share/locale/fr/LC_MESSAGES/
-rw-r--r-- root/root     30386 2014-10-15 05:32 ./usr/share/locale/fr/LC_MESSAGES/steghide.mo
drwxr-xr-x root/root         0 2014-10-15 05:32 ./usr/share/locale/de/
drwxr-xr-x root/root         0 2014-10-15 05:32 ./usr/share/locale/de/LC_MESSAGES/
-rw-r--r-- root/root     30268 2014-10-15 05:32 ./usr/share/locale/de/LC_MESSAGES/steghide.mo
drwxr-xr-x root/root         0 2014-10-15 05:32 ./usr/share/locale/es/
drwxr-xr-x root/root         0 2014-10-15 05:32 ./usr/share/locale/es/LC_MESSAGES/
-rw-r--r-- root/root     29198 2014-10-15 05:32 ./usr/share/locale/es/LC_MESSAGES/steghide.mo
drwxr-xr-x root/root         0 2014-10-15 05:32 ./usr/bin/
-rwxr-xr-x root/root    290888 2014-10-15 05:32 ./usr/bin/steghide
tutu@Divyeshs-MacBook-Pro Forensics % 
```
There are a lot of files mentioning 'steghide'. Looking up steghide, i see its a way of concealing data in pictures, audio etc. Perfect!, just have to find the data hidden in the images using steghide
Since it requires a password, I tried multiple combinations from plan... Finally, the password DUEDILIGENCE worked on picture 3.

FLAG:
picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}


