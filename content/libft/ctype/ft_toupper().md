```
#include <ctype.h>
int toupper(int c);
```
DESCRIPTION:	
	`If c is an lowercase letter, toupper() returns its uppercase equivalent, if a uppercase representation exists in the current locale`

RETURN VALUE:
	The value returned is that of the converted letter, or _c_ if the conversion was not possible.

#conversion  #character  #ctype #libft

```NOTES 

``` 

```EDGE_CASES
just compare all standard ascii alphabet lowercase results with non-ft alternative func.
```