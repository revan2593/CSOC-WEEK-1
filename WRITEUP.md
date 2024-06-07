
# Forensics
they have given picoctf challenges as excercise for practise



## information
[link for question](https://play.picoctf.org/practice/challenge/186?category=4&page=1)
in hints section its given view the details of the [pic](/pics/cat.jpg)
<br>
<img src=/pics/cat.jpg>
<br>

so i looked for the metadata in the license section i saw something peculiar it seemed to be base64 encoded string
i looked for some decoding websites online and myguess proved to be correct

License                         : cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9

flag:- picoCTF{the_m3tadata_1s_modified}


## Matryoshka Doll
i was given with this doll [pic](/pics/dolls.jpg)

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
<img src=/pics/new.png>

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
<img src=/pics/tunnel.bmp>
and the flag is <b>picoCTF{qu1t3_1_v13w_2020}</b>


## MacroHard WeakEdge
i was given with a ppt. in descriptiojn it was gievn <br> <b>I've hidden a flag in this file. Can you find it? Forensics is fun.pptm</b>
its given they have hided the image thus i tried binwalk and i got them extracted <br>
and i that extractedd files i got 0.zip. i unzipped them and saw something special. <br>

<img src=/pics/Screenshot1.png>
<br>
you can see the last line there is file named hidden in the unzipped file <b> ppt/slideMasters/hidden</b> 
<br>
but i didnt observe this at first i started to explore the other files which was ofcourse waste of time
once i opened hidden after so many exploration <br>
 i saw some random strings in which each line is seperated by space.this string wasnt random string base64 encoded string of flag i decoded it with hekp of available online sites<br>
and i got the flag <b>picoCTF{D1d_u_kn0w_ppts_r_z1p5}
</b>



## Enhance!
i was given with this [pic](/pics/drawing.flag.svg)
<br> 
i checcked the metadata and didnt find anything special
<br> even the file format was correct 
<br> i tried binwalk and it didnt have any files embedded
<br> then i did strings and found flag in two parts

<img src=/pics/Screenshot2.png>

and the flag is <b>
picoCTF{3nh4nc3d_d0a757bf}
</b>

## File types 
its the most hectic question accpording to me i wasted so much time <br>
but learnt different type of archieves. and the ways to unarchieving them.
<br> i was given with a pdf  file but its not in correct form when i used file command i came to know its an shell script which produces a file named flag
<br> while running this file i didnt have uudecode command in my system downloaded it using  sudo apt install sharutils
<br>
the command which was handy was <b>file</b>
by this command i first checked for the file form and then renamed it using <b>mv </b>
command i knew some of them like bzip tar lzip and others were unknown i searched in it for commands to unarchieve them
finally you get file having filetype ASCII text which contains s tring 
```shell
7069636f4354467b66316c656e406d335f6d406e3170756c407431306e5f
6630725f3062326375723137795f39353063346665657d0a
```
i at first  assumed its base64 encoded string but when decoded with base64 i got meaning less string then i again looked at the alphabets in the string all were digits betweeen 0-9 and alphabets from a-g then i tried to decode it assuming its base16 or  hex encided string 
and finally got the flag <b>picoCTF{f1len@m3_m@n1pul@t10n_f0r_0b2cur17y_950c4fee} </b>


## hideme

i am given with the following pic <br>
<img src=/pics/flag.png>
<br>
the name of the challenge is hideme so i had gut feeling that some file is hidden in hit and i tried binwalk 
and found 
<img src=/pics/Screenshot3.png>
it contains an image in directory named secret
which intern had the flag <br>
<img src=/pics/flag1.png>
<br>
<b>picoCIF{Hiddinng_An_imag3_within_@n_image_dc2ab58f}
 </b>


## MSB

the name of the problem msb which is short form of the most significant bit. and discription says
```shell
This image passes LSB statistical analysis, but we can't help but think there must be something to the visual artifacts present in this image...
``` 
i already had the idea that a message can be encrypted by changing bits of an image
<br> used <a href="https://github.com/Pulho/sigBits"> this tool </a>

and i got complete paragarph and i tried searching for the word picoCTF using grep 
```
grep -o "picoCTF"
```
<br> and i found the phrase picoCTF exists in that 
then i converted space into newline charcter using tr command  then grepped for the phrase "pico"
<br>

```
cat outputSB.txt | tr " " "\n" | grep  "pico"
```

and i found the flag <b>picoCTF{15_y0ur_que57_qu1x071c_0r_h3r01c_572ad5fe}</b>



## Extension

a txt file us given but its not txt file. when checked for the file type i came to know that its png file and then i changed the extension to png
i got pic <br>
<img src=/pics/xxx.png>
<br>
flag is <b>picoCTF{now_you_know_about_extensions}</b>

<br>

<br>

<br>

<br>

<br>

<br>

<br>


# OSINT

## Sakura Room

this challenge was good but this challenge has become old. so there are so many fake accounts its difficult to
conclude which social media account is correct


### TIP-OFF
<img src=/pics/sakurapwnedletter.svg> <br>
in the metadata we can find the source of the picture <br>
<img src=/pics/Screenshot4.png>
<br>
in export-filename section you can find the path of th image 
```
/home/SakuraSnowAngelAiko/Desktop/pwnedletter.png
```
by this we can confirm the username of attacker goes by
<b>SakuraSnowAngelAiko</b>


### RECONNAISSANCE


its given we can find other accounts which go by same user name
by <a href=https://github.com/sherlock-project/sherlock >sherlock tool<a> <br>
i got its git account by that username hereis <a href=https://github.com/sakurasnowangelaiko>link</a>
<br>
then by google searching the username i came across the twitter account of the 
[user](https://x.com/sakuraloveraiko?lang=en)
<br>
the twitter or x account has posted this <a href=https://x.com/SakuraLoverAiko/status/1355364359090757635>post</a> 
<br>
by which we can confirm user name of the hacker is Aiko Abe
<br>
when i explored complete git i didnt get any idea to find the email id of the hacker. 
i searched the web how can i find the mail by using a git account of user
<br>
i came across this <a href=https://x.com/SakuraLoverAiko/status/1355364359090757635>post</a> 
and found the mail id as <b>sakurasnowangel@users.noreply.github.com</b>
but its not correct :(
<br>
<img src=/pics/Screenshot5.png>
<br>
i actually couldnt find email id mysef took help of the walkthrough of this room
<br>
then i came to know that by php public key we can derive the information about that and i fount this [site](https://8gwifi.org/pgpdump.jsp)
<br>
<img src=/pics/Screenshot6.png>
<br>
we found the mail id as
<b>SakuraSnowAngel83@protonmail.com</b>
<br>




### UNVEIL
by the git acount we got in depository we can find ETH depository
<br>
when seen edits made to this depository you find something interesting <br>

<img src=/pics/Screenshot8.png>
<br>'

``` 

What is the attacker's cryptocurrency wallet address?
```
we can see the crypto currency adress of the attacker <b>0xa102397dbeeBeFD8cD2F73A89122fCdB53abB6ef</b> <br> by googling this id we get thia
<a href=https://etherscan.io/address/0xa102397dbeebefd8cd2f73a89122fcdb53abb6ef>website</a> <br> 
<img src=/pics/Screenshot7.png> 
<br>
```
What cryptocurrency does the attacker own a cryptocurrency wallet for?
```
 and at first the depository name is ETH which means <b>Ethereum</b>


 ```
What mining pool did the attacker receive payments from on January 23, 2021 UTC?
```
its again <b>Ethermine</b>
<br>
<img src=/pics/Screenshot9.png>
<br>

```
What other cryptocurrency did the attacker exchange with using their cryptocurrency wallet?
```
<br>
<img src=/pics/Screenshot10.png>
<br>
in this we can see its <b>Tether</b>

### TAUNT

```
What is the attacker's current Twitter handle?
```
i already found her twitter handle username <b>SakuraLoverAiko</b>

<br>

<img src=/pics/Screenshot11.png>
<br>

### HOMEBOUND

in her X handle i got some pics
<br>
<img src=/pics/Esh-uTvUcAc-sXC.jpeg>
<br>
this pic has the caption 
```
Checking out some last minute cherry blossoms before heading home!
```

in a pic she mentioned the place  ""Bethesda""
<br>
<img src=/pics/Screenshot13.jpg>
<br>
it means she was somewhere near this area before living to her home
by googling this picture i came to know its washinngton 

<br>
<img src=/pics/Screenshot12.png>
<br>
short for of the sirport at washinton is <b>DCA</b>

<br>
next attacker posted this airport launge as

```
My final layover, time to relax!
```
<img src=/pics/EsiM12KVoAEhAsI.png>
<br>

when googled its launge of japan air lines at tokyo
and short form for the airport at tokyo is <b> HND </b>

<br>

```
What lake can be seen in the map shared by the attacker as they were on their final flight home?

```

she uploaded this map image <br>
<img src=/pics/EsiNRuRU0AEH32u.jpeg>
<br>

 by this all research we came to know that is from japan by google map i searched and japan and tred to match the map with picture.
 and i came to know its <b>Lake Inawashiro</b>

 <img src=/pics/Screenshot14.png>


```
What city does the attacker likely consider "home"?
```
in hint section of wifi question a screenshot is given 
<br>
<img src=/pics/deeppaste.png>

 <br>
 in this city name is given as <b>Hirosaki</b>




<br>



<br>



<br>


<br>


<br>


















```
2. https://gralhix.com/list-of-osint-exercises/ Go here and do these (preferably in the order):
    1. OSINT Exercise 6
    2. OSINT Exercise 4
    3. OSINT Exercise 3
    4. OSINT Exercise 14
    5. OSINT Exercise 26
```

 

### 1. OSINT Exercise 6
<img src=/pics/osintexercise006.webp>
<br>
all we have to do is <b>Fact Check </b> this news
<br> by google searching for only car blast image we get this <a href=https://www.iraqinews.com/iraq-war/8-people-killed-wounded-bomb-blast-near-shops-south-baghdad/>artical</a> describing an attack in iraq dated  <b>22nd October 2015</b> which is like 5year before this post was even posted
<br>
<img src=/pics/Screenshot15.png>
thus this post by pakistan reporter is completely <b>False</b>



<br>
###  2. OSINT Exercise 4

<img src=/pics/osintexercise004.webp>
our objective is to find

```
a) What is the name of the resort?
b) What are the coordinates of the island?
c) In which cardinal direction was the camera facing when the photo was taken?



```
<br>
by goggle searching we find the exact image in the page of resort named <a href=https://oanresort.wixsite.com/chuuk/about><b>Oan resort</b></a>
<br>
<img src=/pics/Screenshot16.png>
<br>
by searching for the Oan resort in google maps we find its present in <b>Oan island</b> and coordinate are

```
7.362306, 151.756096
```

### 3. OSINT Exercise 3
our objective is

```
Your task is to find out the name and coordinates of the location seen below.
```

by seaching for this pic in google i found same persons pic standing at the same place (but in different angle) i ended up to this news <a href=https://www.atalayar.com/en/articulo/politics/somalia-erdogans-spearhead-east-africa/20200508113246145709.html> article </a>
<br>
<img src=/pics/Screenshot17.png>
<br>



in this screenshot below the photo you can see the name of the place as <b>Ankara Presidential Complex
</b> ofcourse from question we already know its t=a picture in turkey
by searching it in google map i got this result as only street view available



<br>

<img src=/pics/Screenshot18.png>
<br>



by comparing some other pics of the place i conclude its pic of same monument



<br>
<img src=/pics/Screenshot19.png>
<br>
i get these as coordinates

```
39.931549, 32.800966
```


<br>
###  4. OSINT Exercise 14

i was given with youtube video [link](https://youtu.be/myTG1LpMN7g)
<br>
i took scrrenshot of the image and started searching for the exact matches. in the given time stamp says its video of 24th october 2016. there werre many videos of the same clip uploaded in 2018 but one specific youtube video with fc barcelona dp showedup same video clip
<br> [link here](https://www.youtube.com/watch?v=lvGpouFqmJ0)
<br>
there was nothing in video description but the name of the video was <b>
Cutremur Chisinau 24.09.2016</b> which in english when translated <b>chisinau earthquake</b>
<br>
the title is in romanian language
<br>
i searched the same phrase <b>Cutremur Chisinau 24.09.2016</b>and i got a news article in romanian language 
<br>
[link here](https://www.moldpres.md/en/news/2016/09/24/16007583#)
<br>
<img src=/pics/Screenshot20.png>
which mentioned the magnitude of earthquake was 5.8
<br>i couldnt find coordinates so watchedd its walkthrough video 

### 5. OSINT Exercise 26


i am given zip file which contains these four pics
<img src=/pics/IMG_2597.jpg>
<br>
<img src=/pics/IMG_2626.jpg>
<br>
<img src=/pics/IMG_2658.jpg>
<br>
<img src=/pics/IMG_2747.jpg>
<br>




and this [video](/pics/IMG_2677.MOV)
the sequnce of the name of the pics tells us the order of the pictures taken 
by googling first pic i came to know its <b>Chorsu Bazaar</b> situated in city <b>Tashkent, the capital city of Uzbekistan.</b>
<br>
and the by googling next pic i came to know its <b>Anhor Lokomotiv</b> in same city
i tried googling next pic but i couldnt get anything interesting but i confirmed its from the same city as when i searched for this pic in yandex 
i got this 
<br>
<img src=/pics/screenshot.png>
<br>
i got this instagram account suggested [link](https://www.instagram.com/azajony.1/?hl=am-et)<br>
when i checked other post of this account i got this in a reel
<br>
<img src=/pics/screenshot1.png>
<br>
when searched for the place in background  i got results which said its a monument from the same city <b>Tashkent</b>


