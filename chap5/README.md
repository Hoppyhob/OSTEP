# Process API

```
$ ./p1
hello world (pid:13285)
hello, I am parent of 13286 (pid:13285)
hello, I am child (pid:13286)
```

```
$ ./p2
hello world (pid:13332)
hello, I am child (pid:13333)
hello, I am parent of 13333 (wc:13333) (pid:13332)
```