```
#include <string.h>
int strncmp(const char *s1, const char *s2, size_t n);
```
DESCRIPTION:	
	`The strncmp() function compares only the first (at most) n bytes of s1 and s2`

RETURN VALUE:
	The strncmp() function return an integer less than, equal to, or greater than zero if s1 (or the first n bytes thereof) is found, respectively, to be less than, to match, or be greater than s2.

#string #compare #libft

```NOTES 

``` 

```EDGE_CASES
> n == 0
strncmp(s1, s2, 0);
> passing one or two empty lines ("")

>
```
SRC: https://github.com/openbsd/src/blob/master/sys/lib/libkern/strncmp.c

MAN:https://man.archlinux.org/man/strncmp.3