```
#include <strings.h>
void bzero(void *s, size_t n);
```
DESCRIPTION:
	`The bzero() function erases the data in the n bytes of the memory starting at the location pointed to by s, by writing zeros (bytes containing '\0') to that area. It's just memset with 0's`

RETURN VALUE:
	None.

#setting #zero #memory #strings #libft

```NOTES 
>Why we are able to ignore return value of memset ?
C-Lang allows to ignore any function's return value, bzero lets memset do the work and safely discards the pointer memset returns.
``` 

```EDGE_CASES
// normal
char buffer[5] = "Hello";
bzero(buffer, 5); //  buffer[5] = "00000"

// n == 0
bzero(buffer, 0); // buffer[5] = "Hello"

// offset value 
char array[10] = "123456789"; // array[10] = "123450009" 
bzero(array + 5, 3);

// uninitialized, just allocated memory
char *ptr = malloc(100); // *ptr = "0000000000...00" // [100] zero's
bzero(ptr, 100);
```
SRC: https://github.com/bminor/glibc/blob/master/string/bzero.c

MAN: https://man.archlinux.org/man/bzero.3