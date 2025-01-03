# tunn3l v1s1on

Challenge: We found this file. Recover the flag

The downloaded file contains no extension. using the file command on the file
```
┌──(divyesh㉿macbook)-[~]
└─$ cd Downloads 
                                                                             
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ file tunn3l_v1s10n
tunn3l_v1s10n: data
                                                                             
┌──(divyesh㉿macbook)-[~/Downloads]
└─$ 

```
This shows that the file format is not recognized. Finally opening the file with the hexeditor, we see that the file header starts with BM which is the same as a BME file.

Despite renaming the file to tunn3l_v1s10n.bmp, standard image viewers failed to display it properly, suggesting a corrupted or intentionally altered header. Consulting the BMP file format specification, we noted discrepancies in the header fields, particularly in the DIB header size and the offset to the pixel data.

Using a hex editor, we corrected these fields:
	->	DIB Header Size: Changed to the standard 40 bytes (28 00 00 00 in hexadecimal).
	-> Pixel Data Offset: Set to 54 bytes (36 00 00 00 in hexadecimal), accounting for the 14-byte file header plus the 40-byte DIB header.

After making these adjustments and saving the file, we attempted to open the image again. This time, the image displayed, but it appeared distorted, and a visible message read “notaflag,” indicating further modifications were necessary.

Recognizing that the image’s dimensions might be incorrect, we revisited the BMP header. The width was correctly specified, but the height field seemed inaccurate. By calculating the expected image size based on the file’s total byte count and adjusting the height accordingly, we set the height to a value that matched the image’s data.

Upon reopening the corrected image, it rendered correctly, revealing the hidden flag:

picoCTF{qu1t3_a_v13w_2020}

This process involved identifying the file type through its header signature, correcting the BMP header fields to standard values, and adjusting the image dimensions to properly render the hidden content.
