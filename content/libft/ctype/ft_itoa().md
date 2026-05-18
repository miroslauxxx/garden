#conversion #character #malloc #libft_f #libft 
```
char *ft_itoa(int n);
```
DESCRIPTION:	
	`Allocates memory and returns a string representing the integer received as an argument.`

RETURN VALUE:
The string representing the integer. NULL if the allocation fails.



```NOTES 
something similar with putnbr
``` 

```EDGE_CASES
ft_itoa(42) // "42"
ft_itoa(-42) // "-42"
ft_itoa(0) // "0"
ft_itoa(2147483647) // (INT_MAX), "2147483647"
ft_itoa(-2147483648) // (INT_MIN), "-2147483648"
```