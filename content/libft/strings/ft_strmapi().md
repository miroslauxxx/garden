```c
char *ft_strmapi(char const *s, char (*f)(unsigned int, char));
```
DESCRIPTION:	
`Applies the function f to each character of the string s, passing its index as the first argument and the character itself as the second. A new string is created (using malloc(3)) to store the results from the successive applications of f.`

RETURN VALUE:
`The string created from the successive applications of ’f’. Returns NULL if the allocation fails.`

#iterate #apply #copy #string #malloc #libft

```NOTES 

``` 

```EDGE_CASES

```
SRC: 

MAN: