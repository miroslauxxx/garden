```
#include <string.h>
size_t strlcat(char *dst, const char *src, size_t size);
```
DESCRIPTION:	
	`The strlcat() function appends the NUL-terminated string src to the end of dst. It will append at most size - strlen(dst) - 1 bytes, NUL-terminating the result. strlcat() take the full size of the buffer (not just the length) and guarantee to NUL-terminate the result as long as there is at least one byte free in dst. Byte for the NUL should be included in size.  It operate only on true “C” strings, both src and dst must be NUL-terminated.`

RETURN VALUE:
	Initial length of dst plus the length of src.

#concatenate #string #libft

```NOTES 
> returns src_len + dst_len on success or src_len + size if dst_len == size 
> copying src[i] to dst[i + dst_l] until (src[i] && (dst_l + i + 1) < size)
> setting i + dst_l (rest or at least one byte of dst) as '\0' 
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
ft_strlcat(d, "World", 3) // d stays "Hello", return 8

// zero size buffer boundary
char d[5] = "Hi";
ft_strlcat(d, "There", 0) // d stays "Hi", return 5

// empty source string
char d[5] = "Hi";
ft_strlcat(d, "", 5) // d stays "Hi", return 2
```