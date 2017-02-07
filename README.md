## What ?

SSE2 hashing of parallel streams. Right now, only MD5 is supported with 4
parallel streams, maybe I'll add more hash functions in the future if I
feel like it.

## How ?

You should be able to compile this code using any modern compiler that supports
SSE intrinsics. You'll require SSE2 however. For example, using gcc:

```
$ gcc -O2 -msse2 -DPMD5_TEST -o test-pmd5 md5-sse.c
```

For the API of the MD5 version, check the file [md5-sse2.h](md5-sse2.h).
You can have up to 4 streams being hashed in parallel.

Note that the code is about 2 times as slow as the normal C version
(which is provided). So hashing less than two streams in parallel is useless.
Be smart and flip between the SSE and the C version depending on how many
streams you are processing.

## Why ?

Booze may have been involved. I found that code on my harddrive, and I have
some memories of me writing it.
