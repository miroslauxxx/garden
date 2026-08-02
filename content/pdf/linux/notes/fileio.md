`fd = open(pathname, flags, mode)` opens the file identified by pathname, returning a file descriptor used to refer to the open file in subsequent calls. If the file doesn’t exist, open() may create it, depending on the settings of the flags bit-mask argument. The flags argument also specifies whether the file is to be opened for reading, writing, or both. The mode argument specifies the permissions to be placed on the file if it is created by this call. If the open() call is not
being used to create a file, this argument is ignored and can be 
omitted.
___
`numread = read(fd, buffer, count)` reads at most count bytes from the open file referred to by fd and stores them in buffer. The read() call returns the number of bytes actually read. If no further bytes could be read (i.e., end-of-file was encountered), read() returns 0.
___
`numwritten = write(fd, buffer, count)` writes up to count bytes from buffer to the open file referred to by fd. The write() call returns the number of bytes actually written, which may be less than count.
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

Flag                                  Purpose
___
O_RDONLY                      Open for reading only 
O_WRONLY                     Open for writing only 
O_RDWR                          Open for reading and writing 
O_CLOEXEC                     Set the close-on-exec flag (since Linux 2.6.23)
O_CREAT                          Create file if it doesn’t already exist 
O_DIRECT                        File I/O bypasses buffer cache
O_DIRECTORY                 Fail if pathname is not a directory 
O_EXCL with O_CREAT:  Create file exclusively 
O_LARGEFILE                  Used on 32-bit systems to open large files
O_NOATIME                    Don’t update file last access time on read() (since Linux 2.6.8)
O_NOCTTY                      Don’t let pathname become the controlling terminal 
O_NOFOLLOW                Don’t dereference symbolic links 
O_TRUNC                         Truncate existing file to zero length 
O_APPEND                      Writes are always appended to end of file 
O_ASYNC                         Generate a signal when I/O is possible
O_DSYNC                         Provide synchronized I/O data integrity (since Linux 2.6.33)
O_NONBLOCK                Open in nonblocking mode 
O_SYNC                           Make file writes synchronous 
___