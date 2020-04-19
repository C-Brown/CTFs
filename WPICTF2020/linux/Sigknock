Description:

Port knocking is boring. Enhance your security through obscurity using sigknock.

My solution was to do this manually even though there were probably MUCH easier ways to get it done.. 

It turns out that instead of knocking on ports to get something opened, this just wants interrupt signals in a specific order.. 

so i called the various interrupts until it told me i got to the next step, repeat until i got to the end.  

The proper order was, [2, 3, 11, 13, 17]

```
~ $ ps ax
PID   USER     TIME  COMMAND
    1 wpictf    0:00 {init_d} /bin/sh /bin/init_d
    8 wpictf    0:00 /bin/sh
   41 wpictf    0:00 irqknock
   50 wpictf    0:00 sh
   51 wpictf    0:00 /bin/sh
   52 wpictf    0:00 ps ax
~ $ kill -2 41
Got signal 2
State advanced to 1
~ $ kill -3 41
Got signal 3
State advanced to 2
~ $ kill -11 41
Got signal 11
State advanced to 3
~ $ kill -13 41
Got signal 13
~ $ State advanced to 4
kill -17 41
Got signal 17
State advanced to 5
WPI{1RQM@St3R}
```
