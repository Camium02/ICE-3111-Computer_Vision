---
title: Lab 3 -- Introduction to OpenCV in C/C++ and Python, and Point Operators.
author: Dr Franck P. Vidal
subtitle: ICE-3111 Computer Vision
date: Week 3
keywords: ICE3111, Computer Vision, C/C++, python, image processing, OpenCV, Bangor University, School of Computer Science and Electronic Engineering
institute: School of Computer Science and Electronic Engineering, Bangor University
---

# Instructions in Python

## Contents

[2. Load an image](#2-and-3-load-and-display-an-image)
3. [Display an image](#2-and-3-load-and-display-an-image)
4. [Convert a RGB image in a greyscale image](#4-convert-a-rgb-image-in-a-greyscale-image)
5. [Find the smallest and largest pixel values in an image](#5-find-the-smallest-and-largest-pixel-values-in-an-image)
6. [Improve the contrast of an image:](#6-improve-the-contrast-of-an-image)
    1. [by hand using the equation seen in the lecture](#by-hand-using-the-equation-seen-in-the-lecture)
    2. [using OpenCV's function](#using-opencvs-function)
7. [Change the dynamic range using a log transform](#7-change-the-dynamic-range-using-a-log-transform)
8. [Blend two images in a for loop to create an animation](#8-blend-two-images-in-a-for-loop-to-create-an-animation)

## 2. and 3. Load and display an image

Before we start, the technical documentation is available at: [https://docs.opencv.org/4.5.4/index.html](https://docs.opencv.org/4.5.4/index.html). The OpenCV's functions we will use are:

```cpp
imread() // To read an image from a file
imshow() // To display an image in a window
```
Both functions are available in C, C++ and Python. Find them in the online documentation and read the corresponding text. I often consult the documentation when I forget the name of a function or when I need to find the right sequence of parameters. This is what I get:

```Python
cv.imread( filename[, flags] ) -> 	retval

cv.imshow( winname, mat ) -> 	None
```

### Our first OpenCV program

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

1. Copy paste your previous program in a new one that you call `rgb2grey.py`.

2. The command line is:

```bash
rgb2grey.py  input_filename  output_filename
```

Change the code appropriately.

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

Make sure you change the `2` into `3`, and that you retreive filename of the output image (`argv[2]`).
In future, I may not provide the same level of guidance for this task as I will assume it is something you know now.

3. After you read the image and checked that the image was loaded, and before displaying the image, convert it into a greyscale image:

```python
grey_image = cv2.cvtColor(image, cv2.COLOR_RGB2GRAY)
```

4. Don't forget to display the right image, i.e. `grey_image` not `image`. `imshow` will take care of the change of pixel type (RGB->greyscale).

5. Save the image

The function to save an image is `cv2.imwrite(file_name, image)`. It
returns true if the file has been successfully written; false otherwise.
We can use the return value to handle possible errors:

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

When you detect an error, it is good practive to throw an error. Again, I will assume from now on that you know how to do it.

The program is now complete. You run it with different image files to test it. In your lab report, you must include a listing of your program and put three screenshots (with three different images).


## 5. Find the smallest and largest pixel values in an image.

## 6. Improve the contrast of an image

### by hand using the equation seen in the lecture

### using OpenCV's function

## 7. Change the dynamic range using a log transform.

## 8. Blend two images in a for loop to create an animation.


## Don't forget

To complete the lab report and to submit it.

## Next week

We will use spatial filters to blur an image, find edges, etc.
