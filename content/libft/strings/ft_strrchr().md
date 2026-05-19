```
#include <string.h>
char *strrchr(const char *s, int c);
```
DESCRIPTION:	
	`The strrchr() function returns a pointer to the last occurrence of the character c in the string s.`

RETURN VALUE:
	The strrchr() function return a pointer to the matched character or NULL if the character is not found. The terminating null byte is considered part of the string, so that if c is specified as '\0', this function will return a pointer to the terminator.

#string #scanning #character #libft 

```NOTES 
> cast `int c` to unsigned char
> iterate over string from end of string length until find occurance or reach index 0 of it. 
> return pointer to first occurance in string if character found, or NULL if not found or character to find is '\0'
``` 

```EDGE_CASES
> searching for null terminator
strrchr(s, 0) // will return end of string
> searching in string ""
strrchr(s, 55) // will return NULL
strrchr(s, \0) // will return pointer to end of string
> searching for overflow character (-1, 300)
strrchr(s, -1 / 300) // will cast int to ascii, then return
```
SRC: https://github.com/lattera/glibc/blob/master/string/strrchr.c

MAN:https://man.archlinux.org/man/strrchr.3