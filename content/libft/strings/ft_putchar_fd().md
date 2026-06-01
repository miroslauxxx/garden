```c
#include <stdio.h>
void ft_putchar_fd(char c, int fd);
```
DESCRIPTION:	
`Outputs the character ’c’ to the specified file descriptor using write(2)`

RETURN VALUE:
`None`

#character #fd #print #libft

```NOTES 
wikipedia : File descriptors typically have non-negative integer values, with negative values being reserved to indicate "no value" or error conditions.
``` 

```EDGE_CASES

```
SRC: https://github.com/lattera/glibc/blob/master/libio/putchar.c

MAN:https://man.archlinux.org/man/putchar.3