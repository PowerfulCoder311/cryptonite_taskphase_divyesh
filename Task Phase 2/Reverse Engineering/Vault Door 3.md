# Vault Door 3
source code:
```
import java.util.*;

class VaultDoor3 {
    public static void main(String args[]) {
        VaultDoor3 vaultDoor = new VaultDoor3();
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter vault password: ");
        String userInput = scanner.next();
        String input = userInput.substring("picoCTF{".length(), userInput.length() - 1);
        if (vaultDoor.checkPassword(input)) {
            System.out.println("Access granted.");
        } else {
            System.out.println("Access denied!");
        }
    }

    // Our security monitoring team has noticed some intrusions on some of the
    // less secure doors. Dr. Evil has asked me specifically to build a stronger
    // vault door to protect his Doomsday plans. I just *know* this door will
    // keep all of those nosy agents out of our business. Mwa ha!
    //
    // -Minion #2671
    public boolean checkPassword(String password) {
        if (password.length() != 32) {
            return false;
        }
        char[] buffer = new char[32];
        int i;
        for (i = 0; i < 8; i++) {
            buffer[i] = password.charAt(i);
        }
        for (; i < 16; i++) {
            buffer[i] = password.charAt(23 - i);
        }
        for (; i < 32; i += 2) {
            buffer[i] = password.charAt(46 - i);
        }
        for (i = 31; i >= 17; i -= 2) {
            buffer[i] = password.charAt(i);
        }
        String s = new String(buffer);
        return s.equals("jU5t_a_sna_3lpm12g94c_u_4_m7ra41");
    }
}
```
This is a password checking code that does a few operations on the text given and checks with jU5t_a_sna_3lpm12g94c_u_4_m7ra41
So we have to input suitable text that when manipulated by the code returns jU5t_a_sna_3lpm12g94c_u_4_m7ra41. 
 

   
 String input = userInput.substring("picoCTF{".length(), userInput.length() - 1);
 Therefore this code already removes the picoCTF{} text from the input.  
 

My first approach is to reenter String input = userInput.substring("picoCTF{".length(), userInput.length() - 1); to see what it returns, however the code returns access denied. So, since this is java, we add a system.out.println() before the return statement to see what the output is.

This gets us the flag.
flag-> picoCTF{jU5t_a_s21mpl3_a4gr4m_4_u_c79a21}


```
─(divyesh㉿macbook)-[~]
└─$ cd Do       
cd: no such file or directory: Do
                                                                             
┌──(divyesh㉿macbook)-[~]
└─$ cd Downloads
                                                                             
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ javac VaultDoor3.java
Command 'javac' not found, did you mean:
  command 'javacc' from deb javacc
  command 'javagc' from deb libbpf-tools
Try: sudo apt install <deb name>
                                                                             
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ sudo apt update                  
[sudo] password for divyesh: 
Get:1 http://mirror.kku.ac.th/kali kali-rolling InRelease [41.5 kB]
Get:2 http://mirror.kku.ac.th/kali kali-rolling/main arm64 Packages [20.2 MB]
Get:3 http://mirror.kku.ac.th/kali kali-rolling/main arm64 Contents (deb) [47.9 MB]
Get:4 http://mirror.kku.ac.th/kali kali-rolling/contrib arm64 Packages [95.7 kB]
Get:5 http://mirror.kku.ac.th/kali kali-rolling/contrib arm64 Contents (deb) [182 kB]
Get:6 http://mirror.kku.ac.th/kali kali-rolling/non-free arm64 Packages [154 kB]
Get:7 http://mirror.kku.ac.th/kali kali-rolling/non-free arm64 Contents (deb) [829 kB]
Fetched 69.4 MB in 20s (3,484 kB/s)                                         
WARNING:root:cannot read /var/lib/command-not-found/commands.db.metadata: Expecting value: line 1 column 1 (char 0)
E: LZ4F: /var/lib/apt/lists/http.kali.org_kali_dists_kali-rolling_non-free-firmware_Contents-arm64.lz4 Unexpected end of file
E: LZ4F: /var/lib/apt/lists/http.kali.org_kali_dists_kali-rolling_non-free-firmware_Contents-arm64.lz4 Read error (18446744073709551615: ERROR_GENERIC)
Traceback (most recent call last):
  File "/usr/lib/cnf-update-db", line 32, in <module>
    col.create(db)
  File "/usr/share/command-not-found/CommandNotFound/db/creator.py", line 96, in create
    self._fill_commands(con)
  File "/usr/share/command-not-found/CommandNotFound/db/creator.py", line 145, in _fill_commands
    raise subprocess.CalledProcessError(returncode=sub.returncode,
subprocess.CalledProcessError: Command '/usr/lib/apt/apt-helper cat-file /var/lib/apt/lists/http.kali.org_kali_dists_kali-rolling_non-free-firmware_Contents-arm64.lz4' returned non-zero exit status 100.
Error: Problem executing scripts APT::Update::Post-Invoke-Success 'if /usr/bin/test -w /var/lib/command-not-found/ -a -e /usr/lib/cnf-update-db; then /usr/lib/cnf-update-db > /dev/null; fi'
Error: Sub-process returned an error code
                                                                             
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ sudo apt install default-jdk     
Installing:                     
  default-jdk
                                                                             
Installing dependencies:
  default-jdk-headless  openjdk-21-jdk  openjdk-21-jdk-headless
                                                                             
Suggested packages:
  openjdk-21-demo  openjdk-21-source  visualvm

Summary:
  Upgrading: 0, Installing: 4, Removing: 0, Not Upgrading: 537
  Download size: 85.3 MB
  Space needed: 100 MB / 13.7 GB available

Continue? [Y/n] y
Get:1 http://http.kali.org/kali kali-rolling/main arm64 openjdk-21-jdk-headless arm64 21.0.5+11-1 [81.9 MB]
Get:2 http://kali.download/kali kali-rolling/main arm64 default-jdk-headless arm64 2:1.21-76 [1,124 B]
Get:3 http://http.kali.org/kali kali-rolling/main arm64 openjdk-21-jdk arm64 21.0.5+11-1 [3,422 kB]
Get:4 http://kali.download/kali kali-rolling/main arm64 default-jdk arm64 2:1.21-76 [1,076 B]
Fetched 85.3 MB in 4s (20.8 MB/s)
Selecting previously unselected package openjdk-21-jdk-headless:arm64.
(Reading database ... 394775 files and directories currently installed.)
Preparing to unpack .../openjdk-21-jdk-headless_21.0.5+11-1_arm64.deb ...
Unpacking openjdk-21-jdk-headless:arm64 (21.0.5+11-1) ...
Selecting previously unselected package default-jdk-headless.
Preparing to unpack .../default-jdk-headless_2%3a1.21-76_arm64.deb ...
Unpacking default-jdk-headless (2:1.21-76) ...
Selecting previously unselected package openjdk-21-jdk:arm64.
Preparing to unpack .../openjdk-21-jdk_21.0.5+11-1_arm64.deb ...
Unpacking openjdk-21-jdk:arm64 (21.0.5+11-1) ...
Selecting previously unselected package default-jdk.
Preparing to unpack .../default-jdk_2%3a1.21-76_arm64.deb ...
Unpacking default-jdk (2:1.21-76) ...
Setting up openjdk-21-jdk-headless:arm64 (21.0.5+11-1) ...
update-alternatives: using /usr/lib/jvm/java-21-openjdk-arm64/bin/jar to provide /usr/bin/jar (jar) in auto mode
update-alternatives: using /usr/lib/jvm/java-21-openjdk-arm64/bin/jarsigner to provide /usr/bin/jarsigner (jarsigner) in auto mode
update-alternatives: using /usr/lib/jvm/java-21-openjdk-arm64/bin/javac to provide /usr/bin/javac (javac) in auto mode
update-alternatives: using /usr/lib/jvm/java-21-openjdk-arm64/bin/javadoc to provide /usr/bin/javadoc (javadoc) in auto mode
update-alternatives: using /usr/lib/jvm/java-21-openjdk-arm64/bin/javap to provide /usr/bin/javap (javap) in auto mode
update-alternatives: using /usr/lib/jvm/java-21-openjdk-arm64/bin/jcmd to provide /usr/bin/jcmd (jcmd) in auto mode
update-alternatives: using /usr/lib/jvm/java-21-openjdk-arm64/bin/jdb to provide /usr/bin/jdb (jdb) in auto mode
update-alternatives: using /usr/lib/jvm/java-21-openjdk-arm64/bin/jdeprscan to provide /usr/bin/jdeprscan (jdeprscan) in auto mode
update-alternatives: using /usr/lib/jvm/java-21-openjdk-arm64/bin/jdeps to provide /usr/bin/jdeps (jdeps) in auto mode
update-alternatives: using /usr/lib/jvm/java-21-openjdk-arm64/bin/jfr to provide /usr/bin/jfr (jfr) in auto mode
update-alternatives: using /usr/lib/jvm/java-21-openjdk-arm64/bin/jimage to provide /usr/bin/jimage (jimage) in auto mode
update-alternatives: using /usr/lib/jvm/java-21-openjdk-arm64/bin/jinfo to provide /usr/bin/jinfo (jinfo) in auto mode
update-alternatives: using /usr/lib/jvm/java-21-openjdk-arm64/bin/jlink to provide /usr/bin/jlink (jlink) in auto mode
update-alternatives: using /usr/lib/jvm/java-21-openjdk-arm64/bin/jmap to provide /usr/bin/jmap (jmap) in auto mode
update-alternatives: using /usr/lib/jvm/java-21-openjdk-arm64/bin/jmod to provide /usr/bin/jmod (jmod) in auto mode
update-alternatives: using /usr/lib/jvm/java-21-openjdk-arm64/bin/jps to provide /usr/bin/jps (jps) in auto mode
update-alternatives: using /usr/lib/jvm/java-21-openjdk-arm64/bin/jrunscript to provide /usr/bin/jrunscript (jrunscript) in auto mode
update-alternatives: using /usr/lib/jvm/java-21-openjdk-arm64/bin/jshell to provide /usr/bin/jshell (jshell) in auto mode
update-alternatives: using /usr/lib/jvm/java-21-openjdk-arm64/bin/jstack to provide /usr/bin/jstack (jstack) in auto mode
update-alternatives: using /usr/lib/jvm/java-21-openjdk-arm64/bin/jstat to provide /usr/bin/jstat (jstat) in auto mode
update-alternatives: using /usr/lib/jvm/java-21-openjdk-arm64/bin/jstatd to provide /usr/bin/jstatd (jstatd) in auto mode
update-alternatives: using /usr/lib/jvm/java-21-openjdk-arm64/bin/jwebserver to provide /usr/bin/jwebserver (jwebserver) in auto mode
update-alternatives: using /usr/lib/jvm/java-21-openjdk-arm64/bin/serialver to provide /usr/bin/serialver (serialver) in auto mode
update-alternatives: using /usr/lib/jvm/java-21-openjdk-arm64/bin/jhsdb to provide /usr/bin/jhsdb (jhsdb) in auto mode
Setting up openjdk-21-jdk:arm64 (21.0.5+11-1) ...
update-alternatives: using /usr/lib/jvm/java-21-openjdk-arm64/bin/jconsole to provide /usr/bin/jconsole (jconsole) in auto mode
Setting up default-jdk-headless (2:1.21-76) ...
Setting up default-jdk (2:1.21-76) ...
                                                                             
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ javac VaultDoor3.Java
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
error: Class names, 'VaultDoor3.Java', are only accepted if annotation processing is explicitly requested
1 error
                                                                             
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ javac VaultDoor.java 
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
error: file not found: VaultDoor.java
Usage: javac <options> <source files>
use --help for a list of possible options
                                                                             
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ javac VaultDoor3.java
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
                                                                             
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ java VaultDoor3      
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
Enter vault password: PicoCTF{jU5t_a_sna_3lpm12g94c_u_4_m7ra41}
Access denied!
                                                                             
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ java VaultDoor3
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
Enter vault password: PicoCTF{jU5t_a_sna_3lpm12g94c_u_4_m7ra41}
Access denied!
                                                                             
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ java VaultDoor3
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
Enter vault password: PicoCTF{jU5t_a_sna_3lpm12g94c_u_4_m7ra41}
Access denied!
                                                                             
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ java VaultDoor3
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
Enter vault password: PicoCTF{jU5t_a_sna_3lpm12g94c_u_4_m7ra41}
Access denied!
                                                                             
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ javac VaultDoor3.java
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
VaultDoor3.java:42: error: ';' expected
        system.out.println(s)
                             ^
VaultDoor3.java:43: error: ';' expected
        system.out.println(buffer)
                                  ^
2 errors
                                                                             
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ javac VaultDoor3.java
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
VaultDoor3.java:42: error: package system does not exist
        system.out.println(s);
              ^
VaultDoor3.java:43: error: package system does not exist
        system.out.println(buffer);
              ^
2 errors
                                                                             
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ javac VaultDoor3.java
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
VaultDoor3.java:42: error: cannot find symbol
        System.Out.println(s);
              ^
  symbol:   variable Out
  location: class System
VaultDoor3.java:43: error: cannot find symbol
        System.Out.println(buffer);
              ^
  symbol:   variable Out
  location: class System
2 errors
                                                                             
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ javac VaultDoor3.java
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
                                                                             
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ java VaultDoor3      
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
Enter vault password: PicoCTF{jU5t_a_sna_3lpm12g94c_u_4_m7ra41}
jU5t_a_s21mpl3_a4gr4m_4_u_c79a21
jU5t_a_s21mpl3_a4gr4m_4_u_c79a21
Access denied!
                                                                             
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ java VaultDoor3
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
Enter vault password: picoCTF{jU5t_a_s21mpl3_a4gr4m_4_u_c79a21}        
jU5t_a_s4a_3lpm12g94c_u_4_m7ra41
jU5t_a_s4a_3lpm12g94c_u_4_m7ra41
Access denied!
                                                                             
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ 
```
