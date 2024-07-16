# imageStack

MATLAB class for handling (hyperdimensional) images.

## Documentation

The documentation for scripting can be called by typing in the MATLAB command line
```
doc imageStack
```

## Getting started

To load an image via the BioFormats reader into the imageStack class 'iStack', type 
```
iStack = imageStack.import('path/to/my/file.nd2')
```
Make sure the BioFormats package is in the MATLAB path and the 'bioformats_package.jar' is in the java path, see https://nl.mathworks.com/help/matlab/ref/javaaddpath.html. A list of the supported formats can be found here: https://docs.openmicroscopy.org/bio-formats/5.8.2/supported-formats.html and is not limited to .nd2 files.
The image is stored in an instance of the imageStack class in iStack.I. 

Alternatively, use the fast tiff loader for .tif and .tiff 3D image stacks
```
iStack = imageStack.importTifStack('path/to/my/file.tif',stackLabel);
```
with stackLabel the label of the 3rd dimension, which can either be 'z', 't', or 'c'. The first dimensions are assumed to be 'x' and 'y'.

A final option is to load an array directly in imageStack
```
iStack = imageStack();
iStack = iStack.addImage(I,'label1',...,'labelN');
% for example:
iStack = iStack.addImage(I,'x','y','c');
```
where I is the image array and the 'label1' ... 'labelN' the labels of the 1st ... Nth dimensions respectively. Allowed labels are: 'x','y','z','t','c'.

Now plot the stored image directly via 
```
figure; iStack.plotImage;
```

To get the image without dimensionality reduction, i.e. all dimensions in the image are requested, type
```
I = iStack.getReducedImage('reshaped','label1',...,'labelN');
% for example:
I = iStack.getReducedImage('reshaped','c','x','y');
```
following the same difinition as above. To request the image with fewer dimensions that present in data set, use e.g. 'mean' or 'sum' to take the average or sum of the reduced dimension
```
I = iStack.getReducedImage('mean','c','x','y');
```

## Project organization
- PG = project-generated
- HW = human-writable
- RO = read only
```
.
├── .gitignore
├── CITATION.md
├── LICENSE.md
├── README.md
├── requirements.txt
├── bin                <- Compiled and external code, ignored by git (PG)
│   └── external       <- Any external source code, ignored by git (RO)
├── config             <- Configuration files (HW)
├── data               <- All project data, ignored by git
│   ├── processed      <- The final, canonical data sets for modeling. (PG)
│   ├── raw            <- The original, immutable data dump. (RO)
│   └── temp           <- Intermediate data that has been transformed. (PG)
├── docs               <- Documentation notebook for users (HW)
│   ├── manuscript     <- Manuscript source, e.g., LaTeX, Markdown, etc. (HW)
│   └── reports        <- Other project reports and notebooks (e.g. Jupyter, .Rmd) (HW)
├── results
│   ├── figures        <- Figures for the manuscript or reports (PG)
│   └── output         <- Other output for the manuscript or reports (PG)
└── src                <- Source code for this project (HW)

```


## License

This project is licensed under the terms of the [GPL-3.0 License](/LICENSE.md)
