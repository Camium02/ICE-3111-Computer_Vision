---
title: Lab 1 -- Examples of Image Analysis Using ImageJ/Fiji.
author: Dr Franck P. Vidal
subtitle: ICE-3111 Computer Vision 202122
date: Sept 22th, 2021
keywords: ICE3111, Computer Vision, C/C++, python, image processing, OpenCV, Bangor University, School of Computer Science and Electronic Engineering
institute: School of Computer Science and Electronic Engineering, Bangor University
---

# Introduction

The purpose of this lab is to introduce you to the use of ImageJ2 ![(logo)](../Lab-00/icons/imagej.png). In practice, we will use Fiji ![(logo)](../Lab-00/icons/fiji.png). Fiji is an image processing package, a "batteries-included" distribution of ImageJ2, bundling a lot of plugins which facilitate scientific image analysis.

# Preliminaries

    Is it installed?

The first thing to do is check if ![Fiji](../Lab-00/icons/fiji.png) is installed. Make sure it is on the lab machine and your home computer/laptop. Installing ![Fiji](../Lab-00/icons/fiji.png) is trivial. Just download the archive corresponding to your operating system, and extract it somewhere in your home directory. You'll find the program at https://imagej.net/Fiji/Downloads](https://imagej.net/Fiji/Downloads) or below:

- [![https://downloads.imagej.net/fiji/latest/fiji-win64.zip](../Lab-00/icons/windows.png)](https://downloads.imagej.net/fiji/latest/fiji-win64.zip)
- [![https://downloads.imagej.net/fiji/latest/fiji-macosx.zip](../Lab-00/icons/macos.png)](https://downloads.imagej.net/fiji/latest/fiji-macosx.zip)
- [![https://downloads.imagej.net/fiji/latest/fiji-linux64.zip](../Lab-00/icons/linux.png)](https://downloads.imagej.net/fiji/latest/fiji-linux64.zip)

# Launch ![Fiji](../Lab-00/icons/fiji.png)

Identify the executable file and double-click on:

- ![For Windows](../Lab-00/icons/windows.png): look for `ImageJ-win64.exe` in `path_where_you_extracted_the_archive/Fiji.app/`
- ![For MacOS](../Lab-00/icons/macos.png): look for `Fiji.app` in `path_where_you_extracted_the_archive`
- ![For GNU/Linux](../Lab-00/icons/linux.png): look for `ImageJ-linux64` in `path_where_you_extracted_the_archive/Fiji.app/`

# Main window and menus

First, you must get familiar with the user interface.

## Main windows

![Screenshot](main-window.png)

It will appear on your screen. Do not resize it! This window has a Menu Bar, a Tool Bar (all the icons you can see) and a Status Bar (it will display some information when you move the cursor over an image).

## File menu

![Screenshot](file-menu.png)

I mostly use this menu to:

- open existing files
    - from the disk or
    - from ImageJ test image database,
- import RAW files in binary or ASCII,
- import a sequence of 2D images, and
- save images.

## Edit menu

![Screenshot](edit-menu.png)

I am sure you are already familiar with the `undo` functionality of a text editor. It's the same, but for an image editor. `Cut`, `Copy` and `Paste` are local to ImageJ. If you want to copy an image, or part of it, and paste it into let's say Word, you must use `Copy to System`.

I do not use other options very much, although they are sometimes useful to clear an area of the image or inverse its values.

## Image menu

![Screenshot](image-menu.png)

I use it ALL THE TIME. `Type` is used to change the data type used to store a pixel (8 bits, 16 bits or 32 bits, and greyscale or RGB). `Adjust` is used to control various values. `Brightness/Contrast` and `Threshold` are particularly useful.

To show a greyscale image in colour, `Lookup Tables` is used.
Other useful options are `Crop`, `Scale`, and `Transform`.

## Process menu

![Screenshot](process-menu.png)

I use it ALL THE TIME. It is used to process the image, e.g. applying mathematical functions to images, or applying image filters.

## Analyse menu

![Screenshot](analyse-menu.png)

I use it ALL THE TIME to compute image statistics (min, max, average... pixel values), and compute histograms.

## Plugins

![Screenshot](plugins-menu.png)

All the plugins. There are too many to describe them here.

## Window

![Screenshot](windons-menu.png)

I use it to find a window I "lost".

## Help

![Screenshot](help-menu.png)

I don't use it so much.

# Find the size of a PMMA block in an X-ray image

The image file is stored in the DICOM format. This is the format used to store most medical images. It's the JPEG format for medicine.

1. Download [DX000000](DX000000).
2. Open `DX000000` via `File → Open`.
3. Identify some information from the window that displays the image (look at the status bar at the top of that window):
    - What is the image size in mm?
    - What is the image size in pixels?
    - What is the data type used to store pixels?
    - How many different pixels values an 8-bit image can have?
    - How many different pixels values DX000000 can have in theory?
    - What is the "size of a pixel"? (divide the image size in mm by the image size in pixels)
