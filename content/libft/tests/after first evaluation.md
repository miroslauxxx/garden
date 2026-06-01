### size_t: with negative value 

  
### calloc: handling zero arguments


### strchr - why cannot use return for all cases
`stupid question, don't cry try again` 

### fd for negative number


### Ftsplit how get next word remembers it's index
`get_next_word(&s, c) - &s is the memory address of the variable s itself.`

### Think about detailed description
`////////////////////////`

### Learn about statement inside conditions of loop
`////////////////////`

### Handling null's in every argument of linked lists functions required ! 



### Atoi handling
`pre-story:
- atoi() : receives string as argument and converts it to integer. Based on manual - it the same as strtol(nptr, NULL, 10);, which basically did the same operation. So generaly this guy works with numbers bigger then LONG_MAX, and until you'll discover docs in detail OR beeing evaluated by experienced and strict student with excellent C knowledge - you'll not be able to handle this edge case. BTW moulinette sucking here - it's not handling it. Finally, what's we need to add to our Piscine atoi() to handle such edge cases after calculating actual result:`
- guard against res > LONG_MAX (or INT_MAX as u wish) w/ positive sign. There returning -1;
- guard against res > (unsigned long long)LONG_MAX +1 w/ negative sign. There returning 0;
P.S.: typecasting to unsigned long long + 1 needed to represent bigger value then LONG_MAX could actually supply, because negative value considering 0 as one of possible values and not assuming it as additional;

### lists functions must include guards for all arguments
++++ 


### ft_lstclear -> ft_lstdelone



### add tags of included functions to docs
++++

### ft_memchr CHANGE TYPECAST FROM INT TO SIZE_T
+++

#### memmove use memcpy
++++

##### when casting to int, use size_t instead write
+++

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

```

#### macro
```
`STDOUT_FILENO` is a POSIX macro defined in `<unistd.h>`
```

#### ft_putnbr_fd
```

```

#### ft_split 57
++++


#### ft_strdup use strlcpy 
++++

####         f(i, s + i); // &s[i] == s + i STRITERI
++++

###  malloc - clears them
+++++

#### strjoin maximal buffer length

#### strlcpy order of src_len +  ft_strlcat check for dst

#### 	if (n == 0) return (0); for strncmp
+++++
### ft_strmapi review and try to replace copying with strlcpy