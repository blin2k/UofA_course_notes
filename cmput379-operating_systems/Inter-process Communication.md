Cooperating processes need to exchange information, as well as synchronize with each other, to perform their collective task.

`wait()` can be used to synchronize the cooperation, but they do not convey information between processes.

We need inter-process communication (IPC) methods.
- Shared memory (thread)
- files
- pipes
- signals
- shared memory (processes)
- message passing
- sockets

---
# File

Cumbersome and expensive

- Low level I/O (aka unbuffered I/O)
	- each read and write invokes a system call to the kernal
		- `open(), create(), close(), lseek(), read(), write()`
	- performance is sensitive to buffer size
- High level stream I/O (the Standard I/O library)
	- handles buffer allocation in optimized I/O chunks
	- `sefbuf(0, fflush(), fopen(), fclose(), getc(), gets()`

---
# Pipes

A reliable way to pass a stream of data from one process to a related process.

- tie the output of one process to the input of another
- information flows in ==one direction== (half duplex)
- flow controlled
	- never too full
- bi-direction pipes are also possible

---
# Signals

A rudimentary form of IPC, is used to notify a process of an event.

Generated when the event first occurs,
delivered when the process takes an action on that signal.

Pending when generated but not yet delivered.

Also called Software Interrupts, generally occur asynchronously.

can be sent by:
- one process to another
	- including itself
- kernel to a process

## What to do with a signal?

`kill(int pid, int sig)` allows you to send a signal

Using the `signal()` system call , a process can:
- ignore the signal
	- except `SIGKILL` and `SIGSTOP`
- catch the signal
	- tell the kernel to call a function whenever the signal occurs
- let the default action apply
	- T
		- terminate
		- perform all activities as if the exit system call is requested
	- TC
		- terminate and core dump
		- first produce a core image on disk and then perform the exit activities
	- S
		- stop
		- suspend the process
	- I
		- ignore
		- disregard the signal


`signal(int sig, SIGARG func)` redirects the signal to a new function instead of the default system call.

---
# Long Jumps

`setjmp(jmp_buf return_pt)` marks the line where it is,
`longjmp(jmp_buf return_pt, 1)` redirects the code to the marked line.