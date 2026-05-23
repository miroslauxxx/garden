```c
char **ft_split(char const *s, char c);
```
DESCRIPTION:	
	`Allocates memory (using malloc(3)) and returns an array of strings obtained by splitting ’s’ using the character ’c’ as a delimiter. Each string in the returned array is allocated independently. The array of pointers itself is also allocated dynamically. The returned array must be NULL terminated.`

RETURN VALUE:
	The array of new strings resulting from the split. NULL if any allocation fails. The returned structure will be released using: 1) free() on each string in the array; 2) free() the array itself

#malloc #free #2d #split #string #strings #free #libft 

```NOTES 

``` 

```EDGE_CASES

```
SRC: 

MAN: