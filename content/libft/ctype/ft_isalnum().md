```
#include <ctype.h>
int ft_isalnum(int c);
```
DESCRIPTION:	
	`Checks for an alphanumeric character, it is equivalent to (isalpha() || isdigit())`

RETURN VALUE:
	The values returned are nonzero if the character `c` falls into the tested class, and zero if not.

#classification #character #ctype #libft 

```NOTES 

``` 

```EDGE_CASES
just compare all standard ascii results with non-ft alternative func. 
```
MAN: https://man.archlinux.org/man/core/man-pages/isalnum.3.en