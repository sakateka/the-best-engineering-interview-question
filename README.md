# the-best-engineering-interview-question

## build && run

```bash
the-best-engineering-interview-question (main) λ cd memcached-1.4.15
memcached-1.4.15 (main) λ ./configure
...
memcached-1.4.15 (main) λ make -j8
...
memcached-1.4.15 (main) λ ./memcached
```

## timeline

```bash
the-best-engineering-interview-question (main) λ git log|grep -A2 Date

...

Date:   Tue Oct 17 22:19:31 2023 +0300

    feat: add python bmecached client with mult support
--
Date:   Tue Oct 17 22:18:39 2023 +0300

    fix: binary mult
--
Date:   Tue Oct 17 22:02:33 2023 +0300

    feat: python client with mult cmd
--
Date:   Tue Oct 17 22:02:09 2023 +0300

    fix: add mult stats
--
Date:   Tue Oct 17 21:53:13 2023 +0300

    feat: add new mult command
--
Date:   Tue Oct 17 20:29:21 2023 +0300

    first commit
```

## telnet

```bash
the-best-engineering-interview-question (main) λ telnet 127.0.0.1 11211
Trying 127.0.0.1...
Connected to 127.0.0.1.
Escape character is '^]'.
set age 0 3600 2
37
STORED
mult age 2
74
incr age 1
75
decr age 3
72
^]

```

## memcached python client

```python
the-best-engineering-interview-question (main) λ ipython

In [1]: import sys

In [2]: sys.path.append('.')

In [3]: import memcache

In [4]: mc = memcache.Client(['127.0.0.1:11211'])

In [5]: mc.set('age', 37, time=3600)
Out[5]: True

In [6]: mc.mult('age', 2)
Out[6]: 74

In [7]: mc.incr('age', 1)
Out[7]: 75

In [8]: mc.decr('age', 3)
Out[8]: 72
```

## binary memcache python client (bmemcached)

```python
the-best-engineering-interview-question (main) λ ipython

In [1]: import sys

In [2]: sys.path.append('.')

In [3]: import bmemcached

In [4]: mc = bmemcached.Client(('127.0.0.1:11211', ))

In [5]: mc.set('age', 37, time=3600)
Out[5]: True

In [6]: mc.mult('age', 2)
Out[6]: 74

In [7]: mc.incr('age', 1)
Out[7]: 75

In [8]: mc.decr('age', 3)
Out[8]: 72

In [9]: mc.mult('age', 100)
Out[9]: 7200
```
