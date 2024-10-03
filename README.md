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
   On the repository page, click the "more file actions" button. A dropdown menu will appear. In the dropdown, select "Download" This will download the macro file.

    <img src="https://github.com/ngmedina/NirVisAlign/blob/main/Download%20macro1.png" alt="ImageJscreenshot1" width="700"/>

### Step 2: Open the Macro Script in ImageJ/Fiji

1. **Open ImageJ/Fiji**  
   After downloading the repository, launch ImageJ or Fiji on your computer.

2. **Open the Script Editor**  
   In ImageJ/Fiji, go to `Plugins > New > Script...`. This will open the Script Editor.

3. **Load the Script**  
   Click on `File > Open...` in the Script Editor and navigate to the folder where you extracted the repository. Select the `.ijm` file (the macro script) and load it into the Script Editor.

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

- The macro uses the SIFT alignment method to align the NIR and VIS images. After alignment, the images are cropped and saved in the output folders.

### Step 6: Output

- Aligned NIR and VIS images are saved in the output folders with the `_AL` suffix to indicate they are aligned versions of the original files.

## Macro Script

```javascript
// -------------------------------------------------------------------
// Written by: Nagore García Medina
// Date: 2018-02
// Contact: nagore.garcia@uam.es
// -------------------------------------------------------------------

// v1.0: -Allow perfectly match between Near Infrared (NIR) and visible RGB images (VIS) for spectral image calculation.

// Select near infrared image input folder
inputNIR = getDirectory("./input_NIR_folder");

// Select visible image input folder
inputVIS = getDirectory("./input_VIS_folder");

// Select near infrared image output folder
outputNIR = getDirectory("./aligned_NIR_folder");

// Select visible image output folder
outputVIS = getDirectory("./aligned_VIS_folder");

Dialog.create("File type");
Dialog.addString("File suffix: ", ".tif", 5);
Dialog.show();
suffix = Dialog.getString();

processFolder(inputNIR);

function processFolder(inputNIR) {
    listNIR = getFileList(inputNIR);
    listVIS = getFileList(inputVIS);
    for (i = 0; i < listNIR.length; i++) {
        if(File.isDirectory(listNIR[i]))
            processFolder("" + inputNIR + listNIR[i]);
        if(endsWith(listNIR[i], suffix))
            processFile(inputNIR, outputNIR, listNIR[i]);
    }
}

function processFile(inputNIR, outputNIR, file) {
    fileVIS = listVIS[i];
    filename = replace(file, suffix, "");

    open(inputNIR + file);
    run("RGB Color");
    rename("NIR" + file);

    open(inputVIS + fileVIS);
    run("RGB Color");
    rename("VIS" + fileVIS);

    run("Concatenate...", "title=[Concatenated Stacks] image1=NIR" + file + " image2=[VIS" + fileVIS + "] image3=[-- None --]");
    run("Linear Stack Alignment with SIFT", "initial_gaussian_blur=1.60 steps_per_scale_octave=3 minimum_image_size=64 maximum_image_size=1024 feature_descriptor_size=4 feature_descriptor_orientation_bins=8 closest/next_closest_ratio=0.92 maximal_alignment_error=25 inlier_ratio=0.05 expected_transformation=Similarity interpolate");
    selectWindow("Aligned 2 of 2");
    makeRectangle(320, 96, 3808, 3320);

    run("Crop");
    run("Stack to Images");
    selectWindow("Aligned-0001");
    saveAs("Tiff", outputNIR + filename + "_AL");
    selectWindow("Aligned-0002");
    saveAs("Tiff", outputVIS + filename + "_AL");
    run("Close All");
}

