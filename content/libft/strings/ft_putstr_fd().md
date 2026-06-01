```c
void ft_putstr_fd(char *s, int fd);
```
DESCRIPTION:	
`Outputs the string ’s’ to the specified file descriptor.`

RETURN VALUE:
`None`

#string #print #fd #write #libft

```NOTES 
>using negative value for size_t will cause undefined behavior, specially in my  cases with i = -1 when pre-increment happens on start of loop.

while (s[++i] && write(fd, &s[i], sizeof(char)))
	;
// because of no statetement inside loop, that's a reason why it's not showing it as only one step, if you wish to debug each step - debugger friednly version must be implemented with iteration in statement.

// -O0  flat to turn off all optimizations and show each step of execution. Restrict keyword also considered as optimization stuff. 

wikipedia : File descriptors typically have non-negative integer values, with negative values being reserved to indicate "no value" or error conditions.
``` 

```EDGE_CASES

```
SRC: 

MAN: