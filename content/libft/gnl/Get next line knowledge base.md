- File Descriptors (Standard input, output, error, and file-handling IDs)
    
- System Calls for I/O (read, open, close)
    
- Static Variables (Lifecycle, scope, and persistence across function calls)
    
- Memory Management (Dynamic allocation with malloc/calloc, avoiding leaks with free, valgrind debugging)
    
- Buffer-based Reading (Handling arbitrary BUFFER_SIZE values, processing partial reads, managing chunked data)
    
- String Manipulation (Pointer arithmetic, tracking newlines with strchr, copying/duplicating strings with strndup/strdup)
    
- Linked Lists (Dynamic node creation, list traversal, surgical deletion of nodes, managing head pointers)
    
- Data Structures / Encapsulation (Grouping file descriptors with their respective residual text buffers)
    
- File I/O Mechanics (EOF detection, error checking, tracking current file offset)
    
- Compilation and Preprocessor Directives (Defining macros like BUFFER_SIZE via compiler flags with -D)