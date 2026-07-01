```c
#include <string.h>
void *memcpy(void *dest, const void *src, size_t n);
```
DESCRIPTION:
	`The memcpy() function copies n bytes from memory area src to memory area dest. The memory areas must not overlap. Use memmove() if the memory areas do overlap.`

RETURN VALUE:
	The memcpy() function returns a pointer to dest.

#memory #copy #string  #libft

```NOTES 
typecast src and dest to pointers to unsigned char, then read byte-by-byte at most `n` bytes of sp and assign to dp, return dst.   
overlap example: 
memcpy(p+1, p, 42); - undefined behaviour.
``` 

```EDGE_CASES
// copying src to dest when it's the same 
char buffer[10] = "0123456789";
memcpy(buffer, buffer, 10) // will return pointer to same string

// n == 0
memcpy(dest, src, 0) // will return dest

// Allocated, but contains random garbage
char *src = malloc(10);  
char dest[10];
memcpy(dest, src, 10); // will return pointer to string with garbage

// Shift data forward
char *src = &buffer[3];  // "3456789"
char *dest = &buffer[0]; // "0123..."
memcpy(dest, src, 5); // result will be "3456786789"
```
SRC: https://github.com/gcc-mirror/gcc/blob/master/libgcc/memcpy.c

MAN: https://man.archlinux.org/man/core/man-pages/memcpy.3.en