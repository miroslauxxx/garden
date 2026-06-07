1. `File Descriptors` (FD) are non-negative integers `(0, 1, 2, ...)` that are associated with files that are opened. When we open an existing file or create a new one, the kernel returns a file descriptor to the calling code.

	To the kernel, all open files are referred to by file descriptors, including those entities that aren't files per entity such as anonymous pipes and network sockets. 
- anonymous pipe is `|`
- network socket could be created with `socket(3)`;

	When we want to read or write on a file, we identify the file with the file descriptor that was returned by functions such as `open()` or `create()`, and provided it to either `read()` or `write()`. 
	
	Initially each UNIX process has 20 file descriptors at its disposal, numbered 0 through 19 but it was extended to 63 by many systems. When the parent process forks a process, the child process inherits the file descriptors of the parent. 

	Because PID 1 is the ultimate ancestor of all user-space processes, it forms the root of the file descriptor lineage across the entire operating system

2. `0, 1, 2` are standard **FD**'s that corresponds to `STDIN_FILENO`, `STDOUT_FILENO` and `STDERR_FILENO` (defined in `unistd.h`) opened by default on behalf of shell when the program starts.

3. FD's are allocated in the sequential order, meaning the lowest possible unallocated integer value.

4. FD's for a particular process can be seen in `/proc/$pid/fd` (on Unix based systems).

f print f
file print formatted

