Audo Collapse
CDDC Writeup had same ctf question using same code changing the file name it works perfectly find , we are extracting the LSB of each byte
import wave
song = wave.open("problem.wav", mode='rb')
# Convert audio to byte array
frame_bytes = bytearray(list(song.readframes(song.getnframes())))

# Extract the LSB of each byte
extracted = [frame_bytes[i] & 1 for i in range(len(frame_bytes))]
# Convert byte array back to string
string = "".join(chr(int("".join(map(str,extracted[i:i+8])),2)) for i in range(0,len(extracted),8))
# Cut off at the filler characters
decoded = string.split("###")[0]

# Print the extracted text
print("Sucessfully decoded: "+decoded)
song.close()
# Use wave package (native to Python) for reading the received audio file
import wave
song = wave.open("problem.wav", mode='rb')
# Convert audio to byte array
frame_bytes = bytearray(list(song.readframes(song.getnframes())))

# Extract the LSB of each byte
extracted = [frame_bytes[i] & 1 for i in range(len(frame_bytes))]
# Convert byte array back to string
string = "".join(chr(int("".join(map(str,extracted[i:i+8])),2)) for i in range(0,len(extracted),8))
# Cut off at the filler characters
decoded = string.split("###")[0]

# Print the extracted text
print("Sucessfully decoded: "+decoded)
song.close()
#CDDC2023{tH15_15_AuD10_5t39aNo9rAphy}
![image](https://github.com/SoraAurora/Writeups_GCTF2023/assets/91508322/dedc55ac-6158-4f11-b1d0-219eafd4373f)

GCTF23{4udi0_c0ll4ps3}
