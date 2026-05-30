```c
char **ft_split(char const *s, char c);
```
DESCRIPTION:	
	`Allocates memory (using malloc(3)) and returns an array of strings obtained by splitting ’s’ using the character ’c’ as a delimiter. Each string in the returned array is allocated independently. The array of pointers itself is also allocated dynamically. The returned array must be NULL terminated.`

RETURN VALUE:
	The array of new strings resulting from the split. NULL if any allocation fails. The returned structure will be released using: 1) free() on each string in the array; 2) free() the array itself

#malloc #free #2d #split #string #strings #free #libft 

```NOTES 
ft_split sets s to point to the start: "  Hi  Me" 
Loop Iteration 0: * ft_split calls get_next_word(&s, ' '). 
Inside get_next_word, Step A skips the two spaces. s is advanced. 
Step B reads "Hi" and stops at the next space. s is advanced again. get_next_word returns "Hi". 
Back in ft_split, s now points to "  Me". 
Loop Iteration 1: ft_split calls get_next_word(&s, ' ') again. 
Inside get_next_word, Step A skips the two spaces between the words. 
s is advanced. Step B reads "Me" and stops at \0. 
s is advanced to the end string terminator. 
get_next_word returns "Me". 
Back in ft_split, s now points to \0. 
Loop ends, matrix is null-terminated and returned.

It remembers its position because ft_split passes the memory address of its own pointer variable (&s) to get_next_word.

By accepting a double pointer (const char str), get_next_word gains direct reference to the original pointer. When it increments *str to scan through delimiters and characters, it is not moving a local copy—it is directly manipulating the tracking variable s back in ft_split.

Consequently, when get_next_word returns a completed word, s has been permanently advanced in memory to the threshold of the next word, seamlessly preserving the state for the subsequent loop iteration.
``` 

```EDGE_CASES

```
SRC: 

MAN: