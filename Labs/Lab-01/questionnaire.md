# ICE3111 -- Computer Vision -- Lab 1 -- questionnaire

(worth 5% of Assignment 1)

Deadline: 06/10/2021 at 23:59

- Your name:
- Your user ID:

## Identify some information from the window that displays the image

1. What is the image size in mm?
2. What is the image size in pixels?
3. What is the data type used to store pixels? in other words, you must specify:
    - greyscale vs. colour
    - integer vs. floating point numbers
        - if integer, signed or unsigned,
        - if floating point numbers, single or double precision
    - how many bits per pixels
4. What is the image size in number of bytes?
    - The total number of pixels is $\text{width in pixels} \times \text{height in pixels}$.
    - The number of values per pixel is 1 for greyscale images; 3 or 4 for colour images.
    - $\text{number of pixels} \times \text{bits per pixels} \times{number of values per pixel}/ 8 $
5. How many different pixels values an 8-bit image can have?
6. How many different pixels values DX000000 can have (in theory)?
7. What is the "size of a pixel in mm"? (divide the image size in mm by the image size in pixels)
8. What is the size in both mm and number of pixels of the diagonal of the image. Use Pythagoras' theorem:
    $\sqrt{width^2+height^2}$

## Measure distances

5. Before you release the mouse's button, look at the status bar and note the length of the line segment you just drew.
6. Is the distance given in mm or number of pixels? (compare with the lengths of the diagonal you computed with Pythagoras' theorem)
7. Using the same technique (drawing a line on the image to measure a distance), give the width and height of the object in the centre of the image. Provide the information both in mm and number of pixels.
