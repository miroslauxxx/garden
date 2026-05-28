```c
t_list *ft_lstmap(t_list *lst, void *(*f)(void *), void (*del)(void *));
```
DESCRIPTION:	
`Iterates through the list ’lst’, applies the function ’f’ to each node’s content, and creates a new list resulting of the successive applications of the function ’f’. The ’del’ function is used to delete the content of a node if needed.`

RETURN VALUE:
`The new list. NULL if the allocation fails.`

#lists #iterate #apply #malloc #free #libft

```NOTES 

``` 

```EDGE_CASES

```
SRC: 

MAN: