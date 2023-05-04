# Non-invasive embed-resources
Embed any resource files into your C/C++ executable/library made with CMake project.

You only have to add a piece of code into `CMakeLists.txt` of the project.

## Installation
Copy all lines in `non-invasive-embed-resources.cmake` and paste it into the CMakeLists.txt.

Alternatively, you can download `non-invasive-embed-resources.cmake` and include it from the CMakeLists.txt.

Then you can use `embed_resources()` function.

## Usage
In `CMakeLists.txt`

`embed_resources(<target> [<path/to/item.1> ...])`

In C/C++ code
```
extern "C" const char path_to_item_1[]; // address of the first byte of the data
extern "C" const unsigned path_to_item_1_size; // size of the data
```

## Example
In `CMakeLists.txt`

```
embed_resources(${PROJECT_NAME}
    res/document.txt
    res/image.png
)
```

In C/C++ code
```
#include <stdio.h>

// null character is added at the tail so that
// you can read it as C-style string if the data is a text file
extern "C" const char res_document_txt[];

extern "C" const char res_image_png[];
extern "C" const unsigned res_image_png_size;
// _size variable represents the original file size
// (additional null character is not included)

int main()
{
    printf("%s\n", res_document_txt);
    
    int i;
    for(i = 0; i < res_image_png_size; ++i)
    {
        printf("%x\n", res_image_png[i]);
    }
}
```
