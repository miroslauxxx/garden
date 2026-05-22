```c
#include <string.h>
void *memchr(const void *s, int c, size_t n);
```
DESCRIPTION:
	`The memchr() scans n bytes of the memory area pointed to by s for the first instance of c. Both c and the bytes of the memory area pointed to by s are interpreted as unsigned char.`

RETURN VALUE:
	Return a pointer to the matching byte or NULL if the character does not occur in the given memory area.

#memory #scanning #string #libft

```NOTES 
// Typecast staff
// Scan forward up to n bytes
// If a match is found, return a pointer to that specific byte
// Return NULL if n bytes are scanned without a match
``` 

```EDGE_CASES
char *s = GROWER;
// n == 0
memchr(s, 69, 0); // will return NULL

// c == '\0'
memchr(s, '\0', 10); // will return its memory address if it falls within the n limit

// Values outside the 0-255 for `int c` 
memchr(s, 256, 10); // range are truncated, so in result 256 will be converted to 1 and `c` will be searched as ASCII 1 value.   

// Target found beyond n bound 
memchr(s, 69, 3); // will return NULL 
```
SRC: https://github.com/libressl/openbsd/blob/master/src/lib/libc/string/memchr.c

MAN: https://man.archlinux.org/man/memchr.3