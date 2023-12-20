```
# -- Original Coded --
# from secrets import token_bytes
# from hashlib import md5
# from Crypto.Util.strxor import strxor
# secret = token_bytes(56)
# flag = open('original_flag.png','rb').read()
# length = len(flag)
# blocks = length // 16 + 1
# keys = b''
# for _ in range(blocks):
#     secret = md5(secret).digest()
#     keys += secret 
# open('flag.png','wb').write(strxor(keys[:length],flag))

# -- Solve Script --
from secrets import token_bytes
from hashlib import md5
from Cryptodome.Util.strxor import strxor
# cyberchef png header to hex first 16 btyes then xor downloaded png using png header then acquire the key from 16btyes 
secret='7fe7a51cd536c32d5c0664c8f76988ee'

secret=bytes.fromhex(secret)

flag = open('flag.png','rb').read()

length = len(flag)
#find blocks
blocks = length // 16 
print(blocks)
keys = secret
#hashing it over 688 times
for _ in range(blocks):
    secret = md5(secret).digest()
    keys += secret 
#creating decrypted
open('flag_decrypt.png','wb').write(strxor(keys[:length],flag))
```
![image](https://github.com/SoraAurora/Writeups_GCTF2023/assets/91508322/bc10e58a-f502-4525-ac47-4ca44cc46a4b)

Step 1. Acquire PNG Header Hex
Png Header in Hex
89 50 4e 47 0d 0a 1a 0a 00 00 00 0d 49 48 44 52
Step 2. XOR downloaded with png Header and acquire first 16 btyes (7fe7a51cd536c32d5c0664c8f76988ee) that will be secret
Step 3. create solve script that takes the flag.png then find the blocks by dividng the length by 16 getting 688 then hash it over 688 times
then outputing it as xor the key followed by flag.png cause xorxor original doing so gets decrtpy_flag which holds the flag
GCTF23{x0R_kN0wN_pLa1n_tX7_at7AcK}
