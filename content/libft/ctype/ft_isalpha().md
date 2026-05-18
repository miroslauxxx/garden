```
#include <ctype.h>
int ft_isalpha(int c);
```
DESCRIPTION:	
`Checks for an alphabetic character`

In the standard **"C"** locale, it is equivalent to ([[ft_isupper()]] || [[ft_islower()]]). In some locales, there may be additional characters for which [[ft_isalpha()]] is true — letters which are neither uppercase nor lowercase.

RETURN VALUE:
The values returned are nonzero if the character `c` falls into the tested class, and zero if not.

#classification #character #ctype #libft

```

``` 

```EDGE_CASES
just compare all standard ascii results with non-ft alternative func.
```
MAN: https://man.archlinux.org/man/core/man-pages/isalpha.3.en