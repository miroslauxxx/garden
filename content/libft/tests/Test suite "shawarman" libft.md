	ft_calloc - memory must be allocated, if zero - malloc(0), all the allocated bytes fulfilled with zeros, guard against overflow must be passed. 
	+ft_memset - exactly size of n memory must be fulfilled with certain ascii value as character, character overflow must be handled using typecasting, 0 must do nothing. 
	+ft_bzero - same as memset, but fulfilling with zeros and returning nothing. If used memset (instead of reimplementing memset without return value) return value can be ignored. 
	+ft_memcpy - size 0 do nothing, memory overflow not handled, copying exactly n - 1 bytes of src to dst.
	+ft_memmove - size 0 do nothing, memory overflow handled, copying exactly n - 1 bytes of src to dst.
	+ft_memchr - null terminator considered as part of string, so if it passed as character to find - pointer to it must be returned.
	+ft_memcmp - compare with clear strings, compare non-ascii values, 
	ft_strdup - works only with true C strings. 