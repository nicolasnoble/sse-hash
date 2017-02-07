## What ?

SSE hashing of parallel streams. Right now, only MD5 is supported with 4
parallel streams using SSE2. Maybe I'll add more hash functions in the
future if I feel like it.

## How ?

You should be able to compile this code using any modern compiler that supports
SSE intrinsics. You'll require SSE2 however. For example, using gcc:

```
$ gcc -O2 -fno-strict-aliasing -msse2 -DPMD5_TEST -o test-pmd5 md5-sse.c
```

The code will make use of pointer aliasing by default (as the example
command-line suggests). You can disable that behavior for a (slightly slower
but safer) version by defining `NO_PTR_ALIASING`.

For the API of the MD5 version, check the file [md5-sse2.h](md5-sse2.h).
You can have up to 4 streams being hashed in parallel.

Note that the code is about 2 times as slow as the normal C version
(which is provided). So hashing less than two streams in parallel is useless.
Be smart and flip between the SSE and the C version depending on how many
streams you are processing.

## Why ?

Booze may have been involved. I found that code on my harddrive, and I have
some memories of me writing it. If I get drunk again at some point in the
future, I might add a SHA1 version.

Also, this code should only be useful if you're using MD5 for checking a
lot of files, and you are able to saturate your CPU bandwidth with your
network and/or disk operations, which sounds unlikely. Then again, I might
be proven wrong. Let me know if this is useful to you.

## Who ?

This code is officially released into public domain, or if not applicable in
your contry or for your case, it is then covered under the terms of the
[MIT license](http://www.opensource.org/licenses/MIT), copyrighted by
myself, Nicolas Noble, in 2017.
