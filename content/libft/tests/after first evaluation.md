### size_t: with negative value 
`>using negative value for size_t will cause undefined behavior, specially in my  cases with i = -1 when pre-increment happens on start of loop.`
  
### calloc: handling zero arguments
`>man7.org : if n or size is 0, then calloc() returns a unique pointer value that can later be successfully passed to free().`

`>linux.die.net : If nmemb or size is 0, then calloc() returns either NULL, or a unique pointer value that can later be successfully passed to free().`

`>man.openbsd.org : Allocation of a zero size object returns a pointer to a zero size object`

`>man.archlinux.org : If n or size is 0, then calloc() returns a unique pointer value that can later be successfully passed to free()`

`>stackoverflow.com : 7.20.3 If the size of the space requested is zero, the behavior is implementation defined: either a null pointer is returned, or the behavior is as if the size were some nonzero value, except that the returned pointer shall not be used to access an object.`

### strchr - why cannot use return for all cases
`stupid question, don't cry try again` 

### fd for negative number
`wikipedia : File descriptors typically have non-negative integer values, with negative values being reserved to indicate "no value" or error conditions.`

### Ftsplit how get next word remembers it's index
`get_next_word(&s, c) - &s is the memory address of the variable s itself.`

### Think about detailed description
`////////////////////////`

### Learn about statement inside conditions of loop
`////////////////////`

### Handling null's in lists (gpt suggests)
`ft_lstadd_front : if (!lst || !new) return ;`
`ft_lstiter : if (!lst || !f) return ;`


### Atoi handling 213456765432345678765432345678765432345676543234567

### lists functions must include guards for all arguments


### ft_lstclear -> ft_lstdelone


### add tags of included functions to docs

### ft_memchr CHANGE TYPECAST FROM INT TO SIZE_T


#### memmove use memcpy

##### when casting to int, use size_t instead write

### fd tests
```
batch related to testing fd functions:
>open()
>close()
>write()
///On  success,  the number of bytes written is returned.  On error, -1 is returned, and errno is set to indicate the cause of the error.
>read()
>unlink()
>lseek()
```

ft_putchar_fd
```
void	ft_putstr_fd(char *s, int fd)
{
	int	i;

	if (fd < 0)
		return ;
	i = -1;
	while (s[++i] && write(fd, &s[i], sizeof(char)))
		;
}

```

#### why gdb shows only one step there ?! 
```
while (s[++i] && write(fd, &s[i], sizeof(char)))

```

#### macro
```
`STDOUT_FILENO` is a POSIX macro defined in `<unistd.h>`
```

#### ft_putnbr_fd
```
optimize using buffer
```

#### ft_split 57


#### ft_strdup use strlcpy 

####         f(i, s + i); // &s[i] == s + i STRITERI