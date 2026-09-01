Most file I/O on a UNIX system can be performed using only five functions: open, read, write, lseek, and close.

```
od -A x -t x1z -v main.c // print in hex format

```

`fd = open(pathname, flags, mode)` opens the file identified by `pathname`, returning a `file descriptor` used to refer to the open file in subsequent calls. If the file doesn’t exist, open() may create it, depending on the settings of the flags bit-mask argument. The `flags` argument also specifies whether the file is to be opened for reading, writing, or both. The `mode` argument specifies the permissions to be placed on the file if it is created by this call. If the open() call is not being used to create a file, this argument is ignored and can be 
omitted.
___
`numread = read(fd, buffer, count)` reads at most `count` bytes from the open file referred to by `fd` and stores them in `buffer`. The read() call returns the number of bytes actually read. If no further bytes could be read (i.e., end-of-file was encountered), read() returns 0.
___
`numwritten = write(fd, buffer, count)` writes up to `count` bytes from `buffer` to the open file referred to by `fd`. The write() call returns the number of bytes actually written, which may be less than count.
___
`status = close(fd)` is called after all I/O has been completed, in order to release the file descriptor fd and its associated kernel resources.
#### open
Permissions actually placed on a new file depend not just on the mode argument, but also on the process umask and the (optionally present) default access control list of the parent directory. 
```
#include <fcntl.h>
/* Open existing file for reading */
fd = open("startup", O_RDONLY);
if (fd == -1)
	errExit("open");
/* Open new or existing file for reading and writing, truncating to zero bytes; file permissions read+write for owner, nothing for all others */
fd = open("myfile", O_RDWR | O_CREAT | O_TRUNC, S_IRUSR | S_IWUSR);
if (fd == -1)
	errExit("open");
/* Open new or existing file for writing; writes should always append to end of file */
fd = open("w.log", O_WRONLY | O_CREAT | O_TRUNC | O_APPEND, S_IRUSR | S_IWUSR);
if (fd == -1)
	errExit("open")
```
___
```
Flag           <------>      Purpose

O_RDONLY                     Open for reading only 

O_WRONLY                     Open for writing only 

O_RDWR                       Open for reading and writing 

O_CLOEXEC                    Set the close-on-exec flag (since Linux 2.6.23)

O_CREAT                      Create file if it doesn’t already exist 

O_DIRECT                     File I/O bypasses buffer cache

O_DIRECTORY                  Fail if pathname is not a directory 

O_EXCL with O_CREAT:         Create file exclusively 

O_LARGEFILE                  Used on 32-bit systems to open large files

O_NOATIME                    Don’t update file last access time on read() (since Linux 2.6.8)

O_NOCTTY                     Don’t let pathname become the controlling terminal 

O_NOFOLLOW                   Don’t dereference symbolic links 

O_TRUNC                      Truncate existing file to zero length 

O_APPEND                     Writes are always appended to end of file 

O_ASYNC                      Generate a signal when I/O is possible

O_DSYNC                      Provide synchronized I/O data integrity (since Linux 2.6.33)

O_NONBLOCK                   Open in nonblocking mode 

O_SYNC                       Make file writes synchronous
``` 
___
Since kernel 2.6.22, the Linux-specific files in the directory /proc/PID/fdinfo can be read to obtain information about the file descriptors of any process on the system. There is one file in this directory for each of the process’s open file descriptors, with a name that matches the number of the descriptor. The pos field in this file shows the current file offset. The flags field is an octal number that shows the file access mode flags and open file status flags. (To decode this number, we need to look at the numeric values of these flags in the C library header files.)
#### read
read() doesn’t place a terminating null byte at the end of the string. A moment’s reflection leads us to realize that this must be so, since read() can be used to read any sequence of bytes from a file. In some cases, this input might be text, but in other cases, the input might be binary integers or C structures in binary form. There is no way for read() to tell the difference, and so it can’t attend to the C convention of null terminating character strings. If a terminating null byte is required at the end of the input buffer, we must put it there explicitly.

```
// copy input to output
#define BUFFSIZE 4096

int main(void)
{
	int n;
	char buf[BUFFSIZE];
	
	while ((n = read(STDIN_FILENO, buf, BUFFSIZE)) > 0)
	{
		if (write(STDOUT_FILENO, buf, n) != n)
			err_sys("write error");
	}
	if (n < 0)
		err_sys("read error");
	exit(0);
}
```
#### lseek
```
#include <unistd.h>

off_t lseek(int fd, off_t offset, int whence);
					returns new file offset if successful, or –1 on error
```
For each open file, the kernel records a file offset, sometimes also called the read-
write offset or pointer. This is the location in the file at which the next read() or write()
will commence. The file offset is expressed as an ordinal byte position relative to
the start of the file. The first byte of the file is at offset 0. The file offset is set to point to the start of the file when the file is opened and is automatically adjusted by each subsequent call to read() or write() so that it points to the next byte of the file after the byte(s) just read or written.
```
curr = lseek(fd, 0, SEEK_CUR);
lseek(fd, 0, SEEK_SET); /* Start of file */
lseek(fd, 0, SEEK_END); /* Next byte after the end of the file */
lseek(fd, -1, SEEK_END); /* Last byte of file */
lseek(fd, -10, SEEK_CUR); /* Ten bytes prior to current location */
lseek(fd, 10000, SEEK_END); /* 10001 bytes past last byte of file */
```

We can’t apply lseek() to all types of files. Applying lseek() to a pipe, FIFO,
socket, or terminal is not permitted; lseek() fails, with errno set to ESPIPE. On the
other hand, it is possible to apply lseek() to devices where it is sensible to do so. For
example, it is possible to seek to a specified location on a disk or tape device
`Unseekable file descriptors` are stream-type files (such as pipes and sockets) they do not use the offset because the data in the file is not randomly accessible. 
#### ioctl
The ioctl() system call is a general-purpose mechanism for performing file and
device operations that fall outside the universal I/O model.
```
int ioctl(int fd, int request, ... /* argp */);
		Value returned on success depends on request, or –1 on error
```
The `fd` argument is an open file descriptor for the device or file upon which the
control operation specified by `request` is to be performed. Device-specific header
files define constants that can be passed in the `request` argument.
#### pread / pwrite (perform location)
```
#include <unistd.h>
ssize_t pread(int fd, void *buf, size_t count, off_t offset);
		Returns number of bytes read, 0 on EOF, or –1 on error
ssize_t pwrite(int fd, const void *buf, size_t count, off_t offset);
		Returns number of bytes written, or –1 on error
```
These system calls can be particularly useful in multithreaded applications. As we’ll see in Chapter 29, all of the threads in a process share the same file descriptor table. This means that the file offset for each open file is global to all threads. Using pread() or pwrite(), multiple threads can simultaneously perform I/O on the same file descriptor without being affected by changes made to the file offset by other threads. If we attempted to use lseek() plus read() (or write()) instead, then we would create a race condition. If we are repeatedly performing lseek() calls followed by file I/O, then the pread() and pwrite() system calls can also offer a performance advantage in some cases. This is because the cost of a single pread() (or pwrite()) system call is less than the cost of two system calls: lseek() and read() (or write()). However, the cost of system calls is usually dwarfed by the time required to actually per-form I/O.

#### readv / writev
```
#include <sys/uio.h>

ssize_t readv(int fd, const struct iovec *iov, int iovcnt);
		Returns number of bytes read, 0 on EOF, or –1 on error
ssize_t writev(int fd, const struct iovec *iov, int iovcnt);
		Returns number of bytes written, or –1 on error
```
Instead of accepting a single buffer of data to be read or written, these functions transfer multiple buffers of data in a single system call. The set of buffers to be transferred is defined by the array iov. The integer count specifies the number of elements in iov. Each element of iov is a structure of the following form:
```
struct iovec {
	void *iov_base; /* Start address of buffer */
	size_t iov_len; /* Number of bytes to transfer to/from buffer */
};
```

```
#include <sys/stat.h>
#include <sys/uio.h>
#include <fcntl.h>
#include "tlpi_hdr.h"

int main(int argc, char *argv[])
{
	int     fd;
	struct  iovec iov[3];
	struct  stat myStruct; /* First buffer */
	int     x;             /* Second buffer */
	#define STR_SIZE 100
	char    str[STR_SIZE]; /* Third buffer */
	ssize_t numRead, totRequired;

	if (argc != 2 || strcmp(argv[1], "--help") == 0)
		usageErr("%s file\n", argv[0]);
	fd = open(argv[1], O_RDONLY);
	if (fd == -1)
		errExit("open");
		
	totRequired = 0;
	
	iov[0].iov_base = &myStruct;
	iov[0].iov_len = sizeof(struct stat);
	totRequired += iov[0].iov_len;
	
	iov[1].iov_base = &x;
	iov[1].iov_len = sizeof(x);
	totRequired += iov[1].iov_len;
	
	iov[2].iov_base = str;
	iov[2].iov_len = STR_SIZE;
	totRequired += iov[2].iov_len;
	
	numRead = readv(fd, iov, 3);
	if (numRead == -1)
		errExit("readv");
	
	if (numRead < totRequired)
		printf("Read fewer bytes than requested\n");
		printf("total bytes requested: %ld; bytes read: %ld\n", (long) totRequired, (long) numRead);
	
	exit(EXIT_SUCCESS);
}
```
#### preadv / pwritev

```
#define _BSD_SOURCE
#include <sys/uio.h>

ssize_t preadv(int fd, const struct iovec *iov, int iovcnt, off_t offset);
		Returns number of bytes read, 0 on EOF, or –1 on error
ssize_t pwritev(int fd, const struct iovec *iov, int iovcnt, off_t offset);
		Returns number of bytes written, or –1 on error
```
The preadv() and pwritev() system calls perform the same task as readv() and writev(), but perform the I/O at the file location specified by offset (like pread() and pwrite()).

####  truncate / ftruncate
```
#include <unistd.h>

int truncate(const char *pathname, off_t length);
int ftruncate(int fd, off_t length);
		Both return 0 on success, or –1 on error
```
The truncate() and ftruncate() system calls set the size of a file to the value specified by length. If the file is longer than length, the excess data is lost. If the file is currently shorter than length, it is extended by padding with a sequence of null bytes or a hole. The difference between the two system calls lies in how the file is specified. With truncate(), the file, which must be accessible and writable, is specified as a pathname string. If pathname is a symbolic link, it is dereferenced. The ftruncate() system call takes a descriptor for a file that has been opened for writing. It doesn’t change the file offset for the file.

#### Creating Temporary Files
```
#include <stdlib.h>

int mkstemp(char *template);
		Returns file descriptor on success, or –1 on error
```
The mkstemp() function generates a unique filename based on a template supplied by the caller and opens the file, returning a file descriptor that can be used with I/O system calls. The template argument takes the form of a pathname in which the last 6 characters
must be XXXXXX. These 6 characters are replaced with a string that makes the filename unique, and this modified string is returned via the template argument. Because template is modified, it must be specified as a character array, rather than as a string constant. The mkstemp() function creates the file with read and write permissions for the file owner (and no permissions for other users), and opens it with the O_EXCL flag, guaranteeing that the caller has exclusive access to the file.
```
int fd;
char template[] = "/tmp/somestringXXXXXX";
fd = mkstemp(template);
if (fd == -1)
	errExit("mkstemp");
printf("Generated filename was: %s\n", template);
unlink(template); /* Name disappears immediately, but the file is removed only after close() */
/* Use file I/O system calls - read(), write(), and so on */
if (close(fd) == -1)
	errExit("close");
```

```
#include <stdio.h>

FILE *tmpfile(void);
		Returns file pointer on success, or NULL on error
```
The tmpfile() function creates a uniquely named temporary file that is opened for reading and writing. (The file is opened with the O_EXCL flag to guard against the unlikely possibility that another process has already created a file with the same name.) On success, tmpfile() returns a file stream that can be used with the stdio library functions. The temporary file is automatically deleted when it is closed. To do this,
tmpfile() makes an internal call to unlink() to remove the filename immediately after opening the file.

#### ls program example
```
int	main(int argc, char **argv)
{
	DIR				*dp;
	struct dirent	*dirp;

	if (argc != 2)
		return(printf("usage: ls PATH"));

	if((dp = opendir(argv[1])) == NULL)
		return(printf("error occured while opening."));
	while((dirp = readdir(dp)) != NULL)
		printf("%s\n", dirp->d_name);
	
	closedir(dp);
	exit(0);
}
```
#### atomicity
Atomicity in C means an operation is indivisible and runs completely without interruption or exposure of intermediate states. All system calls are executed atomically. By this, we mean that the kernel guarantees that all of the steps in a system call are completed as a single operation, without being interrupted by another process or thread. It allows us to avoid race conditions. A race condition is a situation where the result produced by two processes (or threads) operating on shared resources depends in an unexpected way on the relative order in which the processes gain access to the CPU.
\*Indivisible means impossible to divide, separate, or break into smaller parts
#### race condition
Race condition is a concurrency bug that occurs when multiple threads or processes read and write to the same memory location at the same time without proper synchronization. This issue happens because the final state depends entirely on the unpredictable timing and order of CPU threads. High-level programming code (such as `x++`) is compiled into multiple hardware steps—typically read, modify, and write - which can be interrupted halfway through by another thread accessing the same location. This leads to sneaky bugs like data corruption and unpredictable behavior that are famously hard to reproduce and fix.
#### summary:
In order to perform I/O on a regular file, we must first obtain a file descriptor using open(). I/O is then performed using read() and write(). After performing all I/O, we should free the file descriptor and its associated resources using close(). These system calls can be used to perform I/O on all types of files. The fact that all file types and device drivers implement the same I/O interface allows for universality of I/O, meaning that a program can typically be used with any type of file without requiring code that is specific to the file type. For each open file, the kernel maintains a file offset, which determines the location at which the next read or write will occur. The file offset is implicitly updated by reads and writes. Using lseek(), we can explicitly reposition the file offset to any location within the file or past the end of the file. Writing data at a position beyond the previous end of the file creates a hole in the file. Reads from a file hole return bytes containing zeros. The ioctl() system call is a catchall for device and file operations that don’t fit into the standard file I/O model.
