- **Function call** runs code within program in user space. It handles standard logic or math, runs faster and cannot access kernel space. e.g. strlen(), printf(), isspace().
- **System call** is request that program sends to the kernel to perform actions in kernel space. It is slower than a standard function because the system has to switch control to the OS. e.g. open(), read(), fork().

![[file_tables.png]]
___
[en.linuzapi](https://rogrx.cc/pdf/linux/en.linuzapi.pdf)  The Linux Programming Interface (Michael Kerrisk, 2010) 
___
[ru.linuzapi](https://rogrx.cc/pdf/linux/en.linuzapi.pdf) The Linux Programming Interface (Michael Kerrisk, 2010)
___
[en.clang](https://rogrx.cc/pdf/en.clang.pdf) The C Programming Language (Brian W. Kernighan & Dennis M. Ritchie, 1988)
____
[ru.clang](https://rogrx.cc/pdf/ru.clang.pdf) The C Programming Language (Brian W. Kernighan & Dennis M. Ritchie, 1988)
____
