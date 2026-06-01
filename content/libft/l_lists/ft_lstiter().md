```c
void ft_lstiter(t_list *lst, void (*f)(void *));
```
DESCRIPTION:	
`Iterates through the list ’lst’ and applies the function ’f’ to the content of each node.`

RETURN VALUE:
`None`

#lists #iterate #apply #libft

```NOTES 
using of lstclear is not possible, because in lstclear we are expecting any function that could be applied as delete function, basically if we want to pass void func that do nothing - we must be able to handle it. 
``` 

```EDGE_CASES

```
SRC: 

MAN: