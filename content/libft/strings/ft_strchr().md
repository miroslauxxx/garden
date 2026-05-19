```
#include <string.h>
char *strchr(const char *s, int c);
```
DESCRIPTION:	
	`The strchr() function returns a pointer to the first occurrence of the character c in the string s.`

RETURN VALUE:
	The strchr() return a pointer to the matched character or NULL if the character is not found. The terminating null byte is considered part of the string, so that if c is specified as '\0', it will return a pointer to the terminator.

#string #scanning #character #libft

```NOTES 
> cast `int c` to unsigned char
> injustice loop with 2 conditions:
> first match with `int c` second match with '\0'
``` 

```EDGE_CASES
> searching for null terminator
strchr(s, 0) // will return end of string
> searching in string ""
strchr(s, 55) // will return NULL
strchr(s, \0) // will return pointer to end of string
> searching for overflow character (-1, 300)
strchr(s, -1 / 300) // will cast int to ascii, then return
```
SRC: https://github.com/gcc-mirror/gcc/blob/master/libiberty/strchr.c

MAN: https://man.archlinux.org/man/strchr.3