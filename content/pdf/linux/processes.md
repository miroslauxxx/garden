Three primary functions for process control: fork(), exec(), and waitpid().

A **process** is an instance of an executing program. Also may be defined as an abstract entity defined by the kernel, to which system resources are allocated in order to execute a program. 
A **program** is a file containing a range of information that describes how to con-
struct a process at run time

```
#include <sys/wait.h>
int main(void)
{
	char buf[MAXLINE]; /* from apue.h */
	pid_t pid;
	int status;
	
	printf("%% "); /* print prompt (printf requires %% to print %) */
	while (fgets(buf, MAXLINE, stdin) != NULL) 
	{
	if (buf[strlen(buf) - 1] == ’\n’)
		buf[strlen(buf) - 1] = 0; /* replace newline with null */
	if ((pid = fork()) < 0)
	{
		err_sys("fork error");
	} 
	else if (pid == 0) 
	{ /* child */
		execlp(buf, buf, (char *)0);
		err_ret("couldn’t execute: %s", buf);
		exit(127);
	}
	
	/* parent */
	if ((pid = waitpid(pid, &status, 0)) < 0)
		err_sys("waitpid error");
	printf("%% ");
	}
	exit(0);
}
```

each program includes:
- Binary format identification which gives kernel ability to interpret the remaining information in the file. Historically, two widely used formats for UNIX executable files were the original a.out (“assembler output”) format and the later, more sophisticated COFF (Common Object File Format). Nowadays, most UNIX implementations (including Linux) employ the Executable and Linking Format (ELF), which provides a number of advantages over the older formats.
- Machine-language instructions: These encode the algorithm of the program.
- Program entry-point address: This identifies the location of the instruction at which execution of the program should commence.
- Data: The program file contains values used to initialize variables and also literal constants used by the program (e.g., strings).
- Symbol and relocation tables: These describe the locations and names of functions and variables within the program. These tables are used for a variety of purposes, including debugging and run-time symbol resolution (dynamic linking).
- Shared-library and dynamic-linking information: The program file includes fields listing the shared libraries that the program needs to use at run time and the pathname of the dynamic linker that should be used to load these libraries.

One program may be used to construct many processes, or, put conversely, many
processes may be running the same program

```
#include <unistd.h>
pid_t getpid(void);
		Always successfully returns process ID of caller
pid_t getppid(void);
		Always successfully returns process ID of parent of caller
```
With the exception of a few system processes such as init (process ID 1), there is no fixed relationship between a program and the process ID of the process that is created to run that program.

#### Memory Layout of Segments inside a Process

- The text segment contains the machine-language instructions of the program run by the process. The text segment is made read-only so that a process doesn’t accidentally modify its own instructions via a bad pointer value. Since many processes may be running the same program, the text segment is made sharable so that a single copy of the program code can be mapped into the virtual address space of all of the processes.
- The initialized data segment (a.k.a. user-initialized data segment) contains global and static variables that are explicitly initialized. The values of these variables are read from the executable file when the program is loaded into memory.
- The uninitialized data segment (a.k.a. zero-initialized data segment) contains global and static variables that are not explicitly initialized. Before starting the program, the system initializes all memory in this segment to 0. For historical reasons, this is often called the bss segment, a name derived from an old assembler mnemonic for “block started by symbol.” The main reason for placing global and static variables that are initialized into a separate segment from those that are uninitialized is that, when a program is stored on disk, it is not necessary to allocate space for the uninitialized data. Instead, the executable merely needs to record the location and size required for the uninitialized data segment, and this space is allocated by the program loader at run time.
- The stack is a dynamically growing and shrinking segment containing stack frames. One stack frame is allocated for each currently called function. A frame stores the function’s local variables (so-called automatic variables), arguments, and return value.
- The heap is an area from which memory (for variables) can be dynamically allocated at run time. The top end of the heap is called the program break.

```
#include <stdio.h>
#include <stdlib.h>

char globBuf[65536];            /* Uninitialized data segment */
int primes[] = { 2, 3, 5, 7 };  /* Initialized data segment */
static int square(int x)        /* Allocated in frame for square() */
{
	int result;                 /* Allocated in frame for square() */
	result = x * x;
	return result;              /* Return value passed via register */
}
static void doCalc(int val)     /* Allocated in frame for doCalc() */
{
	printf("The square of %d is %d\n", val, square(val));
	if (val < 1000) {
	int t;                      /* Allocated in frame for doCalc() */
	t = val * val * val;
	printf("The cube of %d is %d\n", val, t);
	}
}

int main(int argc, char *argv[])/* Allocated in frame for main() */
{
	static int  key = 9973;     /* Initialized data segment */
	static char mbuf[10240000]; /* Uninitialized data segment */
	char        *p;             /* Allocated in frame for main() */
	p = malloc(1024);           /* Points to memory in heap segment */
	doCalc(key);
	exit(EXIT_SUCCESS);
}
```

#### Threads and Thread IDs
Usually, a process has only one thread of control — one set of machine instructions executing at a time. Some problems are easier to solve when more than one thread of control can operate on different parts of the problem. Additionally, multiple threads of control can exploit the parallelism possible on multiprocessor systems. All threads within a process share the same address space, file descriptors, stacks, and process-related attributes. Each thread executes on its own stack, although any thread can access the stacks of other threads in the same process. Because they can access the same memory, the threads need to synchronize access to shared data among themselves to avoid inconsistencies. Like processes, threads are identified by IDs. Thread IDs, however, are local to a process. A thread ID from one process has no meaning in another process. We use
thread IDs to refer to specific threads as we manipulate the threads within a process. Functions to control threads parallel those used to control processes. Because threads were added to the UNIX System long after the process model was established, however, the thread model and the process model have some complicated interactions. 

```
// includes array of char pointers of all environment variables

extern char **environ;
```

good to know about environment: 
```
### avoid using putenv(), use setenv() it works with memory under the hood

### do not modify variables, clear one and create new
// int unsetenv(const char *name);
// int setenv(const char *name, const char *value, int overwrite);

### Environment variables passed from the parent stored in memory segment located above the stack. Added via setenv() are stored on the heap, via putenv() - on the heap or global data.
```