# Forensics
they have given picoctf challenges as excercise for practise
## information
[link for question](https://play.picoctf.org/practice/challenge/186?category=4&page=1)
in hints section its given view the details of the [pic](/cat.jpg)

so i looked for the metadata in the license section i saw something peculiar it seemed to be base64 encoded string
i looked for some decoding websites online and myguess proved to be correct

License                         : cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9

flag:- picoCTF{the_m3tadata_1s_modified}


## Matryoshka Doll
i was given with this doll [pic](/dolls.jpg)

in the hints its given that ~~~ Wait, you can hide files inside files? But how do you find them? ~~~
* At first by binwalk i got to know there are files that can be extracted
Ididnt remember the extraction by binewalk -e i tried binwalk -d doll.jpg
It didnt give me anything then i did foremost doll.jpg got output directory and then 
I got .zip file when extracted further in that directory directory i got base_images directory in that i found 2_c.jpg
By this time i remembered binwak -e
* Binwalk -e 2_cjpg
* Cd  _2_c.jpg.extracted
* Got 3_c.jpg
* Binwalk -e 3_c.jpg
* Cd _3_c.jpg.extracted
* Got 4_c.jpg
* Binwalk -e 4_c.jpg
* Cd _4_c.jpg.extracted
* Got flag.txt finally

  
*after solving this challenge i got to know really there are such dolls which contains dolls smaller than them inside them

flag:- picoCTF{4f11048e83ffc7d342a15bd2309b47de}


## tunn3l v1s10n
i was given with this kind of file

whenever i encounter such files which dont have any information i do binwalk but i didnt get anything usedful from that then i lookedd up for the metadata and found that file is a bmp pic. i changed its extension to bmp and then i tried opening it 

<p>
  it showed up incorrect header size <br>
  then i didnt know how to hexedit a file. i looked up for some some videos how to edit i came to know about the different type of editors i endedd up using <b>Hexedit</b> <br>
  i looked up for the headers of a png file in chatgpt <br> 
  first 14 bits shows the header the file contained header <br>
</p>

```shell
first 32 bits of the hexdump
00000000   42 4D 8E 26  2C 00 00 00  00 00 BA D0  00 00 BA D0
00000010   00 00 6E 04  00 00 32 01  00 00 01 00  18 00 00 00 

```
<p> chat gpt siggested the first 14 bits give information about header <br> while the next 4 bit
  s give the size of the header which is 40 bits thus the next 4 bits after 14 bits should be 28 00 00 00 </p>

```shell
the corrected version
00000000   42 4D 8E 26  2C 00 00 00  00 00 BA D0  00 00 28 00  
00000010   00 00 6E 04  00 00 32 01  00 00 01 00  18 00 00 00
```

then when i opened corrected png file this image showed up <br>
<img src=/new.png>

whenni was going through last year csoc problems i have seen such problem over there which is solved by extending length and width <br>
in that question also i saw that soorry{dig_more} was given in this problem notflag{sorry} is given
i updated height adn width in hexedit then the new image that was shown is

```shell
this is incomplete one
00000000   42 4D 8E 26  2C 00 00 00  00 00 BA D0  00 00 28 00  BM.&,.........(.
00000010   00 00 6E 04  00 00 32 01  00 00 01 00  18 00 00 00  ..n...2.........
00000020   00 00 58 26  2C 00 25 16  00 00 25 16  00 00 00 00  ..X&,.%...%.....
00000030   00 00 00 00  00 00 23 1A  17 27 1E 1B  29 20 1D 2A  ......#..'..) .*
```

```shell
comlete one
00000000   42 4D 8E 26  2C 00 00 00  00 00 BA D0  00 00 28 00  BM.&,.........(.
00000010   00 00 6E 04  00 00 32 03  00 00 01 00  18 00 00 00  ..n...2.........
00000020   00 00 58 26  2C 00 25 16  00 00 25 16  00 00 00 00  ..X&,.%...%.....
00000030   00 00 00 00  00 00 23 1A  17 27 1E 1B  29 20 1D 2A  ......#..'..) .*
```
<p> i changed the height bits from <b>32 01 00 00 </b> to <b>32 03 00 00 </b></p>
and got this 
<img src=tunnel.png>


