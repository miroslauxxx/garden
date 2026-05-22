```c
char *ft_substr(char const *s, unsigned int start, size_t len);
```
DESCRIPTION:	
	`Allocates memory (using malloc(3)) and returns a substring from the string ’s’. The substring starts at index ’start’ and has a maximum length of ’len’.`

RETURN VALUE:
	The substring. NULL if the allocation fails.

#string #copy #malloc #libft

```C
if (start >= s_len)
	ft_strdup("");
if (len > s_len - start)
	len = s_len - start;
// LEN + 1 FOR MALLOC
``` 

```EDGE_CASES
char *substr_str1 = "holy forty two six six six";
// normal behaviour 
ft_substr(substr_str1, 15, 11)
ft_substr(substr_str1, 19, 7)
ft_substr(substr_str1, 0, 8)

// NULL string passed
ft_substr(NULL, 19, 7)

// start out of *s range 
ft_substr(substr_str1, 48, 0)

// len is bigger then expected 
ft_substr(substr_str1, 15, 500)

// len is 0
ft_substr(substr_str1, 5, 0)
```
