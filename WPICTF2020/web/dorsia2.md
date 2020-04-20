We are given the dorsia video and directed towards the 2nd card in the video, which has new code. The description also tells us that:
flag is in ~/flag.txt and the code is run in /home/ctf/web/

```
void main() {
char a[69]={0};
scanf("GET /%s", &a);
printf("HTTP 200\r\n\r\n");
fflush(stdout); 
execlp("cat",a,a,0);}
```

Visiting the page with a browser, it seem that it is just text being sent back with no headers or anything.. Decided to just connect with netcat and see what all I can do with it.

With the description hint, connect with netcat and send GET /../flag.txt:

```
GET /../flag.txt


WPI{1_H4VE_2_return_SOME_VIDE0TAP3S}
```
