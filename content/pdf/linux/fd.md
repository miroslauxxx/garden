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

	It is possible and useful to have multiple descriptors referring to the same open file. These file descriptors may be open in the same process or in different processes. 

	To understand what is going on, we need to examine three data structures maintained by the kernel:
	-  The per-process file descriptor table.
	-  The system-wide table of open file descriptions. 
	-  The file system i-node table.

	For each process, the kernel maintains a table of open file descriptors. Each entry in this table records information about a single file descriptor, including:
	-  Set of flags controlling the operation of the file descriptor 
	-  Reference to the open file description.

	The kernel maintains a system-wide table of all open file descriptions. (This table is sometimes referred to as the open file table, and its entries are sometimes called open file handles.) An open file description stores all information relating to an open file, including:
	- the current file offset (as updated by read() and write(), or explicitly modified using lseek());
	- status flags specified when opening the file (i.e., the flags argument to open());
	- the file access mode (read-only, write-only, or read-write, as specified in open());
	- settings relating to signal-driven I/O 
	- reference to the i-node object for this file.

	Each file system has a table of i-nodes for all files residing in the file system:
	- file type (e.g., regular file, socket, or FIFO) and permissions;
	- pointer to a list of locks held on this file;
	- various properties of the file, including its size and timestamps relating to different types of file operations.

	descriptor is integer applied for opened file, descriptor is content that can be read or 