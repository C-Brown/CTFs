ransomeware that takes flag.gif and "encrypts" it.


the "encrypt" is an xor character by character with a key that is as long as the file itself..


they provided an encrypted flag.gif file for us to decrypt.


the key is seeded with a timestamp. so we need the time that it was encrypted to be able to create the key to decrypt it.


they provided us with a pcap that sends an epoch timestamp over the socket it's communicating with.

timestamp: 1585599106


created a decrypter to use the seed value and xor the encrypted file with all the rand values and writes to flag.gif.


```
#include <stdio.h>
#include <stdlib.h>
int main () {
   int i, c;
   FILE *enc, *decrypt;
   int len;
   /* Intializes random number generator */
   srand(1585599106);
   enc = fopen("flag-gif.EnCiPhErEd", "rb");
   decrypt = fopen("flag-decrypt.gif", "wb");
   fseek(enc, 0, 2);
   len = ftell(enc);
   fseek(enc, 0, 0);
   while ((c = getc(enc)) != EOF) {
      putc(c ^ rand(), decrypt);
   }
   fclose(enc);
   fclose(decrypt);
   return(0);
}
```


output was a gif that has the flag written inside the ship's sail:


WPI{It_always_feels_a_little_weird_writing_malware}
