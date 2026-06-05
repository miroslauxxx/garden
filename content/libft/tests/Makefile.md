#### Following document represents my own discovery of writing makefiles, all the references and sources will be mentioned at the bottom.

```
gcc -I libft ft_memcpy_test.c libft/libft.h libft/ft_memcpy.c util.c util.h shawarman-libft.h
```

/usr/bin/ld: libft/libft.a(ft_substr.o): warning: relocation in read-only section `.text'
/usr/bin/ld: warning: creating DT_TEXTREL in a PIE
