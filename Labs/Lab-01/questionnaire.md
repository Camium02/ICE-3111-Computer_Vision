# ICE3111 -- Computer Vision -- Lab 1 -- questionnaire

(worth 5% of Assignment 1)

Deadline: 06/10/2021 at 23:59

- Your name:
- Your user ID:

**Note:** the numbers below correspond to the numbers in the lab script:

## Identify some information from the  status bar

1. What is the image size in mm? \_\_\_\_\_\_\_\_\_\_\_\_\_
2. What is the image size in pixels?\_\_\_\_\_\_\_\_\_\_\_\_\_
3. What is the data type used to store pixels?     \_\_\_\_\_\_\_\_\_\_\_\_\_
4. What is the image size in number of bytes? \_\_\_\_\_\_\_\_\_\_\_\_\_
5. How many different pixels values an 8-bit image can have? \_\_\_\_\_\_\_\_\_\_\_\_\_
6. How many different pixels values DX000000 can have (in theory)? \_\_\_\_\_\_\_\_\_\_\_\_\_
7. What is the "size of a pixel in mm"? \_\_\_\_\_\_\_\_\_\_\_\_\_
8. What is the size in both mm and number of pixels of the diagonal of the image.
    - In mm: \_\_\_\_\_\_\_\_\_\_\_\_\_
    - In pixels: \_\_\_\_\_\_\_\_\_\_\_\_\_

## Measure distances

1. Move the cursor over the image. Keep an eye on the status bar of ImageJ's main window. Describe in your own words what is happening.
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

5. Before you release the mouse's button, look at the status bar and note the length of the line segment you just drew.

\_\_\_\_\_\_\_\_\_\_\_\_\_

6. Is the distance given in mm or number of pixels? (compare with the lengths of the diagonal you computed with Pythagoras' theorem)

\_\_\_\_\_\_\_\_\_\_\_\_\_

7. Using the same technique (drawing a line on the image to measure a distance), give the width and height of the object in the centre of the image. Provide the information both in mm and number of pixels.

## Statistical analysis

### Overall image

1. What is the smallest pixel value in the image? \_\_\_\_\_\_\_\_\_\_\_\_\_
2. What is the largest pixel value in the image? \_\_\_\_\_\_\_\_\_\_\_\_\_
3. What is the average pixel value in the image? \_\_\_\_\_\_\_\_\_\_\_\_\_
4. What is the standard deviation? \_\_\_\_\_\_\_\_\_\_\_\_\_
5. What is the dynamic range? \_\_\_\_\_\_\_\_\_\_\_\_\_
6. The intensity histogram is a graph that shows the number of pixels in an image at each different intensity value found in that image. Insert the intensity histogram below:



### PMMA block

1. What is the smallest pixel value in the part of the image corresponding to the PMMA block? \_\_\_\_\_\_\_\_\_\_\_\_\_
2. What is the largest pixel value in the part of the image corresponding to the PMMA block? \_\_\_\_\_\_\_\_\_\_\_\_\_
3. What is the average pixel value in the part of the image corresponding to the PMMA block? \_\_\_\_\_\_\_\_\_\_\_\_\_
4. What is the standard deviation? \_\_\_\_\_\_\_\_\_\_\_\_\_
5. What is the range of pixel values in this region of the image? \_\_\_\_\_\_\_\_\_\_\_\_\_
6. Insert the corresponding histogram below:


### Background

1. What is the smallest pixel value in the part of the image corresponding to the background? \_\_\_\_\_\_\_\_\_\_\_\_\_
2. What is the largest pixel value in the part of the image corresponding to the background? \_\_\_\_\_\_\_\_\_\_\_\_\_
3. What is the average pixel value in the part of the image corresponding to the background? \_\_\_\_\_\_\_\_\_\_\_\_\_
4. What is the standard deviation? \_\_\_\_\_\_\_\_\_\_\_\_\_
5. What is the range of pixel values in this region of the image? \_\_\_\_\_\_\_\_\_\_\_\_\_
6. Insert the corresponding histogram below:


### Compare the 3 histograms

You can move the mouse over the histograms to see more information. We are trying to locate the pixel intensity that separate the PMMA block from the background. See the red arrow pointing to the middle of the valley between the two peaks below:

![Screenshot of the image histogram](images/imagej-histograms-valley.png)

What is the corresponding pixel intensity? \_\_\_\_\_\_\_\_\_\_\_\_\_
