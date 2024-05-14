# HI Lya Emission From a Metal-Poor Cool Stream Fueling an Early Dusty Starburst

This repository provides the customized Python notebooks used to perform the analysis in the *Astrophysical Journal*: [HI Lya Emission From a Metal-Poor Cool Stream Fueling an Early Dusty Starburst](https://ui.adsabs.harvard.edu/abs/2024arXiv240500795H/abstract)

We provide both the final data products, as well as a breakdown of each analysis stage. 

## Stages of kcwi datacube analysis for the G0913 system

The ipynb notebooks uploaded to this drive will save various outputs to specific directories
You may need to change where they are saved locally. This guide will state the order of events during the analysis.

*Quick Note*: These notebooks can all be placed into one master notebook if the user prefers.

0. Setup directory
    - Create 'drp' directory
    - Create 'trimcube' directory
    - Create 'psfsub' directory
    - Create 'psfcontsub' directory
    - Create 'Coadds' directory

1. Run kcwidrp
    - produce icubes.fits and vcubes.fits
    - We have provided our icubes.fits and vcubes.fits within the 'drp' folder. Simply move those files into your drp folder

2. Trim datacubes
    - Run notebook: trim_kcwi_datacube.ipynb
    - Removes Edges from each icubes and vcubes
    - Trims wavelength axis 
    - Once we trim each datacube, we correct the WCS info for each fits file
    - Correct WCS with: correctWCS.ipynb
    - output is saved to: 'trimcube/' dir
    - Each trimmed fits file has '_tr_' appended to filename
    
3. Subtract Quasars
    - run notebook: subtract_qso.ipynb
    - Notebook subtracts QSO1 and QSO2 from the datacubes (south)
    - Wavelengths within +/- 2000 km/s window excluded from PSF model wrt to each target (SMG,QSO1,QSO2). The velocity width can be modified easily. 
    - Notebook disables QSO subtraction at user specified index values from kcwi datacube where absorption is present, which we provide (but can be removed)
    - output is saved to: 'psfsub/' directory.
    - Each fits file with qso subtraction has '_psfsub_' appended to filename
    
4. Subtract Continuum
    - run notebook: subtract_continuum.ipynb
    - function creates a median filter along the wavelength axis
    - The median filter acts as a narrowband image that is then subtracted from the datacube
    - Notebook has the width of the filter set to 150 AA, or 300 layers (index)
    - output is saved to: 'psfcontsub/' directory
    - Each fits file with both QSO/continuum subtraction has '_psfcontsub_' appended to filename
    
5. Coadd
    - run notebook: coadd_cubes.ipynb
    - notebook performs a coadd for datacubes within stages: 2, 3, and 4
    - Each coadd reads a list file that controls which datacubes will be coadded
    - These list files are in the coadds/ dir within this Onedrive
    - These stages are denoted in the corresponding cells. Allows comparisons between each stage
    - To perform a coadd, user must have the modified cwitools cubes.py file. We have provided this .py file within this repo
    - Please refer to [the repository for cwitools](https://github.com/dbosul/cwitools/tree/v0.8/cwitools) for the full cwitools python package. 
    - The parameters for the coadd are already set
    - output will have a 0.7" x 0.7" pixel size
    - all output are saved to the 'coadds/' directory
    
6. Optimal Extraction
    - run notebook: extract_flux.ipynb
    - Generates a 3D mask
    - Saves 3D mask to 'optextract/' dir
    - Presents a quick 2D look at the 3D mask
    
7. Generate Moment Maps
    - run notebook: create_sbmaps.ipynb
    - generates surface brightness maps, velocity, and dispersion maps for SMG, QSO1, QSO2
    
    
    
    
    
    
