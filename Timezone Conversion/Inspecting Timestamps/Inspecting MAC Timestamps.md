
# Task 1:Inspecting MAC Timestamps

The following questions should be answered for the files in \Task1\C5W_timestamps.zip. Assume that the host that these files were generated on is in Eastern Timezone.

1. Was the target host on Eastern Standard Time or Eastern Daylight Time when these files were acquired? How do you know?

![image](https://user-images.githubusercontent.com/65653010/235359797-88c19ff8-a126-428f-882c-f2ca7981157c.png)
- Both refer to the US Eastern Time Zone during the Daylight Saving Time period, which is designated as Eastern Daylight Time (EDT).


2. Why are the Modified and Created timestamps on cybersecurity-image.png the same? What may this indicate?

 One possible reason is that the file was created and modified at the same time. This could happen if the file was copied or moved from another location on the same computer or if it was created by an automated process that sets both timestamps to the same value.

![image](https://user-images.githubusercontent.com/65653010/235462233-a70a908c-60e6-4b8f-aaac-2f8c2d4b0590.png)


3. When was sample_textdoc.txt first saved? What does the Modification time indicate?

![image](https://user-images.githubusercontent.com/65653010/235462444-e2ed6ad5-43db-46c6-b00d-539513565e3a.png)

4. What are the MAC timestamps for Notes.csv? What is the most likely reason that the Modified date is earlier than the Created date? 

![image](https://user-images.githubusercontent.com/65653010/235462657-8b53fb01-36d0-4b83-a346-92dfdae4049f.png)

5. Look at another document.txt's MAC timestamps. What is the most likely reason that the Modified date is earlier than the Created date?

![image](https://user-images.githubusercontent.com/65653010/235462766-0c3bde7c-f282-4e6d-aa95-733e32ae8267.png)

a. Bonus: What are another document.txt's MAC timestamps in UTC?
M - Modified - 2020-Nov-01 06:02:02 A - Accessed - 2021-Jul-30 07:33:48 C - Created - 2020-Nov-01 05:59:50

# Task 2:Inspecting Timestamps

## 1.In the Recycle Bin, "$I" files are generated to contain the metadata for a deleted file. Its hex code will detail the original file's size in bytes, deletion time, and path. For more information about Recycle Bin file format, refer to Cyber5w's Recycle Bin course. The information for its deletion time can be found at byte 0x10, and is 8 bytes long. For more information about Endianness, refer to Cyber5w's Computer and Data Representation course. Use DCode to conduct the following:

a. Open Task2$Recycle.Bin_backup$I111B13.jpg in a hex editor and locate its deletion time. Highlight the 8 bytes from byte 0x10 to 0x17, and copy the selection in Hexadecimal, Little Endian

![image](https://user-images.githubusercontent.com/65653010/235464249-1c097a2b-dfea-461d-abd0-39fcd4b261e1.png)

b. How many bits are in 8 bytes?

Ans 64 bytes

c. Open DCode and paste the hex in the "Value to Decode" field. In the "Decode Format" dropdown menu, select Windows: 64 bit Hex Value -Little Endian", then press "Decode"

![image](https://user-images.githubusercontent.com/65653010/235465245-4ae9ed73-dcdc-4e6c-9fe4-69e71ff44135.png)

 d. What is this file's deletion time in UTC?
 
 ![image](https://user-images.githubusercontent.com/65653010/235465386-ab319c25-d352-47b4-b350-26f7da2df590.png)
 
## 2.Many archive files, such as ZIP, RAR, 7Z, and Microsoft DOCX use timestamps to identify times that its containing files were created. For ZIP files, this timestamp can be located at bytes 0x0A to 0x0D (11th to 14th bytes) relative to the start of that entry's File Record. However, this 4-byte segment can be interpreted as 2 Little Endian bytes for the File Time (DOStime) and 2 Little Endian bytes for the File Date (DOSdate), which can be manipulated to be interpreted as MS-DOS: 32-bitHex Value in localtime. This is particularly useful for password-encrypted ZIP files that cannot be extracted through normal means.
a.Open c5w_timestamp-Sample.zip in a hex editor and locate the first entry's creation timestamp (should be at 0xA-0xD). Highlight the 4 bytes at that location in Hexadecimal, Little Endian.

![image](https://user-images.githubusercontent.com/65653010/235466114-05c3e7bd-7bd9-4a30-84d6-473d5797d292.png)

b.How many bits are in 4 bytes?

32 bytes

c.Open DCode and paste this value into the "Value to Decode" field, applying the "Decode Format:" equal to "MS-DOS: 32-bitHex Value.

![image](https://user-images.githubusercontent.com/65653010/235466554-94d7a862-1fd6-41d3-8c99-07fbc6fca27f.png)

d.What time was this file created?

2021-03-23 09:14:42

e. What timezone is stored in archive files?

Localtime zone

## 3.Certain file types will include "ExifData", which is usually metadata about an image and the camera that took it. The most common file type that will include Exif Data is JPG files. Exif data usually includes a lot of information, such as the make and model of the camera that took the picture, the resolution of the picture, the GPS location that the picture was taken at, the camera's lens configuration, exposure, color encoding, flash, field of depth, time the file was taken, and more. This data can be read in Phil Harvey's ExifTool, a hex editor, an Exif Data Viewer online
a. Open c5w_exif-pink_rose.jpg in a hex editor andreview its Exif data (look for the word, "Exif"). Most of the Exif data should be in plaintext, making it readable without decoding it.

![image](https://user-images.githubusercontent.com/65653010/235467415-52adcba3-8edd-40de-a03d-317c4a6418f7.png)

b.The Exif data will automatically save the time in localtime, the timezone that the file was taken in. Based on parsing the file in a hex editor, what time was the picture taken?

![image](https://user-images.githubusercontent.com/65653010/235467877-a91da160-fd9c-4899-ba04-47ff86f58c84.png)

c. Verify the hex timestamp by comparing it to the output of exiftool. Run exiftool(-k).exe against c5w_exif-pink_rose.jpg by issuing the command, "exiftool(-k).exe c5w_exif-pink_rose.jpg". What timestamp does it show that the photo was taken?

![image](https://user-images.githubusercontent.com/65653010/235468422-cefbd981-8b4a-4d30-ada7-ccebc343932e.png)

![image](https://user-images.githubusercontent.com/65653010/235468568-fa554d1f-0ca1-4ac4-aec8-643b6983c850.png)

d. Bonus: What time was the picture taken in UTC? Hint: See what other information is stored in Exif metadata that can help you locate the appropriate timezone.

![image](https://user-images.githubusercontent.com/65653010/235468787-b929f444-34b0-4e89-80a8-f45a61f30e5a.png)




