
Stegazip
using apriesolve we see binwalk and common password 
[+] Upload count: 26
[+] Common password(s): 5t3g4n0p1c, 5t3g4n0plc
![image](https://github.com/SoraAurora/Writeups_GCTF2023/assets/91508322/cb286a0e-e9e0-42e5-bd02-c1aaee3dddd5)

using binwalk on kali to download the files we get a flag folder with 1000 images 
then sorting using file size we see file img 666 with 14358
then opening requires password using  5t3g4n0plc above we open and see an image
now using string we extract a line (apriesolve)

GCTF23{$t3g4n0s4n1ty?}
