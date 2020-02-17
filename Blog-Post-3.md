---
permalink: /Blog-Post-3.html
---

# Blog Post Week 3

## This Week's Work

### Progress on bias and flatfield correction

Bias correction for the entire dataset was already completed last week; for those results see Blog Post Week 2. Flatfielding, on the other hand, is not quite complete yet, however I am in a very good position. My module code to prepare each master flat is finished, as well as the code to perform the flatfield correction on science frames. Below is the python code in my module for each of these functions:

~~~ python
#
# norm combine flats: normalize each flat frame then median combine the set
#
def norm_combine_flats(filelist):
    '''
    Divide each individual pixel by the median pixel value to normalize the flats.
    All flats same exposure time!
    '''
    # Assign a variable to the length of the input filelist
    n = len(filelist)
    # Assign a variable to the data associated with the first file in the file list (index of 0)
    first_frame_data = fits.getdata(filelist[0])
    # finding the x and y dimensions of teh first_frame_data array
    imsize_y, imsize_x = first_frame_data.shape
    # creaing a zero array with dimensions y*x*n
    fits_stack = np.zeros((imsize_y, imsize_x , n))
    # Go through every file in the input filelist, get the data, then normalize each pixel in the flat
    for ii in range(0, n):
        im = fits.getdata(filelist[ii])
        norm_im = im/np.median(im.flatten()) # finish new line here to normalize flats
        fits_stack[:,:,ii] = norm_im
    # median combine the normalized flats
    med_frame = np.median(fits_stack, axis=2)
    return med_frame
#
# flatfield: perform flatfielding on a science frame
#
def flatfield(filename, path_to_masterflat, band):
    '''
    Takes a fits file path, a corresponding master flat file path, and a
    filter name and performs flatfielding on the fits file.
    '''
    # Load in data for a given file
    dat_load = fits.getdata(filename)
    # Read header for that file
    dat_header = fits.getheader(filename)
    # Load in data for master flat frame
    master_flat = fits.getdata(path_to_masterflat)
    # Divide master bias from an input FITS 'filename'
    sub_frame = dat_load / master_flat
    # Write results to file
    fits.writeto(str(band)+'_flat' + filename, sub_frame, dat_header, overwrite = True)
    return
~~~
For the most part, this is the same as the corresponding functions used in AST 337; since they were very adaptable, very little was changed. One correction was made where the norm_combine_flats function used the maximum value rather than the median to normalize each flatfield frame before median combining. To give some credit, my version of the AST 337 flatfield code was largely written by classmate Kenneth Lin as we shared code while completing that project.

After finalizing the code I went on to test it on some frames, then after being satisfied with those results, reduced each of the science frames for the first night of data. Here is an example, using the bias corrected vs. flatfielded versions of visual image 198 from night one:



### Roadblocks encountered thus far

## Revisit Science

### Summary of Boudrealt Paper

## Looking Ahead

### Next Data Analysis Steps
