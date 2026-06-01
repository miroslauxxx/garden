```c
#include <stdlib.h>
void *calloc(size_t n, size_t size);
```
DESCRIPTION:
	`The calloc() function allocates memory for an array of n elements of size bytes each and returns a pointer to the allocated memory. The memory is set to zero. If n or size is 0, then calloc() returns a unique pointer value that can later be successfully passed to free()`

`free() `
	`The free() function frees the memory space pointed to by p, which must have been returned by a previous call to malloc() or related functions. Otherwise, or if p has already been freed, undefined behavior occurs. If p is NULL, no operation is performed.`

RETURN VALUE:
	Return a pointer to the allocated memory, which is suitably aligned for any type that fits into the requested size or less. On error, these functions return NULL. 

#setting #memory #malloc #stdlib  #libft
#ft_bzero

```NOTES 
//nmemb non null and size < size_t-1 / nmemb
//Allocate memory 
//Initialize the entire allocated memory block to zero
``` 

```EDGE_CASES
// normal
calloc(10, sizeof(char)) // Returns a valid unique pointer  

// count == 0 or size == 0
void *ptr1 = ft_calloc(0, 10); // Returns a valid unique pointer    
void *ptr2 = ft_calloc(5, 0);  // Returns a valid unique pointer

// integer overflow 
ft_calloc(SIZE_MAX, 2) // Multiplication overflows size_t. Safe check returns NULL.


>man7.org : if n or size is 0, then calloc() returns a unique pointer value that can later be successfully passed to free().

>linux.die.net : If nmemb or size is 0, then calloc() returns either NULL, or a unique pointer value that can later be successfully passed to free().

>man.openbsd.org : Allocation of a zero size object returns a pointer to a zero size object

>man.archlinux.org : If n or size is 0, then calloc() returns a unique pointer value that can later be successfully passed to free()

>stackoverflow.com : 7.20.3 If the size of the space requested is zero, the behavior is implementation defined: either a null pointer is returned, or the behavior is as if the size were some nonzero value, except that the returned pointer shall not be used to access an object.
```
SRC: https://github.com/gcc-mirror/gcc/blob/master/libiberty/calloc.c
SRC: https://github.com/kraj/uClibc/blob/master/libc/stdlib/malloc/calloc.c

MAN: https://man.archlinux.org/man/calloc.3