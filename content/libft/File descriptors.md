My personal interpretation of  `*_fd` functions presence in the very end of second part of libft - neccesity to test them. It's takes time to write (lol, it's Piscine :) ), but the most interesting - to test them. Here we got freedom, freedom of style and allowed functions. I gonna use [read()](https://man.archlinux.org/man/core/man-pages/close.2.en), [open()](https://man.archlinux.org/man/core/man-pages/open.2.en), [close()](https://man.archlinux.org/man/core/man-pages/close.2.en), [unlink()](https://man.archlinux.org/man/core/man-pages/unlink.2.en), [pipe()](https://man.archlinux.org/man/core/man-pages/pipe.2.en) and [fork()](https://man.archlinux.org/man/fork.2) (list may be not concrete). That's nice point to start exploring get_next_line.
,,, 

- `File Descriptors` (FD) are non-negative integers `(from 0 to 1024)` that are associated with files that are opened. When we open an existing file or create a new one, the parent process forks a process, the child process inherits the file descriptors of the parent and kernel returns a file descriptor to the calling code. 

	To the kernel, all open files are referred to by file descriptors, including those entities that aren't files per entity such as anonymous pipes and network sockets. 
	- anonymous pipe is `|`
	- network socket could be created with `socket(3)`;

	When we want to read or write on a file, we identify the file with the file descriptor that was returned by functions such as `open()` or `create()`, and provided it to either `read()` or `write()`. 

	Because PID 1 is the ultimate ancestor of all user-space processes, it forms the root of the file descriptor lineage across the entire operating system

	defined in `<unistd.h>`
	`0: STDIN_FILENO` .. 
	`1: STDOUT_FILENO`..
	`2: STDERR_FILENO`.. :: 
	standard **FD**'s that corresponds to `STDIN_FILENO`, `STDOUT_FILENO` and `STDERR_FILENO`  opened by default on behalf of shell when the program starts.

	FD's are allocated in the sequential order, meaning the lowest possible unallocated integer value.

	FD's for a particular process can be seen in `/proc/[pid]/fd` (on Unix based systems).

