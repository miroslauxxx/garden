isalpha compare results with original function of entire ascii table using loop

isdigit compare results with original function of entire ascii table using loop

isalnum compare results with original function of entire ascii table using loop

isascii compare results with original function of entire ascii table using loop

isprint compare results with original function of entire ascii table using loop

toupper compare with original function all lowercase values results using loop

tolower compare with original function all uppercase values results using loop\

strlen calculate length of clear and non-clear strings

memset pass 0 as size - nothing must happen with array, pass something with non-zero size and check is expected bytes (not less not more) has been overwritten

bzero pass 0 as size - nothing must happen with array, pass non-zero size and check is expected bytes (not less not more) has been overwritten

memcpy pass 0 as size - nothing must happen with array, pass NULL as src - must not crush, normal copying 

memmove pass NULL as dest, pass NULL as src, check forward and backward copying, pass 0 as size

strlcpy test with sizes: 0,1,2,-1, less for 1 then src, equal to src and 1 more then src, more big then src, passing "" as src.

strlcat test with sizes: 0,1,2,-1, less for 1 then src, equal to src and 1 more then src, more big then src, passing "" as src.

strchr - find something that in string, not in string, pass 0 as size, check is character overflow closes circle with ascii table

strrchr - find something that in string, not in string, pass 0 as size, check is character overflow closes circle with ascii table

strncmp - pass 0 as size, very first and very last character difference, very last character difference when out of size, size bigger then strings, 1 character and clear, two clear strings. May be with comparing of original one

memchr - pass 0 as size, pass 0 as argument, pass something that already in string, character overflow.

memcmp - equal arrays, equal arrays with character overflow, different arrays.

strnstr - pass -1, 0 as size, find clear string, something that not exist, search in clear string.

atoi - negative, positive, (+/-)zero, overflow of int min/max, add characters, add couple of -/+, string with digits, starts with a lot of spaces and/or 9-13 ascii

calloc - 0 as size  - must be able to freed, 20 as size, overflow checks, negative values as arguments

strdup - duplicate clear string and true string

