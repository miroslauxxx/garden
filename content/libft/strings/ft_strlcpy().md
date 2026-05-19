```
#include <string.h>
size_t strlcpy(char *dst, const char *src, size_t size);
```
DESCRIPTION:	
	`The strlcpy() function copies up to size - 1 characters from the NUL-terminated string src to dst, NUL-terminating the result. strlcpy() take the full size of the buffer (not just the length) and guarantee to NUL-terminate the result as long as size is larger than 0. Byte for the NUL should be included in size.  It operate only on true “C” strings, so src must be NUL-terminated.`

RETURN VALUE:
	Length of src.

#copy #string #libft 

```NOTES 
> returns src_len anyway - if size == 0 or on success 
> copying until iteration reach size length (src[i] && i < (size - 1))
> setting last byte as '\0'
``` 

```EDGE_CASES
// normal
char d[10] = "Hi"; 
ft_strlcat(d, "There", 10)  // d becomes "HiThere", return 7

// truncation (buffer too small)
char d[6] = "Hi";
ft_strlcat(d, "There", 6)   // d becomes "HiThe\0", return 7

// buffer size smaller than original dest length
char d[5] = "Hello";
ft_strlcat(d, "World", 3)   // d stays "Hello", return 8.

// zero size buffer boundary
char d[5] = "Hi";
ft_strlcat(d, "There", 0)   // d stays "Hi", return 5

// empty source string
char d[5] = "Hi";
ft_strlcat(d, "", 5)        // d stays "Hi", return 2
```