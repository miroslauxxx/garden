```c
#include <stdlib.h>
int atoi(const char *nptr);
```
DESCRIPTION:	
	`Converts the initial portion of the string pointed to by nptr to int`

RETURN VALUE:
	The converted value or 0 on error.

#conversion #string #integer #stdlib #libft 
#ft_isdigit

```NOTES 
>Skip all standard whitespace characters
>Handle a single optional '+' or '-' sign
>Process digits and stop immediately at any non-numeric character
>res = res * 10 + (*nptr - '0');

- atoi() : receives string as argument and converts it to integer. Based on manual - it the same as strtol(nptr, NULL, 10);, which basically did the same operation. So generaly this guy works with numbers bigger then LONG_MAX, and until you'll discover docs in detail OR beeing evaluated by experienced and strict student with excellent C knowledge - you'll not be able to handle this edge case. BTW moulinette sucking here - it's not handling it. Finally, what's we need to add to our Piscine atoi() to handle such edge cases after calculating actual result:`
- guard against res > LONG_MAX (or INT_MAX as u wish) w/ positive sign. There returning -1;
- guard against res > (unsigned long long)LONG_MAX +1 w/ negative sign. There returning 0;
P.S.: typecasting to unsigned long long + 1 needed to represent bigger value then LONG_MAX could actually supply, because negative value considering 0 as one of possible values and not assuming it as additional;
``` 

```EDGE_CASES
>normal 
ft_atoi("42") 
ft_atoi("-42") 

>spaces and signs 
ft_atoi(" +42") // return 42 
ft_atoi(" --42") // Multiple signs, return 0
ft_atoi("+-42") // Conflicting back-to-back signs, returns 0

>non-numeric characters 
ft_atoi("42a73") // return 42
ft_atoi("a42") // return 0
```
SRC: https://github.com/lattera/glibc/blob/master/stdlib/atoi.c

MAN: https://man.archlinux.org/man/core/man-pages/atoi.3.en