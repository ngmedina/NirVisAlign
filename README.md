# Image Alignment Macro for Spectral Image Calculation

## Description

This macro allows for the alignment of Near Infrared (NIR) and visible RGB (VIS) images, ensuring perfect matching for spectral image calculations. The script processes all images in the selected input folders and outputs aligned versions in the respective output folders.

**Author:** Nagore García Medina  
**Date:** February 2018  
**Contact:** nagore.garcia@uam.es
**Version:** v1.0

## Features

- Select input and output folders for both NIR and VIS images.
- Align images using the SIFT (Scale-Invariant Feature Transform) algorithm.
- Crop and save the aligned images.

## Requirements

- ImageJ/Fiji software.
- NIR and VIS images in `.tif` format.

## How to Use

### Step 1: Download the macro from the repository

1. **Go to the repository page in which the macro is saved**  
   [vignettes/vignette_ImageJ_preprocessing/Alignment_Process_Folder.ijm](https://github.com/MMolBus/PhotomossR/blob/master/vignettes/vignette_ImageJ_preprocessing/Alignment_Process_Folder.ijm)

2. **Download the macro**  
   On the repository page, click the "more file actions" button. A dropdown menu will appear. In the dropdown, select "Download" This will download the macro, a file with `.ijm` extension.

    <img src="https://github.com/ngmedina/NirVisAlign/blob/main/Download%20macro1.png" alt="ImageJscreenshot1" width="700"/>

### Step 2: Open the Macro Script in ImageJ/Fiji

1. **Open ImageJ/Fiji**  
   After downloading the macro, launch ImageJ or Fiji on your computer. If you do not have ImageJ or Fiji installed you can download it here https://imagej.net/software/fiji/

2. **Open the Script Editor**  
   In ImageJ/Fiji, go to `Plugins > New > Script...`. This will open the Script Editor.

3. **Load the Script**  
   Click on `File > Open...` in the Script Editor and navigate to the folder where you extracted the macro. Select the `Alignment_Process_Folder.ijm` file (the macro script) and load it into the Script Editor.

4. **Run the Macro**  
   Click `Run` in the Script Editor to execute the macro.

### Step 3: Select Input and Output Folders

- When the macro starts, it will prompt you to:
  - Select the folder containing the NIR images.
  - Select the folder containing the VIS images.
  - Specify the output folders for the aligned images.

### Step 4: File Suffix

- You will be asked to specify the suffix of the image files (e.g., `.tif`). The macro will process files with this suffix from the input folders.

### Step 5: Alignment Process

- The macro uses the SIFT alignment method to align the NIR and VIS images. If you want to know more about the method https://imagej.net/plugins/linear-stack-alignment-with-sift

### Step 6: Output

- Aligned NIR and VIS images are saved in the output folders with the `_AL` suffix to indicate they are aligned versions of the original files.
