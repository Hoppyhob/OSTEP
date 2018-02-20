# VIRTUALIZATION
source: [chapter 1 of OSTEP](http://pages.cs.wisc.edu/~remzi/OSTEP/)

`cpu.c` shows the wonders of CPU virtualization.
```
gcc -o cpu cpu.c -Wall -Werror
```
Note that the [`-Wall`](https://www.thegeekstuff.com/2012/10/gcc-compiler-options/)
option enables all warning and the `-Werror` option converts warnings into errors.

We can run multiple instances of this program:
```
./cpu A & ./cpu B & ./cpu C & ./cpu D &
```

`mem.c (or mem-stack.c or ...) demonstrates memory virtualization.
```
gcc -o mem mem.c -Wall -Werror
./mem
./mem & ./mem &
```

To get it to work, must turn off address-space layout randomization
([ASLR](https://askubuntu.com/questions/318315/how-can-i-temporarily-disable-aslr-address-space-layout-randomization)).
Run the following command to disable ASLR in your current shell temporarily:
```
setarch `uname -m` -R /bin/bash
```

# CONCURRENCY

`threads.v0.c` shows a simple counter shared between two concurrent threads.
```
gcc -o threads.v0 threads.v0.c -Wall -pthread
./threads.v0 1000
Initial value : 0
Final value   : 1935
```
`threads.v1.c` doesn't seem to suffer from the problem in `threads.v0.c`.

```
gcc -o threads.v1 threads.v1.c -Wall -pthread
./threads.v1 100000
```

If you want to look at the disassembly use "objdump":
```
```
, locks
- if you want to look at the disassembly, use "otool" on macs
  or "objdump" on linux
  see "disasm-threads.csh" for the mac command
  on recent macs, had to compile very carefully to get an
  easy instruction sequence to examine
  (see make-threads.csh)
- add flag -pthread to compile

* PERSISTENCE
`io.c`
run 'dtrace -s trace-io.d' in another window
  ("trace-io.csh" can do this for you)
  this shows how complex the file system is ...

















