# node-setrlimit

Fork from [ohmu/node-posix](https://github.com/ohmu/node-posix) to just expose setrlimit

### getrlimit(resource)

Get resource limits. (See getrlimit(2).)

The `soft` limit is the value that the kernel enforces for the
corresponding resource. The `hard` limit acts as a ceiling for the soft
limit: an unprivileged process may only set its soft limit to a value in the
range from 0 up to the hard limit, and (irreversibly) lower its hard limit.

A limit value of `null` indicates "unlimited" (RLIM_INFINITY).

Supported resources:

`'core'` (RLIMIT_CORE) Maximum size of core file. When 0 no core dump files
are created.

`'cpu'` (RLIMIT_CPU) CPU time limit in seconds. When the process reaches the
soft limit, it is sent a SIGXCPU signal. The default action for this signal is
to terminate the process.

`'data'` (RLIMIT_DATA) The maximum size of the process's data segment
(initialized data, uninitialized data, and heap).

`'fsize'` (RLIMIT_FSIZE) The maximum size of files that the process may create.
Attempts to extend a file beyond this limit result in delivery of a SIGXFSZ
signal.

`'nofile'` (RLIMIT_NOFILE) Specifies a value one greater than the maximum file
descriptor number that can be opened by this process.

`'nproc'` (RLIMIT*NPROC) The maximum number of processes (or, more precisely on Linux,
threads) that can be created by this process. *(Note: Only Linux, OS X, and BSDs support the 'nproc' resource limit. An error will be raised on unsupported platforms.)\_

`'stack'` (RLIMIT_STACK) The maximum size of the process stack, in bytes. Upon
reaching this limit, a SIGSEGV signal is generated.

`'as'` (RLIMIT_AS) The maximum size of the process's virtual memory (address
space) in bytes.

    var limits = getrlimit('nofile');
    console.log('Current limits: soft=' + limits.soft + ', max=' + limits.hard);

### setrlimit(resource, limits)

Set resource limits. (See setrlimit(2).) Supported resource types are listed
under `getrlimit`.

The `limits` argument is an object in the form
`{ soft: SOFT_LIMIT, hard: HARD_LIMIT }`. Current limit values are used if
either `soft` or `hard` key is not specifing in the `limits` object. A limit
value of `null` indicates "unlimited" (RLIM_INFINITY).

    // raise maximum number of open file descriptors to 10k, hard limit is left unchanged
    setrlimit('nofile', { soft: 10000 });

    // enable core dumps of unlimited size
    setrlimit('core', { soft: null, hard: null });

## LICENSE

Copyright (c) 2011-2015 Mika Eloranta

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
