```
#include <stdlib.h>
int atoi(const char *nptr);
```
DESCRIPTION:	
	`Converts the initial portion of the string pointed to by nptr to int`

RETURN VALUE:
	The converted value or 0 on error.

#conversion #character #stdlib #libft 

```NOTES 
// Skip all standard whitespace characters
// Handle a single optional '+' or '-' sign
// Process digits and stop immediately at any non-numeric character
``` 

```EDGE_CASES
// normal 
ft_atoi("42") 
ft_atoi("-42") 

// spaces and signs 
ft_atoi(" +42") // return 42 
ft_atoi(" --42") // Multiple signs, return 0
ft_atoi("+-42") // Conflicting back-to-back signs, returns 0

// non-numeric characters 
ft_atoi("42a73") // return 42
ft_atoi("a42") // return 0
```
SRC: https://github.com/lattera/glibc/blob/master/stdlib/atoi.c

MAN: https://man.archlinux.org/man/core/man-pages/atoi.3.en