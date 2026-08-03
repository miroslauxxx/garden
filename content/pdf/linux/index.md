
- **Function call** runs code within program in user space. It handles standard logic or math, runs faster and cannot access kernel space. e.g. strlen(), printf(), isspace().
- **System call** is request that program sends to the kernel to perform actions in kernel space. It is slower than a standard function because the system has to switch control to the OS. e.g. open(), read(), fork().
![[file_tables.png]]

