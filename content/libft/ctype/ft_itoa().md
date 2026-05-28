```c
char *ft_itoa(int n);
```
DESCRIPTION:	
	`Allocates memory and returns a string representing the integer received as an argument.`

RETURN VALUE:
The string representing the integer. NULL if the allocation fails.

#conversion #integer #string #malloc #libft 

```NOTES 
>get_num_len - n /= 10; len++;
>MALLOC + close string 
>if 0, if < 0, 
>if > 0 str[--len] = (nbr % 10) + '0'; nbr /= 10; // --len means null at very end
``` 

```EDGE_CASES
>normal
ft_itoa(42) // "42"
ft_itoa(-42) // "-42"
ft_itoa(0) // "0"
ft_itoa(2147483647) // (INT_MAX), "2147483647"
ft_itoa(-2147483648) // (INT_MIN), "-2147483648"
```