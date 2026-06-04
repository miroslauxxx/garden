	+ft_calloc - memory must be allocated, if zero - malloc(0), all the allocated bytes fulfilled with zeros, guard against overflow must be passed. 
	+ft_memset - exactly size of n memory must be fulfilled with certain ascii value as character, character overflow must be handled using typecasting, 0 must do nothing. 
	+ft_bzero - same as memset, but fulfilling with zeros and returning nothing. If used memset (instead of reimplementing memset without return value) return value can be ignored. 
	+ft_memcpy - size 0 do nothing, memory overflow not handled, copying exactly n - 1 bytes of src to dst.
	+ft_memmove - size 0 do nothing, memory overflow handled, copying exactly n - 1 bytes of src to dst.
	+ft_memchr - null terminator considered as part of string, so if it passed as character to find - pointer to it must be returned.
	+ft_memcmp - compare with clear strings, compare non-ascii values, 
	+ft_strdup - works only with true C strings. 



	+ft_strlen - default string, string including \0 with characters after it, non-printable characters, clear string
	ft_strlcpy - ebala
	ft_strlcat - ebala suka !!!!
	ft_strchr - +++
	ft_strrchr - +++
	ft_strncmp - +++
	ft_strnstr - +++  
	ft_substr - +++ 
	ft_strjoin - +++ 
	ft_strtrim - +++ 
	ft_split - +
	ft_strmapi - +
	ft_striteri - ++ 
	ft_atoi - +++ 
	ft_itoa - ++  


	ft_isalpha - +++
	ft_isdigit - +++
	ft_isalnum  - +++
	ft_isascii - +++
	ft_isprint - +++
	ft_toupper - +++
	ft_tolower - +++

	ft_putchar_fd - +
	ft_putstr_fd - +
	ft_putendl_fd - +
	ft_putnbr_fd - +

- feature: specify list of functions you want to test with
    - separate file
    - using `make` argument
- feature: test functions by their groups
- feature: test for additional stuff (atoi, fd, null as value in lists, using of non-ft functions etc.)
- readme file: includes detailed description of all tested stuff, where to focus attention when reviewing, how to contribute, my own experience, how and why i decided to implement this library
- use one cycle for all char classification functions

