```c
#include <string.h>
size_t strlcpy(char *dst, const char *src, size_t size);
```
DESCRIPTION:	
	`The strlcpy() function copies up to size - 1 characters from the NUL-terminated string src to dst, NUL-terminating the result. strlcpy() take the full size of the buffer (not just the length) and guarantee to NUL-terminate the result as long as size is larger than 0. Byte for the NUL should be included in size.  It operate only on true “C” strings, so src must be NUL-terminated.`

RETURN VALUE:
	Length of src.

#copy #string #bsd #libft 
#ft_strlen 

```NOTES 
> returns src_len anyway
> copying until iteration reach size length (src[i] && i < (size - 1))
> setting last byte as '\0'
``` 

```EDGE_CASES
>size too small
char dst1[6] = "Hi";
ft_strlcpy(dst1, "There", 4) == 5) // dst1 == "The"

>full copy
char dst2[6] = "Hi";
ft_strlcpy(dst2, "There", 6) == 5); // dst2 = "There"

>size == 0
char dst3[5] = "Hi";
ft_strlcpy(dst3, "There", 0) == 5); dst3 = "Hi"

>clear string as source
char dst4[5] = "Hi";
ft_strlcpy(dst4, "", 5) == 0); // dst4 = ""
```
SRC: 
https://github.com/OPCFoundation/UA-LDS/blob/master/strlcpy.c
https://github.com/apple/darwin-xnu/blob/main/osfmk/arm/strlcpy.c

MAN:
https://linux.die.net/man/3/strlcpy