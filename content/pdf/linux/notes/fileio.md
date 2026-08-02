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
Since kernel 2.6.22, the Linux-specific files in the directory /proc/PID/fdinfo
can be read to obtain information about the file descriptors of any process on
the system. There is one file in this directory for each of the process’s open file
descriptors, with a name that matches the number of the descriptor. The pos
field in this file shows the current file offset. The flags field is an octal number that shows the file access mode flags and open file status flags. (To decode this number, we need to look at the numeric values of these flags in the C library header files.)

#### read
read() doesn’t place a terminating null byte at the end of the string. A moment’s reflection leads us to realize that this must be so, since read() can be used to read any sequence of bytes from a file. In some cases, this input might be text, but in other cases, the input might be binary integers or C structures in binary form. There is no way for read() to tell the difference, and so it can’t attend to the C convention of null terminating character strings. If a terminating null byte is required at the end of the input buffer, we must put it there explicitly.

#### lseek
```
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

#### summary:
In order to perform I/O on a regular file, we must first obtain a file descriptor using open(). I/O is then performed using read() and write(). After performing all I/O, we should free the file descriptor and its associated resources using close(). These system calls can be used to perform I/O on all types of files. The fact that all file types and device drivers implement the same I/O interface allows for universality of I/O, meaning that a program can typically be used with any type of file without requiring code that is specific to the file type. For each open file, the kernel maintains a file offset, which determines the location at which the next read or write will occur. The file offset is implicitly updated by reads and writes. Using lseek(), we can explicitly reposition the file offset to any location within the file or past the end of the file. Writing data at a position beyond the previous end of the file creates a hole in the file. Reads from a file hole return bytes containing zeros. The ioctl() system call is a catchall for device and file operations that don’t fit into the standard file I/O model.