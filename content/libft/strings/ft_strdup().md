```c
#include <string.h>
char *strdup(const char *s);
```
DESCRIPTION:	
	`The strdup() function returns a pointer to a new string which is a duplicate of the string s. Memory for the new string is obtained with malloc(3), and can be freed with free(3).`

RETURN VALUE:
	On success, the strdup() function returns a pointer to the duplicated string. It returns NULL if insufficient memory was available, with errno set to indicate the error.

#string #copy #malloc #libft
#ft_strlen

```NOTES 

``` 

```EDGE_CASES
// normal
ft_strdup("Hello")

// empty string
ft_strdup("")
```
SRC: https://github.com/lattera/glibc/blob/master/string/strdup.c

MAN: https://man.archlinux.org/man/strdup.3