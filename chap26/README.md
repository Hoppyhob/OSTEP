Run `t0.c` a number of times to observe the behavior of the two threads.
The outputs from the two threads should appear in any interleaving pattern
possible.

```
gcc -o t0 t0.c -Wall -lpthread
./t0
```

Now lets make two threads work together to increment a shared counter:
```
gcc -m32 -g -o t1 t1.c -lpthread
./t1 10000
./t1 100000
```
Run the last command a fews time to let the problem surface. The heart of the
problem lies in the following three lines of compiler generated code:

<pre>
$ ./t1 100000
main: begin [counter = 0] [<mark>804a048</mark>]
A: begin [addr of i: 0xf7504348]
B: begin [addr of i: 0xf6d03348]
A: done
B: done
main: done
 [counter: 155917]
 [should: 200000]

$ objdump -d t1
...
8048808:       a1 48 a0 04 08          mov    0x<mark>804a048</mark>,%eax
804880d:       83 c0 01                add    $0x1,%eax
8048810:       a3 48 a0 04 08          mov    %eax,0x804a048
...
</pre>
