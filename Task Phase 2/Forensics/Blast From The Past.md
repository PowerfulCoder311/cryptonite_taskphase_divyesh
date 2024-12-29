# Blast From The Past (additional challenge 1)
Challenge:  
The judge for these pictures is a real fan of antiques. Can you age this photo to the specifications? Set the timestamps on this picture to 1970:01:01 00:00:00.001+00:00 with as much precision as possible for each timestamp. In this example, +00:00 is a timezone adjustment. Any timezone is acceptable as long as the time is equivalent. As an example, this timestamp is acceptable as well: 1969:12:31 19:00:00.001-05:00. For timestamps without a timezone adjustment, put them in GMT time (+00:00). The checker program provides the timestamp needed for each. Use this picture.

Additional details will be available after launching your challenge instance.

__After Launching Instance__: Submit your modified picture here: nc -w 2 mimas.picoctf.net 60162 <original_modified.jpg   
Check your modified picture here: nc mimas.picoctf.net 58611

The hint mentions exiftools for reading metadata.  
Studying exiftool commands:
```
0) Extract information from a file

    exiftool a.jpg

    A basic command to extract all metadata from a file named a.jpg.

1) Basic write example

    exiftool -artist=me a.jpg

    Writes Artist tag to a.jpg. Since no group is specified, EXIF:Artist will be written and all other existing Artist tags will be updated with the new value ("me").

2) Write multiple files

    exiftool -artist=me a.jpg b.jpg c.jpg

    Writes Artist tag to three image files.

3) Write to all files in a directory

    exiftool -artist=me c:/images

    Writes Artist tag to all files in directory c:/images.

4) Write multiple tags

    exiftool -artist="Phil Harvey" -copyright="2011 Phil Harvey" a.jpg

    Writes two tags to a.jpg.

5) Extracting duplicate tags

    exiftool -a -u -g1 a.jpg

    Print all meta information in an image, including duplicate and unknown tags, sorted by group (for family 1).
```
__Reading the File__:
```
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ exiftool original.jpg 
ExifTool Version Number         : 13.00
File Name                       : original.jpg
Directory                       : .
File Size                       : 2.9 MB
File Modification Date/Time     : 2024:12:29 23:43:30+05:30
File Access Date/Time           : 2024:12:29 23:43:30+05:30
File Inode Change Date/Time     : 2024:12:29 23:43:30+05:30
File Permissions                : -rw-rw-r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
Exif Byte Order                 : Little-endian (Intel, II)
Image Description               : 
Make                            : samsung
Camera Model Name               : SM-A326U
Orientation                     : Rotate 90 CW
X Resolution                    : 72
Y Resolution                    : 72
Resolution Unit                 : inches
Software                        : MediaTek Camera Application
Modify Date                     : 2023:11:20 15:46:23
Y Cb Cr Positioning             : Co-sited
Exposure Time                   : 1/24
F Number                        : 1.8
Exposure Program                : Program AE
ISO                             : 500
Sensitivity Type                : Unknown
Recommended Exposure Index      : 0
Exif Version                    : 0220
Date/Time Original              : 2023:11:20 15:46:23
Create Date                     : 2023:11:20 15:46:23
Components Configuration        : Y, Cb, Cr, -
Shutter Speed Value             : 1/24
Aperture Value                  : 1.9
Brightness Value                : 3
Exposure Compensation           : 0
Max Aperture Value              : 1.8
Metering Mode                   : Center-weighted average
Light Source                    : Other
Flash                           : On, Fired
Focal Length                    : 4.6 mm
Sub Sec Time                    : 703
Sub Sec Time Original           : 703
Sub Sec Time Digitized          : 703
Flashpix Version                : 0100
Color Space                     : sRGB
Exif Image Width                : 4000
Exif Image Height               : 3000
Interoperability Index          : R98 - DCF basic file (sRGB)
Interoperability Version        : 0100
Exposure Mode                   : Auto
White Balance                   : Auto
Digital Zoom Ratio              : 1
Focal Length In 35mm Format     : 25 mm
Scene Capture Type              : Standard
Compression                     : JPEG (old-style)
Thumbnail Offset                : 1408
Thumbnail Length                : 64000
Image Width                     : 4000
Image Height                    : 3000
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Time Stamp                      : 2023:11:21 02:16:21.420+05:30
MCC Data                        : United States / Guam (310)
Aperture                        : 1.8
Image Size                      : 4000x3000
Megapixels                      : 12.0
Scale Factor To 35 mm Equivalent: 5.4
Shutter Speed                   : 1/24
Create Date                     : 2023:11:20 15:46:23.703
Date/Time Original              : 2023:11:20 15:46:23.703
Modify Date                     : 2023:11:20 15:46:23.703
Thumbnail Image                 : (Binary data 64000 bytes, use -b option to extract)
Circle Of Confusion             : 0.006 mm
Field Of View                   : 71.5 deg
Focal Length                    : 4.6 mm (35 mm equivalent: 25.0 mm)
Hyperfocal Distance             : 2.13 m
Light Value                     : 4.0
                                                                             
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ 
```
Studying about exiftool commands and reading writeups, i find that the best way to alter the time stamp is to use the -AllDates arguement.

desired time stamp: 1970:01:01 00:00:00.001+00:00  
This is to be edited in a duplicate of the original.jpg. So we first duplicate original.jpg and name it original_modified.jpg 
__Using -AllDates__:
```
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ exiftool -AllDates="1970:01:01 00:00:00.001+00:00" original_modified.jpg
    1 image files updated
                                                                             
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ 
```
Now checking our modified image:
```
┌──(divyesh㉿macbook)-[~]
└─$ cd Downloads                                           
                                                                             
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ nc -w 2 mimas.picoctf.net 56842 < original_modified.jpg
                                                                             
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ nc mimas.picoctf.net 63531
MD5 of your picture:
e7537a20fd614f08232eaa16d4f6587a  test.out

Checking tag 1/7
Looking at IFD0: ModifyDate
Looking for '1970:01:01 00:00:00'
Found: 1970:01:01 00:00:00
Great job, you got that one!

Checking tag 2/7
Looking at ExifIFD: DateTimeOriginal
Looking for '1970:01:01 00:00:00'
Found: 1970:01:01 00:00:00
Great job, you got that one!

Checking tag 3/7
Looking at ExifIFD: CreateDate
Looking for '1970:01:01 00:00:00'
Found: 1970:01:01 00:00:00
Great job, you got that one!

Checking tag 4/7
Looking at Composite: SubSecCreateDate
Looking for '1970:01:01 00:00:00.001'
Found: 1970:01:01 00:00:00.703
Oops! That tag isn't right. Please try again.
                                                                             
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ 
```
Therefore, the milliseconds are not accurate. Trying to edit this specific component...
```
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ exiftool -AllDates="1970:01:01 00:00:00.001+00:00" original_modified.jpg
    1 image files updated
                                                                             
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ exiftool -SubSecCreateDate="1970:01:01 00:00:00.001+00:00" original_modified.jpg
    1 image files updated
```
Checking again...
```
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ nc -w 2 mimas.picoctf.net 56842 < original_modified.jpg
                                                                             
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ nc mimas.picoctf.net 63531
MD5 of your picture:
48bf66a48e3a8253fdd85787e5e60cad  test.out

Checking tag 1/7
Looking at IFD0: ModifyDate
Looking for '1970:01:01 00:00:00'
Found: 1970:01:01 00:00:00
Great job, you got that one!

Checking tag 2/7
Looking at ExifIFD: DateTimeOriginal
Looking for '1970:01:01 00:00:00'
Found: 1970:01:01 00:00:00
Great job, you got that one!

Checking tag 3/7
Looking at ExifIFD: CreateDate
Looking for '1970:01:01 00:00:00'
Found: 1970:01:01 00:00:00
Great job, you got that one!

Checking tag 4/7
Looking at Composite: SubSecCreateDate
Looking for '1970:01:01 00:00:00.001'
Found: 1970:01:01 00:00:00.001
Great job, you got that one!

Checking tag 5/7
Looking at Composite: SubSecDateTimeOriginal
Looking for '1970:01:01 00:00:00.001'
Found: 1970:01:01 00:00:00.703
Oops! That tag isn't right. Please try again.
                                                                             
┌──(divyesh㉿macbook)-[~/Downloads]
└─$
```
Now repeating the steps for this component and rechecking...
```
Checking tag 5/7
Looking at Composite: SubSecDateTimeOriginal
Looking for '1970:01:01 00:00:00.001'
Found: 1970:01:01 00:00:00.001
Great job, you got that one!

Checking tag 6/7
Looking at Composite: SubSecModifyDate
Looking for '1970:01:01 00:00:00.001'
Found: 1970:01:01 00:00:00.703
Oops! That tag isn't right. Please try again.
```
repeating and rechecking
```
Checking tag 6/7
Looking at Composite: SubSecModifyDate
Looking for '1970:01:01 00:00:00.001'
Found: 1970:01:01 00:00:00.001
Great job, you got that one!

Checking tag 7/7
Timezones do not have to match, as long as it's the equivalent time.
Looking at Samsung: TimeStamp
Looking for '1970:01:01 00:00:00.001+00:00'
Found: 2023:11:20 20:46:21.420+00:00
Oops! That tag isn't right. Please try again.
```
repeating
```
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ exiftool -Samsung:TimeStamp="1970:01:01 00:00:00.001+00:00" original_modified.jpg
Warning: Sorry, Samsung:TimeStamp doesn't exist or isn't writable
Nothing to do.
                                                                             
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ 
```
The Samsung component is not editable by exiftools. Trying binary editing:

```
                                                                             ┌──(divyesh㉿macbook)-[~]
└─$ sudo apt install hexedit
[sudo] password for divyesh: 
Installing:                     
  hexedit

Summary:
  Upgrading: 0, Installing: 1, Removing: 0, Not Upgrading: 623
  Download size: 27.7 kB
  Space needed: 93.2 kB / 13.4 GB available

Get:1 http://http.kali.org/kali kali-rolling/main arm64 hexedit arm64 1.6-1+b1 [27.7 kB]
Fetched 27.7 kB in 2s (15.0 kB/s)  
Selecting previously unselected package hexedit.
(Reading database ... 395023 files and directories currently installed.)
Preparing to unpack .../hexedit_1.6-1+b1_arm64.deb ...
Unpacking hexedit (1.6-1+b1) ...
Setting up hexedit (1.6-1+b1) ...
Processing triggers for kali-menu (2024.4.0) ...
Processing triggers for man-db (2.13.0-1) ...
                                                                             
┌──(divyesh㉿macbook)-[~]
└─$ sudo apt install bless  
Error: Unable to locate package bless
                                                                             
┌──(divyesh㉿macbook)-[~]
└─$ sudo apt install ghex
Installing:                     
  ghex
                                                                             
Installing dependencies:
  libadwaita-1-0  libappstream5  libgtkhex-4-1  libstemmer0d  libxmlb2
```
```
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ ghex original_modified.jpg
```
Studying about samsung timestamps, it is basically the image utc and the end of the file. Since the time stamp required is 1 millisecond after 1970, and computers start counting seconds from 1970, the encoded number should be 0000000000001.
Trying again
```
Checking tag 5/7
Looking at Composite: SubSecDateTimeOriginal
Looking for '1970:01:01 00:00:00.001'
Found: 1970:01:01 00:00:00.001
Great job, you got that one!

Checking tag 6/7
Looking at Composite: SubSecModifyDate
Looking for '1970:01:01 00:00:00.001'
Found: 1970:01:01 00:00:00.001
Great job, you got that one!

Checking tag 7/7
Timezones do not have to match, as long as it's the equivalent time.
Looking at Samsung: TimeStamp
Looking for '1970:01:01 00:00:00.001+00:00'
Found: 1970:01:01 00:00:00.001+00:00
Great job, you got that one!

You did it!
picoCTF{71m3_7r4v311ng_p1c7ur3_3e336564}
```
flag -> picoCTF{71m3_7r4v311ng_p1c7ur3_3e336564}
