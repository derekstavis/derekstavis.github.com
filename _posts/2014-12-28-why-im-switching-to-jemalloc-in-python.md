---
layout: post
title: "Why I'm switching to jemalloc in Python"
category: posts
---

Following the release of Ruby 2.2.0, with built-in jemalloc support my curiosity in this memory allocator increased. 

In additition to Ruby for web development, last years I have been working with Python for Linux embedded software development, and never tried tweaking my systems performance by changing memory allocator.

Today I decided to benchmark Python with jemalloc allocator on a Raspberry Pi. I'm really concerned with Python performance on this little machines as the company where I work will be releasing a tech solution based on ARM and Python, and every tick I can squeeze out of processing power will be greatly appreciated.

## The benchmark

I will be basing the whole benchmark on a *very simple* code that I've found on the interwebs:

```
iterations = 2000000

l = []
for i in xrange(iterations):
    l.append(None)

for i in xrange(iterations):
    l[i] = {}

for i in xrange(iterations):
    l[i] = None

for i in xrange(iterations):
    l[i] = {}
```

The main purpose of this code is to profile memory trashing and allocation.

For profiler, I will be using the built-in `cProfile` module.

The first run was ran with glibc, but was discarded, because the first run usually needs to load Python libraries into memory, and this could interfere in results.


## The results


### glibc's malloc

```
$ python2 -m cProfile bench.py

	         2000002 function calls in 228.634 seconds

   Ordered by: standard name

   ncalls  tottime  percall  cumtime  percall filename:lineno(function)
        1  224.192  224.192  228.633  228.633 alloc.py:1(<module>)
  2000000    4.441    0.000    4.441    0.000 {method 'append' of 'list' objects}
        1    0.001    0.001    0.001    0.001 {method 'disable' of '_lsprof.Profiler' objects}
```

### jemalloc's malloc

```
$ LD_PRELOAD=jemalloc.so python2 python2 -m cProfile bench.py

         2000002 function calls in 162.033 seconds

   Ordered by: standard name

   ncalls  tottime  percall  cumtime  percall filename:lineno(function)
        1  157.873  157.873  162.032  162.032 alloc.py:1(<module>)
  2000000    4.159    0.000    4.159    0.000 {method 'append' of 'list' objects}
        1    0.001    0.001    0.001    0.001 {method 'disable' of '_lsprof.Profiler' objects}

```

## The obvious conclusion

The total run time got reduced by 66.601 seconds when using jemalloc.