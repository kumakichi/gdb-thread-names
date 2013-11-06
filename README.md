# About This Script

This script can be used within GDB to show thread names,got from backtrace in GDB.

**Attention that this script works only with POSIX standard thread library**

# Requirements

GNU awk, which is used to filter the output of command 'backtrace' in GDB.

# Installation

To install this script, add the following to `~/.gdbinit`:

```
source '/path/to/gdb-thread-names'
```

# Usage

while in GDB, just type

`show_thread_name`

It will print the threads entry point function names.

`help show_thread_name`

Show help infomation.

# Example

```
#include <pthread.h>
#include <stdio.h>

void *foo(void *arg)
{
	while (1)
		sleep(10);
}

void *bar(void *arg)
{
	while (1)
		sleep(10);
}

int main(int argc, char **argv)
{
	pthread_t t1, t2;
	pthread_create(&t1, NULL, foo, NULL);
	pthread_create(&t2, NULL, bar, NULL);
	while (1)
		sleep(10);
	return 0;
}
```

output:

```
(gdb) show_thread_name 
Thread-Id	Thread-Func
3 		 bar
2 		 foo
1 		 main
```
