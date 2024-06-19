# Cryptography
the challenges we need to solve as practise problems are 
```


Solve the following Cryptohack challenges:

INTRODUCTION
ALL
GENERAL
ENCODING
ALL except "Encoding Challenge"
XOR
ALL except "Lemur XOR" (you can quickly whip up a script if you want to solve it, or use software like GIMP, Photoshop, or maybe Paint.NET)
MATHEMATICS
ALL
SYMMETRIC CIPHERS
HOW AES WORKS
Keyed Permutations
Resisting Bruteforce
Structure of AES
RSA
STARTER
ALL
PUBLIC EXPONENT
Salty
```
## INTRODUCTION
### Finding Flags
the flag is directly mentioned in the challenge itself as its first challenge
**crypto{y0ur_f1rst_fl4g}**

### Great Snakes
i was given with a python executable script ehich when opened had a list containing the ascii values of the each alphabet of the flag and then it converted them each into letter inorder to print the flag

the flag is  
**crypto{z3n_0f_pyth0n}**

### Network Attacks
i was given with host adress to connect and a pyhton file i opened the python script and saw it was also connecting to the same host and wwas sending some message in json form into a function which further encoded the message and sending it to the server 


when i saw the file it was sending json message
```
{
    "buy" : "clothes"
}
```
first i changed the clothes into flags 
when i executed the script i didnt get the flag
then i tried some random strings which also didnt work and then i tried the string "sell" instead of "buy"

then it came up with message you can only buy the flags

then when i ran through challenge againn i saw the phrase  
```
Send a JSON object with the key buy and value flag.

```
then i changed it to 
```
{
    "buy" : "flag"
}
```
then it came with flag **crypto{sh0pp1ng_f0r_fl4g5}**





## General

### ENCODING

#### ASCII
i was given with array containing ascii values of the each alphabet of the flag.

```
[99, 114, 121, 112, 116, 111, 123, 65, 83, 67, 73, 73, 95, 112, 114, 49, 110, 116, 52, 98, 108, 51, 125]
```

i used python to decode the flag as below


```
list=[99, 114, 121, 112, 116, 111, 123, 65, 83, 67, 73, 73, 95, 112, 114, 49, 110, 116, 52, 98, 108, 51, 125]
str=""
for item in list:
   str=str+chr(item)
print(str)
```

#### Hex
i was given with hex string 
i had knowledge how a string is converted into hex form

for example take string "hello"

the ascii value of each alphabets of string are considered then each ascii value is comverrtedd into their respective hex values and they are clubbed back into a single string

'h'=68  ,'e'=65    ,'l'=6C    ,'l'=6C   ,'o'=6F
hello in hex is "68656C6C6F"

each character is two bits long

```
str="63727970746f7b596f755f77696c6c5f62655f776f726b696e675f776974685f6865785f737472696e67735f615f6c6f747d"
i=0
list=[]


while(i<len(str)):
   str2=""
   if i<len(str):
       str2=str2+str[i]
   if i+1<=len(str):
       str2=str2+str[i+1]
   list.append(str2)
   i=i+2
ans=""
print(list)
for item in list:
   res = int(item,16)
   ans=ans+chr(res)
print(ans)

```
this prints the ans as **crypto{You_will_be_working_with_hex_strings_a_lot}**

then after some research i found
```
str="63727970746f7b596f755f77696c6c5f62655f776f726b696e675f776974685f6865785f737472696e67735f615f6c6f747d"
print(bytes.fromhex(str))
```
which is simple form of the before code

#### Base64
i was given with base64 string 
i red how base64 works by this 
[link](https://www.lifewire.com/base64-encoding-overview-1166412)



base 64 can be decoded by using the following function


the actual idea is converting the given string into their respective value according to base64 table
then converting them into banary and clubbing them together and converting them 8-bit groups gives us encoded msg string in binary form
```
import base64
str="72bca9b68fc16ac7beeb8f849dca1d8a783e8acf9679bf9269f7bf"
print(base64.b64encode(bytes.fromhex(str)))
```
the flag is **crypto/Base+64+Encoding+is+Web+Safe/**


#### Bytes and Big Integers

 in the given challenge its mentioned how a message made up of alphabets is converted into number
 ```
 The most common way is to take the ordinal bytes of the message, convert them into hexadecimal, and concatenate. This can be interpreted as a base-16/hexadecimal number, and also represented in base-10/decimal.

```
we are given with large number in order to convert it back into message we need to first convert it into its hex form
then converting it into encoded message by breaking the hex string into two bits and converting those two bits into respective alphabet using ascii values

as i mentioned in the prior challenge this all can be done by a simple function bytes.fromhex()

```
i=11515195063862318899931685488813747395775516287289682636499965282714637259206269
h=hex(i)
h=h[2:]


print(bytes.fromhex(h))
```

this when i first solved i constructed this script



```

j=11515195063862318899931685488813747395775516287289682636499965282714637259206269
h=hex(j)
str=h[2:]
i=0
list=[]


while(i<len(str)):
   str2=""
   if i<len(str):
       str2=str2+str[i]
   if i+1<=len(str):
       str2=str2+str[i+1]
   list.append(str2)
   i=i+2
ans=""
print(list)
for item in list:
   res = int(item,16)
   ans=ans+chr(res)
print(ans)
```

### XOR
#### XOR Starter
in this challenge we are given with a string "label" all we need to do is XOR each alphabets ascii value with number 13 (given in challenge)


all we need to traverse through the string convert each alphabets into its ascii value then xor with 13

```
str="label"
ans=""
for item in str:
   i=ord(item)
   b=13
   a=i^b
   ans=ans+chr(a)
print(ans)

```
by this script the string we obtain is "aloha"
thus flag is **crypto{aloha}**

#### XOR Properties
the commutative property of XOR function is explained at this challenge and challenge is based on the same property

we are given with keys and their xors in the hex form 
i have used them to do so
````
key1="a6c8b6733c9b22de7bc0253266a3867df55acde8635e19c73313"
key12="37dcb292030faa90d07eec17e3b1c6d8daf94c35d4c9191a5e1e"
key23="c1545756687e7573db23aa1c3452a098b71a7fbf0fddddde5fc1"
key123f="04ee9855208a2cd59091d04767ae47963170d1660df7f56f5faf"
key13=int(key12,16)^int(key23,16)
key2f=int(key123f,16)^key13
key12f=int(key1,16)^key2f
keyf=int(key12,16)^key12f
h=hex(keyf)[2:]
print(bytes.fromhex(h))
````

```
BETTER METHOD
keyab= is xor of keya and keyb
the challenge can be solved simply by xoring key1 with key12 by which we get key2 then xoring new found key2 with key23 woiuld have given us with key3
'then xoring all three with key123f would have given the flag
```

the thing i did in the script is my first attempt seems like rookie 

and the flag is **Crypto{x0r_i5_ass0c1at1v3}**

#### Favourite byte
in the challenge its given 
```
I've hidden some data using XOR with a single byte, but that byte is a secret. Don't forget to decode from hex first.
```
single byte has been used to encode the flag and the given string is in hex form first it should be converted to int for xoring

```
str="73626960647f6b206821204f21254f7d694f7624662065622127234f726927756d"
ans=int(str,16)
a=0
list=[]
i=0
while(i<len(str)):
   s=""
   if i<len(str):
       s=s+str[i]
   if(i+1<len(str)):
       s=s+str[i+1]
   list.append(s)
   i=i+2
print(list)
while (a<=127):
   ans=""
   for item in list:
       n=int(item,16)
       f=n^a
       ans=ans+chr(f)
   if ans[0:6]=="crypto":
       print(ans)
  
   a=a+1

```
i convertes the hex form into a list containing each two bytes which i xored with number 1 to 127 as its mentioned in the question its been xored by a single bit. printed only that string which had crypto as its first 6 letters.


the flag is **crypto{0x10_15_my_f4v0ur173_by7e}**

#### You either know, XOR you don't
i was given with a hex string which is final product of encoding flag with unknown key it can be single letter or a word or a sentence with no spaces
some part of it can be found using the known part of the flag
```
we know the flag is of the form crypto{*****}
first 7 letters are crypto{ its confirmed
```
we know xor is commutative and xoring with same number gives 0 we can use this as follows
```
flag ^ secretkey =givenstring
flag ^ secretkey ^flag =givenstring ^flag
secret key= govenstring ^flag
but we dont know the complete flag all i know first 7 letters by this we can find first 7 letters of secret key
```
i prepared the following script
```
str="0e0b213f26041e480b26217f27342e175d0e070a3c5b103e2526217f27342e175d0e077e263451150104"
ans =int(str,16)
a=0
list=[]
i=0
while(i<len(str)):
   s=""
   if i<len(str):
       s=s+str[i]
   if(i+1<len(str)):
       s=s+str[i+1]
   list.append(s)
   i=i+2
ans="crypto{"
li=""
i=0
for item in list:
   li=li+chr((int(item,16))^ord(ans[i]))
   i=i+1
   if i>=len(ans):
       i=0
print(li)
```
i got the output as
```
myXORke+y_Q
           HOMe$~seG8bGURNDFWg)a|TM!an
```
first 8 keys are exact part of secret key that means
myXORke is part of secret key

then i guessed the key might be **myXORkey**
it proved to be correct

```

key="myXORkey"
i=0
lo=""
for item in list:
   lo=lo+chr((int(item,16))^ord(key[i]))
   i=i+1
   if i>=len(key):
       i=0


print(lo)
```

### MATHEMATICS

this part took me good amount of time
this perticular [playlist](https://www.youtube.com/watch?v=M42uDLGRSpI&list=PLBlnK6fEyqRjjeHdm0cwu6E-nhhEluuVA&index=4)
helped me

#### Greatest Common Divisor
this challenge helps us to learn how GCD is found using euclid's algorithm

```
a = 66528
b = 52920
sum=a+b
a=min(a,b)
b=sum-a
diff=b%a
while(diff<a and diff>0):
  
   b=a
   a=diff
   diff=b%a


print(a)
```

#### Extended GCD
although i understood extended Euclid's algo stated there will be twon unique integers u and v such that p *u + q *v = GCD(p,q)

implementing it into code wasnt that easy for me i knew it can be achieved by recalling function but couldnt come up with correct code
so i took help if chat gpt and obtained this code

```
def extended_gcd(a, b):
   if a == 0:
       return b, 0, 1
   else:
       gcd, x1, y1 = extended_gcd(b % a, a)
       x = y1 - (b // a) * x1
       y = x1
       return gcd, x, y


# Example usage
a = 26513
b = 32321
gcd, x, y = extended_gcd(a, b)
print(f'GCD of {a} and {b} is {gcd}')
print(f'Coefficients x and y are {x} and {y}')
```
#### Modular Arithmetic 1
it helped me to understand the terminolgy of mod and congruency
```
Another way of saying this, is that when we divide the integer a by m, the remainder is b. This tells you that if m divides a (this can be written as m | a) then a ≡ 0 mod m.

```

```
print(11%6)
print(8146798528947%17)

```

#### Modular Arithmetic 2
this challenge introduces us to [Fermat's little  Theorem](https://www.geeksforgeeks.org/fermats-little-theorem/)
its nothing but
```
Here p is a prime number 
ap ≡ a (mod p).
```
```
ap-1 ≡ 1 (mod p) 
OR 
ap-1 % p = 1 
Here a is not divisible by p. 
```
and no calculator is needed for this problem anser is 1

#### Modular Inverting
this challenge introduces us to modular inverse if a number
```
For all elements g in the field, there exists a unique integer d such that g * d ≡ 1 mod p
```
for the existance of modular inverse both g and p must be coprime that is GCD(g,p)=1
```
g *d -p * y=gcd(g,p)=1
we have seen this somewhere isnt it
itsw extended euclid's algorithm
we know the hcf of g and p is 1 and all we care is a nnumber d such that g*d -p*y =1
when we take modulus on both sides by p
the term p*y is completely divisible by the p 
(g*d)%p = 1 which can be written as g*d = 1 mod p
```
using this concept the extended gcd code can be improved to find modular inverse.
```
def extended_gcd(a, b):
    if a == 0:
        return b, 0, 1
    gcd, x1, y1 = extended_gcd(b % a, a)
    x = y1 - (b // a) * x1
    y = x1
    return gcd, x, y

def modular_inverse(a, m):
    gcd, x, _ = extended_gcd(a, m)
    if gcd != 1:
        raise ValueError(f"No modular inverse exists for {a} modulo {m}")
    return x % m

# Example usage:
a = 3
m = 11
inverse = modular_inverse(a, m)
print(f"The modular inverse of {a} modulo {m} is {inverse}")

```

## SYMMETRIC CIPHERS
all the challenges in this section (that need to be solved)are informative 
### HOW AES WORKS
#### Keyed Permutations
mathematical term one-to one correspondance is bijective

#### Resisting Bruteforce
i just googled for answet but i completely read all the articles they have given
answer is Biclique attack

#### Structure of AES



## RSA
### STARTER
#### RSA Starter 1
this challenge helps us to learn about the pow() function in python

```

Find the solution to 10^117 mod 22663
pow(10,117,22663)

```
and the answer is **11570**

#### RSA Starter 2
rsa encryption is explained in this [page](https://www.splunk.com/en_us/blog/learn/rsa-algorithm-cryptography.html#:~:text=RSA%20is%20a%20popular%20and,the%20source%20of%20a%20message.)

here is its important part
```
Encryption. When encrypting a message, the sender uses the public key (n, e) of the recipient to compute the ciphertext, where the ciphertext = m^e mod n. The m indicates the plaintext message.
Decryption. When decrypting an RSA encrypted message, the recipient uses their private key (n, d) to compute the plaintext message, where the plaintext message = c^d mod n.
```
in this challenge 12 is the message and e p and q arre given and we know that N=p*q
now c is  m^e mod N
```
m=12
e=65537
p=17
q=23
N=p*q
print(pow(m,e,N))
```
and answer is **301**


#### RSA Starter 3
```
What is the totient of N?
```
we know totient of N is (p-1)*(q-1)
 
given 
```
p = 857504083339712752489993810777

q = 1029224947942998075080348647219
```

```
p = 857504083339712752489993810777

q = 1029224947942998075080348647219
print((p-1)*(q-1))
```
and answer is **882564595536224140639625987657529300394956519977044270821168**


#### RSA Starter 4
private key d is the modular multiplicative inverse of e modulo ϕ(n) where ϕ(n) is totient of N that is (p-1)*(q-1)
we are given with p,q,e we have to find d
```
Given the two primes:

p = 857504083339712752489993810777

q = 1029224947942998075080348647219

and the exponent:

e = 65537
```
we know e*d is congruent to 1 mod ϕ(n) where d is modular inverse then
we know gcd(e,ϕ(n))=1
e *d + ϕ(n) * y =1 (extended Euclear algo)
taking mod on both sides
e*d mod ϕ(n) =1
d =  e ^-1 mod ϕ(n)
thus d can be found by pow(e,-1,ϕ(n))

```
p = 857504083339712752489993810777
q = 1029224947942998075080348647219
e = 65537
print(pow(e,-1,(p-1)*(q-1)))
```
answer for this challenge is **121832886702415731577073962957377780195510499965398469843281**

#### RSA Starter 5

we know

```
Encryption. When encrypting a message, the sender uses the public key (n, e) of the recipient to compute the ciphertext, where the ciphertext = m^e mod n. The m indicates the plaintext message.
Decryption. When decrypting an RSA encrypted message, the recipient uses their private key (n, d) to compute the plaintext message, where the plaintext message = c^d mod n.
```
thus it can be decrypted by pow(c,d,N) and its given to use p and q from the last problem

```
p = 857504083339712752489993810777
q = 1029224947942998075080348647219
N = 882564595536224140639625987659416029426239230804614613279163
e = 65537
c = 77578995801157823671636298847186723593814843845525223303932
d = pow(e,-1,(p-1)*(q-1))
print(pow(c,d,N))
```
the answer is **13371337**

#### RSA Starter 6
```
import hashlib
from Crypto.Util.number import *

f = open("private.key", 'r')
data = f.readlines()
cnt = 0
for i in data:
    if cnt == 0:
        N = int(i[4:-1])
    else:
        d = int(i[4:-1])
    cnt += 1
print(N)
print(d)
m = b"crypto{Immut4ble_m3ssag1ng}"

hash_m = hashlib.sha256(m).digest()
print(hash_m)
sign_message = pow(bytes_to_long(hash_m), d, N)
print(sign_message)
```
the answer is **13480738404590090803339831649238454376183189744970683129909766078877706583282422686710545217275797376709672358894231550335007974983458408620258478729775647818876610072903021235573923300070103666940534047644900475773318682585772698155617451477448441198150710420818995347235921111812068656782998168064960965451719491072569057636701190429760047193261886092862024118487826452766513533860734724124228305158914225250488399673645732882077575252662461860972889771112594906884441454355959482925283992539925713424132009768721389828848907099772040836383856524605008942907083490383109757406940540866978237471686296661685839083475
**