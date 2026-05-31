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

### fd tests
```
batch related to testing fd functions:
>open()
>close()
>read()
>unlink()
>lseek()
```

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