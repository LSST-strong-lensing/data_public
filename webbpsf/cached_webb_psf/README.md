# Cached PSFs from WebbPSF

When applying PSF convolution to images, using WebbPSF to generate PSFs is very time consuming. 
Thus, these files contain PSFs that have already been generated ahead of time so that they can be loaded, rather
than re-generated every time a PSF convolution needs to be done.

The file name format is {band}\_{detector}\_{detector_position[0]}\_{detector_position[1]}\_{oversample}.pkl

For now, only PSFs corresponding to the Roman bands F062, F106, F129, and F184 and detector position (2000, 2000) with oversample = 5 (and also oversample = 3 only for F062) have been generated, for the 18 Roman WFI detectors. They were generated on 8/21/2024, using webbpsf v1.3.0. A notebook which can be used to generate more PSFs is included.

Note that these pickle files were written in binary mode, so to access the PSF kernels stored within, they must be opened in binary mode.
