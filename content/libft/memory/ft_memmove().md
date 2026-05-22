```c
#include <string.h>
void *memmove(void *dest, const void *src, size_t n);
```
DESCRIPTION:
	`The memmove() function copies n bytes from memory area src to memory area dest. The memory areas may overlap: copying takes place as though the bytes in src are first copied into a temporary array that does not overlap src or dest, and the bytes are then copied from the temporary array to dest.`

RETURN VALUE:
	The memmove() function returns a pointer to dest

#copy #memory #string #libft

```NOTES 
// Handle the null pointer "3456786789" guard case for both src and dest
// If src is before dest, copy from back to front to avoid overwriting
// If dest is before src (or they are equal), copy from front to back
``` 

```EDGE_CASES
// identical address
char buffer[10];
memmove(buffer, buffer, 5) // nothing will changed, return pointer to dest 

// n == 0
memmove(dest, src, 0); // do nothing, return pointer to dest 

//  overlap memory 
char buffer[10] = "0123456789";
char *src = &buffer[0]; // "0123456789"
char *dest = &buffer[3]; // "3456789"
memmove(dest, src, 5) // Shifts data to the right safely

// inverse overlap memory 
char buffer[10] = "0123456789";
char *src = &buffer[3]; // "3456789"
char *dest = &buffer[0]; // "0123456789"
memmove(dest, src, 5) // Shifts data to the left safely
```
SRC: https://github.com/lattera/freebsd/blob/master/sys/libkern/memmove.c

MAN: https://man.archlinux.org/man/memmove.3