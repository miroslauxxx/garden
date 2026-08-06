Operating System can be defined as the software that controls the hardware resources of the computer and provides an environment under which programs can run. The interface to the kernel is a layer of software called the system calls. 
![[unix_arch_diagram.png]]
- **Function call** runs code within program in user space. It handles standard logic or math, runs faster and cannot access kernel space. e.g. strlen(), printf(), isspace().
- **System call** is request that program sends to the kernel to perform actions in kernel space. It is slower than a standard function because the system has to switch control to the OS. e.g. open(), read(), fork().
___
[[fileio]] 
![[file_tables.png]]
___
[[processes ]]
![[process_layout.png]]
___
