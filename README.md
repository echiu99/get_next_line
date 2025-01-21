# Get_Next_Line
Get Next Line is a function I implemented in C to read and return a single line from a file descriptor (fd) at a time. This project explores the use of static variables and highlights efficient memory management and file I/O operations.

## Features
- Reads from any valid file descriptor, including files and standard input.
- Returns each line one at a time, including the newline character (\n).
- Handles varying buffer sizes with flexibility and efficiency.
- Designed for robust error handling and compliance with system-level constraints.

## Installation
1. Clone this repository:
```
git clone https://github.com/your-username/get_next_line.git  
cd get_next_line  
```
2. Compile the program using the provided Makefile:
```
make
```

## Usage
You can use the get_next_line function in your projects to read lines from any file descriptor.

### Function Prototype:
```
char *get_next_line(int fd);  
```

### Parameters:
- fd: The file descriptor to read from.
### Return Value:
- Line: Returns the next line from the file descriptor, including the newline character.
- NULL: If there is nothing left to read or an error occurs.

### Example Usage:
```
#include "get_next_line.h"
#include <fcntl.h>
#include <stdio.h>

int main(void) {
    int fd = open("example.txt", O_RDONLY);
    char *line;

    while ((line = get_next_line(fd))) {
        printf("%s", line);
        free(line);
    }
    close(fd);
    return 0;
}
```
### Compilation Example:
Compile with a specified buffer size:
```
cc -Wall -Wextra -Werror -D BUFFER_SIZE=42 get_next_line.c get_next_line_utils.c -o gnl  
```
## Key Features
- Dynamic Buffer Management: The buffer size is defined at compile time using -D BUFFER_SIZE=n.
- Efficient Reads: Reads as little as possible to fetch one line at a time without preloading the entire file.
- Static Variables: Uses static variables to maintain the state between function calls for efficient line retrieval.
- Error Handling: Gracefully handles invalid file descriptors, memory allocation errors, and edge cases like empty files or EOF without \n.

## Bonus Features
- Support for Multiple File Descriptors:
  - The bonus version of get_next_line can handle multiple file descriptors simultaneously.
  - For example, it can read from fd1, then fd2, then fd1 again without losing the state of either file descriptor.

### Bonus File Structure:
- get_next_line_bonus.c
- get_next_line_bonus.h
- get_next_line_utils_bonus.c

### Compilation for Bonus:
```
cc -Wall -Wextra -Werror -D BUFFER_SIZE=42 get_next_line_bonus.c get_next_line_utils_bonus.c -o gnl_bonus
```

## Testing
### Scenarios to Test:
1. Small and large buffer sizes (BUFFER_SIZE=1, BUFFER_SIZE=9999).
2. Files of varying sizes, including empty files and files without a newline at the end.
3. Simultaneous reads from multiple file descriptors.
4. Reading from standard input (fd=0).

### Example Test:
```
echo -e "Line 1\nLine 2\nLine 3" > testfile  
./gnl testfile  
```

## Challenges
This project provided valuable experience with:
- Managing static variables for maintaining function state.
- Memory allocation and optimization for real-time file reading.
- Understanding file descriptors and their behavior in different scenarios.

## About This Project
I developed Get Next Line as part of my journey to master system-level programming in C. This project emphasizes efficient file handling and prepares the foundation for more complex I/O operations in future projects.

## Acknowledgments:
This project is part of the 42 curriculum and is designed to teach the fundamentals of threading, synchronization, and process management. Special thanks to the 42 network for the learning opportunity.
