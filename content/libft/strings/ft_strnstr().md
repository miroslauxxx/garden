```c
#include <string.h>
char * strnstr(const char *big, const char *little, size_t len);
```
DESCRIPTION:	
	`The strnstr() function locates the first occurrence of the null-terminated string little in the string big, where not more than len characters are searched. Characters that appear after a ‘\0’ character are not searched`

RETURN VALUE:
	If little is an empty string, big is returned; if little occurs nowhere in big, NULL is returned; otherwise a pointer to the first character of the first occurrence of little is returned.

#string #scanning #bsd #libft

```NOTES 
// If little  empty string, return haystack
// Iterate haystack until \0 oy reach the length limit
// check is little matches at current position and (h + n) does not exceed or equal le
// return casted non-const index of haystack where first occurance found  
``` 

```EDGE_CASES
const char *big = "Foo Bas Baz";
const char *little = "Bar";
char *ptr;

> len == 0
ptr = strnstr(big, little, 0); // NULL
> little == ""
ptr = strnstr(big, little, 4); // return big
> little found in big
ptr = strnstr(big, little, 8); // return pointer to big[5]
> little nor found in big
const char *big = "Foo Bas Baz";
ptr = strnstr(big, little, 4); // return NULL
```
SRC: https://github.com/lattera/freebsd/blob/master/lib/libc/string/strnstr.c
https://github.com/reswitched/newlib/blob/master/newlib/libc/string/strnstr.c

MAN:https://man.archlinux.org/man/strnstr.3bsd