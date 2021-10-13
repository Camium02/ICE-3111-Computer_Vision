---
title: Lab 3 -- Introduction to OpenCV in C/C++ and Python, and Point Operators.
author: Dr Franck P. Vidal
subtitle: ICE-3111 Computer Vision
date: Week 3
keywords: ICE3111, Computer Vision, C/C++, python, image processing, OpenCV, Bangor University, School of Computer Science and Electronic Engineering
institute: School of Computer Science and Electronic Engineering, Bangor University
---

# Lab 3 -- Introduction to OpenCV in C/C++ and Python, and Point Operators


- (worth 30% of Assignment 1)
- Deadline: 20/10/2021 at 23:59
- Write your answers in the template provided: [questionnaire.docx](https://github.com/effepivi/ICE-3111-Computer_Vision/raw/main/Labs/Lab-03/questionnaire.docx)

## Introduction

Look at the ellipses in the mindmap. It illustrates which concepts we are discussing this week.

![Week 3 mindmap](../../mindmap/Week-03/screenshot.png)

This week we studied point operators in the lecture.
For example, we saw how to improve the contrast of an image that is dull using a simple, but powerful, technique called "histogram stretching" (also called min-max normalisation).

Today we will:

1. Install OpenCV if needed:
    - Either use C/C++, or,
    - Python.
2. Load an image.
3. Display an image.
4. Convert a RGB image in a greyscale image.
5. Find the smallest and largest pixel values in an image.
6. Improve the contrast of an image:
    - by hand using the equation seen in the lecture,
    - using OpenCV's function.
7. Change the dynamic range using a log transform.
8. Blend two images in a for loop to create an animation.


## 1. Preliminaries: Install OpenCV if needed

Ask yourself if you prefer to write code using C, C++ or Python.
Have you installed OpenCV for your favourite language? If not, refer to [Lab 0](../Lab-00).
For the lab machines, it should be done, at least for the C and C++ language.

- [Click here for instructions in C/C++](C-CXX.md)
- [Click here for instructions in Python](Python.md)

## 2. and 3. Load and display an image

Before we start, the technical documentation is available at: [https://docs.opencv.org/4.5.4/index.html](https://docs.opencv.org/4.5.4/index.html). The OpenCV's functions we will use are:

```cxx
imread() // To read an image from a file
imshow() // To display an image in a window
```
Both functions are available in C, C++ and Python. Find them in the online documentation and read the corresponding text. I often consult the documentation when I forget the name of a function or when I need to find the right sequence of parameters. This is what I get:

### C/C++
```cpp
Mat cv::imread (const String&	filename, int	flags = IMREAD_COLOR );

void cv::imshow (	const String&	winname, InputArray	mat );
```

### Python

```Python
cv.imread( filename[, flags] ) -> 	retval

cv.imshow( winname, mat ) -> 	None
```

### Our first OpenCV program

#### C/C++

In C and C++, we will use CMake to generate a project that you can use in MS Visual C++ or Apple XCode. CMake relies on a text file called `CMakeLists.txt` to configure the project.

1. Create two new files (`CMakeLists.txt` and `displayImage.cxx`). Make sure the file extensions are correct. MS Windows tend to hide them. **If you are using MS Windows, make sure you show the file extensions in the file explorer!** `CMakeLists.txt` contains:


2. Set the minimum CMake version to at least 3.1. It is needed to enable  the C++ 11 standard.
```cmake
CMAKE_MINIMUM_REQUIRED(VERSION 3.1)
PROJECT(ICE-3111-Lab-Week3)
```

3. C++ 11 is a requirement for OpenCV 4, enable it with:

```cmake
set (CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
```

4. For MS Windows users, add where OpenCV might be installed (look in D: first, then in C:). If you installed OpenCV somewhere else, adjust the path accordingly:

```cmake
IF (WIN32)
    SET (CMAKE_PREFIX_PATH ${CMAKE_PREFIX_PATH} "D:\\opencv\\build")
    SET (CMAKE_PREFIX_PATH ${CMAKE_PREFIX_PATH} "C:\\opencv\\build")
ENDIF (WIN32)
```

5. Find OpenCV
```cmake
FIND_PACKAGE(OpenCV REQUIRED)
```

6. The executable program
```cmake
ADD_EXECUTABLE (displayImage   displayImage.cxx)
```

7. Add OpenCV's header path for the program
```cmake
TARGET_INCLUDE_DIRECTORIES(displayImage PUBLIC ${OpenCV_INCLUDE_DIRS})
```

8. Add OpenCV libraries to each the program
```cmake
TARGET_LINK_LIBRARIES (displayImage   ${OpenCV_LIBS})
```

9. If windows is used, copy the DLLs into the project directory
```cmake
SET (CV_VERSION_STRING ${OpenCV_VERSION_MAJOR}${OpenCV_VERSION_MINOR}${OpenCV_VERSION_PATCH})
IF (WIN32)
    IF ( ${OpenCV_VERSION_MAJOR} EQUAL 4)
        IF (EXISTS "${OpenCV_DIR}/x64/vc15/bin/opencv_videoio_ffmpeg${CV_VERSION_STRING}_64.dll")
            FILE (COPY        "${OpenCV_DIR}/x64/vc15/bin/opencv_videoio_ffmpeg${CV_VERSION_STRING}_64.dll"
                  DESTINATION "${CMAKE_CURRENT_BINARY_DIR}/")
        ELSE ()
            MESSAGE (WARNING "opencv_videoio_ffmpeg${CV_VERSION_STRING}_64.dll is not in ${OpenCV_DIR}/x64/vc15/bin/, you have to make sure is it in the PATH or to copy it manually in your project binary directory")
        ENDIF ()
  ELSE ()
        IF (EXISTS "${OpenCV_DIR}/x64/vc15/bin/opencv_ffmpeg${CV_VERSION_STRING}_64.dll")
            FILE (COPY        "${OpenCV_DIR}/x64/vc15/bin/opencv_ffmpeg${CV_VERSION_STRING}_64.dll"
                  DESTINATION "${CMAKE_CURRENT_BINARY_DIR}/")
        ELSE ()
            MESSAGE (WARNING "opencv_ffmpeg${CV_VERSION_STRING}_64.dll is not in ${OpenCV_DIR}/x64/vc15/bin/, you have to make sure is it in the PATH or to copy it manually in your project binary directory")
        ENDIF ()
  ENDIF ()

    IF (EXISTS "${OpenCV_DIR}/x64/vc15/bin/opencv_videoio_msmf${CV_VERSION_STRING}_64.dll")
        FILE (COPY        "${OpenCV_DIR}/x64/vc15/bin/opencv_videoio_msmf${CV_VERSION_STRING}_64.dll"
              DESTINATION "${CMAKE_CURRENT_BINARY_DIR}/")
    ELSE ()
        MESSAGE (WARNING "opencv_videoio_msmf${CV_VERSION_STRING}_64.dll is not in ${OpenCV_DIR}/x64/vc15/bin/, you have to make sure is it in the PATH or to copy it manually in your project binary directory")
    ENDIF ()

    IF (EXISTS "${OpenCV_DIR}/x64/vc15/bin/opencv_videoio_msmf${CV_VERSION_STRING}_64d.dll")
        FILE (COPY        "${OpenCV_DIR}/x64/vc15/bin/opencv_videoio_msmf${CV_VERSION_STRING}_64d.dll"
              DESTINATION "${CMAKE_CURRENT_BINARY_DIR}/")
    ELSE ()
        MESSAGE (WARNING "opencv_videoio_msmf${CV_VERSION_STRING}_64d.dll is not in ${OpenCV_DIR}/x64/vc15/bin/, you have to make sure is it in the PATH or to copy it manually in your project binary directory")
    ENDIF ()

    IF (EXISTS "${OpenCV_DIR}/x64/vc15/bin/opencv_world${CV_VERSION_STRING}.dll")
        FILE (COPY        "${OpenCV_DIR}/x64/vc15/bin/opencv_world${CV_VERSION_STRING}.dll"
              DESTINATION "${CMAKE_CURRENT_BINARY_DIR}/")
    ELSE ()
        MESSAGE (WARNING "opencv_world${CV_VERSION_STRING}.dll is not in ${OpenCV_DIR}/x64/vc15/bin/, you have to make sure is it in the PATH or to copy it manually in your project binary directory")
    ENDIF ()

    IF (EXISTS "${OpenCV_DIR}/x64/vc15/bin/opencv_world${CV_VERSION_STRING}d.dll")
        FILE (COPY        "${OpenCV_DIR}/x64/vc15/bin/opencv_world${CV_VERSION_STRING}d.dll"
              DESTINATION "${CMAKE_CURRENT_BINARY_DIR}/")
    ELSE ()
        MESSAGE (WARNING "opencv_world${CV_VERSION_STRING}d.dll is not in ${OpenCV_DIR}/x64/vc15/bin/, you have to make sure is it in the PATH or to copy it manually in your project binary directory")
    ENDIF ()
ENDIF (WIN32)    
```

10. Configuring the project using CMake is relatively straightforward. **MAKE SURE YOU USE A GENERATOR THAT SUPPORT 64 BITS.** Every year some people use Win32 instead of Win64. OpenCV is now shipped with the libs compiled in 64 bits only. Win32 won't work.

Do not compile (see "Where to build the binaries:") in the same directory a your source code.

![Project configuration using CMake.](cmake.png)

11. Open the project in your favourite IDE, e.g. MS Visual C++ for Windows, XCode for MacOS. Now you can edit `displayImage.cxx`.

12. Add a preamble to `displayImage.cxx`.

Using C++ comments, add a preamble at the top of your file.
It must describe the program:

    1. the author of the program (you),
    2. the date,
    3. the purpose of the file (inc. the command line options),
    4. the todo-list if anything is missing.

13. Header inclusion

OpenCV uses exceptions. To catch them, we need `<exception>`. To display
text in the console `<iostream>` is required. The main OpenCV header is
`<opencv2/opencv.hpp>`.

```cpp
#include <exception> // Header for catching exceptions
#include <iostream>  // Header to display text in the console
#include <opencv2/opencv.hpp> // Main OpenCV header
```

14. Namespaces

We'll use two namespaces `std` for the standard library, and `cv` for OpenCV.

```cpp
using namespace std;
using namespace cv;
```

15. Main structure

As stated previously, OpenCV uses exceptions. We can (or should) catch
them to handle errors. The structure of the main is (almost always):

```cpp
//-----------------------------
int main(int argc, char** argv)
//-----------------------------
{
    try
    {
        // Check the command line
        if (argc != 2)
        {
            // Create an error message
            std::string error_message;
            error_message  = "usage: ";
            error_message += argv[0];
            error_message += " <input_image>";

            // Throw an error
            throw error_message;
        }

        // Write your own code here
        //....
        //....
        //....
    }
    // An error occured
    catch (const std::exception& error)
    {
        // Display an error message in the console
        cerr << error.what() << endl;
    }
    catch (const std::string& error)
    {
        // Display an error message in the console
        cerr << error << endl;
    }
    catch (const char* error)
    {
        // Display an error message in the console
        cerr << error << endl;
    }
    catch (...)
    {
        // Display an error message in the console
        cerr << "Unnown error caught" << endl;
    }

#ifdef WIN32
#ifdef _DEBUG
    system("pause");
#endif
#endif

    return 0;
}
```

**Read the code in order to understand what it does. As you can see, I commented pretty much every single line of code.** Right, now we have a general skeleton we can use for any OpenCV program.

Now replace the code
```cpp
// Write your own code here
//....
//....
//....
```
with something useful.

16. Arguments of the Command Line

The first program only takes one parameter. It corresponds to the path
of an image file. To make sure the number of arguments is correct, we use:

```cpp
// Check the command line, do we have two arguments?
// argv[0] is always the executable file
// In our case argv[1] should be the name of an image file
if (argc != 2)
{
    // Create an error message
    std::string error_message;
    error_message  = "usage: ";
    error_message += argv[0];
    error_message += " <input_image>";

    // Throw an error
    throw error_message;
}
```

If there was no error, you can use to get the file name:

```cpp
std::string input_filename(argv[1]);
```

17. Reading the File

An image is stored in an instance of the class `Mat`. Note that OpenCV's
namespace is `cv::`. To declare the variable that will hold our image,
type:

```cpp
// Create an image instance
cv::Mat image;
```

In OpenCV 4, the image is loaded using:

```cpp
// Open and read the image
image = cv::imread( input_filename );
```

It is a good practice to check if any error occurred, e.g. to avoid
unspecified behaviours and crashed. If the image is not loaded, its
`data` field is empty. If it is the case we can throw an error as
follows:

```cpp
// The image has not been loaded
if (!image.data)
{
    // Create an error message
    std::string error_message;
    error_message  = "Could not open or find the image \"";
    error_message += input_filename;
    error_message += "\".";

    // Throw an error
    throw error_message;
}
```

18. Displaying the Image

There are four steps to create a window and display and image:

    1.  Create a string to contain the window title (it is used to identify
        the window);
    2.  Create the window;
    3.  Show the image in the window;
    4.  Wait for a user input to leave the window.

It can be done as follows:

```cpp
// Create a string to contain the window title
string window_title;
window_title  = "My OpenCV Display \"";
window_title += input_filename;
window_title += "\"";

// Create the window
cv::namedWindow(window_title, cv::WINDOW_AUTOSIZE);

// Show the image in the window
cv::imshow(window_title, image);

// Wait for a user input to leave the window
cv::waitKey(0);
```

The program is now complete. You can compile it and run it with
different image files to test it.
In your lab report, you must include a listing of your program and put three screenshots (with three different images).

#### Python

1. Create a new file (`displayImage.py`). Make sure the file extension is correct. MS Windows tend to hide them. **If you are using MS Windows, make sure you show the file extensions in the file explorer!**.

2. Open the `displayImage.py` in your favourite text editor.

3. Add the shebang line (useful for Unix computers).

```bash
#!/usr/bin/env python3
```

4. Add a preamble.

Using Python comments, add a preamble at the top of your file.
It must describe the program:

    1. the author of the program (you),
    2. the date,
    3. the purpose of the file (inc. the command line options),
    4. the todo-list if anything is missing.

5. Package inclusion

```python
import sys # to read the command line arguments
import cv2 # cv2 library
```

6. Create the `NoneType`. It is useful when checking errors.

```python
NoneType = type(None)
```

7. Arguments of the Command Line

The first program only takes one parameter. It corresponds to the path
of an image file. To make sure the number of arguments is correct, we use:

```python
# Check the command line, do we have two arguments?
# argv[0] is always the executable file
# In our case argv[1] should be the name of an image file
if len(sys.argv) != 2:
    # Create an error message
    error_message  = "usage: "
    error_message += sys.argv[0]
    error_message += " <input_image>"

    # Throw an error
    raise Exception(error_message)
```

If there was no error, you can use to get the file name:

```python
input_filename = sys.argv[1]
```

8. Reading the File

In OpenCV 4, the image is loaded using:

```python
# Open and read the image
image = cv2.imread( input_filename )
```

It is a good practice to check if any error occurred, e.g. to avoid
unspecified behaviours and crashed. If the image is not loaded, `cv2.imread` returns `None`.
`data` field is empty. If it is the case we can throw an error as
follows:

```python
# The image has not been loaded
if isinstance(image, NoneType):
    # Create an error message
    error_message  = "Could not open or find the image \""
    error_message += input_filename
    error_message += "\"."

    # Throw an error
    raise Exception(error_message)
```

9. Displaying the Image

There are four steps to create a window and display and image:

    1.  Create a string to contain the window title (it is used to identify
        the window);
    2.  Create the window;
    3.  Show the image in the window;
    4.  Wait for a user input to leave the window.

It can be done as follows:

```python
# Create a string to contain the window title
window_title  = "My OpenCV Display \""
window_title += input_filename
window_title += "\""

# Create the window
cv2.namedWindow(window_title, cv2.WINDOW_AUTOSIZE)

# Show the image in the window
cv2.imshow(window_title, image)

# Wait for a user input to leave the window
cv2.waitKey(0)
```

The program is now complete. You run it with
different image files to test it.
In your lab report, you must include a listing of your program and put three screenshots (with three different images).


## 4. Convert a RGB image in a greyscale image.

1. Copy paste your previous program in a new one that you call either `rgb2grey.cxx` or `rgb2grey.py`.
    - If you use C/C++, don't forget to edit `CMakeLists.txt` to add:

```cmake
TARGET_INCLUDE_DIRECTORIES(rgb2grey PUBLIC ${OpenCV_INCLUDE_DIRS})
TARGET_LINK_LIBRARIES (rgb2grey   ${OpenCV_LIBS})
```

2. The command line is:

```bash
rgb2grey  input_filename  output_filename
```

Change the code appropriately.

### C/C++

```cpp
// Check the command line, do we have three arguments?
// argv[0] is always the executable file
// In our case argv[1] should be the name of an input image file
// In our case argv[2] should be the name of an output image file
if (argc != 3)
{
    // Create an error message
    std::string error_message;
    error_message  = "usage: ";
    error_message += argv[0];
    error_message += " <output_image> <>";

    // Throw an error
    throw error_message;
}

std::string input_filename(argv[1]);
std::string output_filename(argv[2]);
```

### Python

```python
# Check the command line, do we have three arguments?
# argv[0] is always the executable file
# In our case argv[1] should be the name of an input image file
# In our case argv[2] should be the name of an output image file
if len(sys.argv) != 3:
    # Create an error message
    error_message  = "usage: "
    error_message += sys.argv[0]
    error_message += " <input_image>"
    error_message += " <output_image>"

    # Throw an error
    raise Exception(error_message)

input_filename = sys.argv[1]
output_filename = sys.argv[2]
```

3. After you read the image and checked that the image was loaded, and before displaying the image, convert it into a greyscale image:

### C/C++

```cpp
cv::Mat grey_image;
cv::cvtColor(image, grey_image, cv::COLOR_RGB2GRAY);
```

### Python

```python
grey_image = cv2.cvtColor(image, cv2.COLOR_RGB2GRAY)
```

4. Don't forget to display the right image, i.e. `grey_image` not `image`.

5. Save the image

The function to save an image is `cv::imwrite(file_name, image)`. It
returns true if the file has been successfully written; false otherwise.
We can use the return value to handle possible errors:

```cpp
// Write the image
if (!cv::imwrite(output_filename, grey_image))
{
    // The image has not been written

    // Create an error message
    std::string error_message;
    error_message  = "Could not write the image \"";
    error_message += output_filename;
    error_message += "\".";

    // Throw an error
    throw error_message;
}
```

```python
# Write the image
if not cv2.imwrite(output_filename, grey_image):
    # The image has not been written

    # Create an error message
    error_message  = "Could not write the image \""
    error_message += output_filename
    error_message += "\"."

    # Throw an error
    raise Exception(error_message)
```

## Saving an Image into a File

The function to save an image is `cv::imwrite(file_name, image)`. It
returns true if the file has been successfully written; false otherwise.
We can use the return value to handle possible errors:

```cxx
// Write the image
if (!cv::imwrite(output_filename, grey_image))
{
    // The image has not been written

    // Create an error message
    std::string error_message;
    error_message  = "Could not write the image \"";
    error_message += output_filename;
    error_message += "\".";

    // Throw an error
    throw error_message;
}
```

## 5. Find the smallest and largest pixel values in an image.

## 6. Improve the contrast of an image:
  - by hand using the equation seen in the lecture,
  - using OpenCV's function.

## 7. Change the dynamic range using a log transform.

## 8. Blend two images in a for loop to create an animation.


## Don't forget

To complete the lab report and to submit it.

## Next week

We will use spatial filters to blur an image, find edges, etc.
