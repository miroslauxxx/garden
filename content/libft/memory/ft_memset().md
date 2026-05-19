```
#include <string.h>
void *memset(void *s, int c, size_t n);
```
DESCRIPTION:	
	`The memset() function fills the first n bytes of the memory area pointed to by s with the constant byte c.`

RETURN VALUE:
	Returns pointer to modified piece of memory. 

#setting #memory #string #libft

```NOTES
>>unsigned char!
>Cast the void pointer to an unsigned char pointer to work byte-by-byte
>Cast the int to an unsigned char and loop through the memory and assign the value `n` times
``` 

```EDGE_CASES
> n == 0
char str[10] = "Hello";
ft_memset(str, 'X', 0);

> filling non-char arrays
int arr[5]; 
ft_memset(arr, 1, sizeof(arr)); // arr[0-4] will not equal 1. It will equal 16,843,009 each. It happens because an int is made of 4 bytes, the integer looks like 00000001 00000001 00000001 00000001 in binary. In decimal, that number is $16,843,009$.

> character truncation
char str[5];
ft_memset(str, 257, 4); // it will not crash because compiler converts the `int` to an `unsigned char`, so memory will be filled with ASCII 1 value (SOH)
```
SRC: https://github.com/openbsd/src/blob/master/lib/libc/string/memset.c

MAN: https://man.archlinux.org/man/memset.3