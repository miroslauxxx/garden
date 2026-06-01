_This project has been created as part of the 42 curriculum by milnicki._

Description
C programming can be quite tedious without access to the highly useful standard functions. This project aims to help understand how these functions work by implementing them and learning to use them effectively. Following project introduces library which will be valuable for future C school assignments. Main goal of project - learning C-lang during implementing norminette-compilant functions and tests for them. As tests not mentioned as mandatory part of project - they are highly recommended for deeper understanding of stuff "under the hood".

Instructions
	complile: `make`
	rebuild: `make re`
	to clean binaries `make clean` or `make fclean`

Resources
    - Tests used (user/repo): Buzhanin/lft-adhoc-tests, FranFrau/Supreme-Tester-Libft, also work on my own tests: in progress.
    - ai used as a "source of truth" documentation reference, concept clarification, and edge-case discovery. 100% of the code logic and implementation was structurally designed and written by me (`milnicki`).
    - Made use of a lot resources, too many to write. Will update later.

Detailed description could be found on my digital garden https://garden.miroslau.workers.dev/index 

Functions to classify and manipulate with characters:

	int ft_isalpha(int c); // returns 1 if `c` is in ascii alphabet range 
	int ft_isdigit(int c); // returns 1 if `c` is in ascii digit range
	int ft_isalnum(int c); // returns 1 if `c` is in ascii alphabet or digit range  
	int ft_isascii(int c); // returns 1 if `c` is in ascii range
	int ft_isprint(int c); // returns 1 if `c` is in ascii printable character range
	int ft_toupper(int c); // converts `c` to uppercase character if it's lowercase 
	int ft_tolower(int c); // converts `c` to lowercase character if it's uppercase 

Functions to manipulate strings:

	size_t ft_strlen(const char *s); // calculate `s` length
	size_t ft_strlcpy(char *dst, const char *src, size_t size); // copy at most bytes `size` from string `src` to `dst` and add null terminator 
	size_t ft_strlcat(char *dst, const char *src, size_t size); // concatenate `dst` and `src` to buffer with at most `size` bytes
	char *ft_strchr(const char *s, int c); // find first occurrence of character `c` in string `s`
	char *ft_strrchr(const char *s, int c); // last occurrence of character `c` in string `s`
	int ft_strncmp(const char *s1, const char *s2, size_t n); // compare at most `n` bytes of strings `s1` and `s2` character by character 
	char *ft_strnstr(const char *big, const char *little, size_t len); // scan at most `len` bytes of string `big` for occurrence of string `little` 
	char *ft_substr(char const *s, unsigned int start, size_t len); // create new string from `s`, `start` is index of `s` from which new string starts and `len` it's length
	char *ft_strjoin(char const *s1, char const *s2); // concatenate `s1` and `s2` into new string
	char *ft_strtrim(char const *s, char const *set); // trim `set` from `s` string and return trimmed result
	char **ft_split(char const *s, char c); // using `c` as delimiter split `s` on array of pointers to each word
	char *ft_strmapi(char const *s, char (*f)(unsigned int, char)); // apply function `f` to each character of string `s` and place em into fresh string
	void ft_striteri(char *s, void (*f)(unsigned int, char *)); // iterate over string `s` and apply function `f` to each character specified by index  
	int ft_atoi(const char *nptr);  // converts string pointer by `*nptr` to integer
	char *ft_itoa(int n); // converts integer `n`to string and allocates memory for it 
  

Functions to manipulate memory:

	void *ft_calloc(size_t nmemb, size_t size); // allocate `nmemb` * `size` of memory and fulfill with zero's 
	void *ft_memset(void *s, int c, size_t n); // set character c for each cell of memory pointer by `s` 
	void ft_bzero(void *s, size_t n); // same as ft_memset(s, 0, n);
	void *ft_memcpy(void *dest, const void *src, size_t n); // copy at most bytes `n` from `src` to `dest`, do not consider memory overlaps 
	void *ft_memmove(void *dest, const void *src, size_t n); // copy at most bytes `n` from `src` to `dest`, if overlap - copy backward, if no overlap - copy forward
	void *ft_memchr(const void *s, int c, size_t n); //  scan at most bytes `n` for occurrence of characher `c` in memory area pointed to by `s` 
	int ft_memcmp(const void *s1, const void *s2, size_t n); // compare at most `n` bytes of memory pointed to by `s1` with memory pointed to by `s2` and return subtraction diff 
	char *ft_strdup(const char *s);	// duplicate string pointer to by `s` into freshly allocated string

Functions to write to a file descriptor

	void ft_putchar_fd(char c, int fd); // write() character into certain file descriptor
	void ft_putstr_fd(char *s, int fd); // write() string pointed to by `s` character by character into certain file descriptor
	void ft_putendl_fd(char *s, int fd); // write() string pointed to by `s` character by character into certain file descriptor and add new line  `\n`
	void ft_putnbr_fd(int n, int fd); // write() number into certain file descriptor

Functions to manipulate with linked lists 

	t_list *ft_lstnew(void *content); // add new element of list 
	void ft_lstadd_front(t_list **lst, t_list *new); // add new element into start of list
	int ft_lstsize(t_list *lst); // count amount of list elements
	t_list *ft_lstlast(t_list *lst); // return pointer to last list element
	void ft_lstadd_back(t_list **lst, t_list *new); // add new element into end of list
	void ft_lstdelone(t_list *lst, void (*del)(void *)); // delete element pointed by `lst` using `del` function 
	void ft_lstclear(t_list **lst, void (*del)(void *)); // clear entire list pointed to by `lst` with func `del` and free it's memory 
	void ft_lstiter(t_list *lst, void (*f)(void *)); // iterate over list and apply function `f` for `content` of each node 
	t_list *ft_lstmap(t_list *lst, void *(*f)(void *), void (*del)(void *)); // iterate over list and apply function `f` for `content` of each node and create fresh list elements from applied stuff. Handle unsuccessful attempts with `del` function. 
