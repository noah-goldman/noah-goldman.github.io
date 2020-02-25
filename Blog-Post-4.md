---
permalink: /Blog-Post-4.html
---
# Blog Post Week 4

## This Week's Work

### Bias Subtraction and Flatfielding Progress

Bias and flatfield corrections have been performed on all Praesepe VRI frames we'll be using from the larger data set. Using the algorithm described last class this was no challenge. The last step is to verify the correction was effective. To this end, I've been in touch with my project partner Johari to exchange data and methods files in order to compare results; if we both did the corrections identically the same, this would be a good indication the method we used was correct. Alternatively, if there is a difference then likely one of us made a mistake and we could discuss which one of us made the mistake and work to correct it. This has not yet been done, but I look to do it within the next week.

### Shifting and Aligning Images and shift_methods.py

Shifting has begun! Thus far I have done shifting to align a set of five I-band images from the first night of data to the first image in that set. The code for this process is as follows:

~~~ python
import numpy as np
from astropy.io import fits
import a341mod
import os
import shift_methods
import matplotlib.pyplot as plt
#
I_1  = ['I_flatb_c8867t0145o00.fits', 'I_flatb_c8867t0146o00.fits', 'I_flatb_c8867t0147o00.fits', 'I_flatb_c8867t0148o00.fits', 'I_flatb_c8867t0149o00.fits']
im_1 = fits.getdata(I_1[0])
plt.imshow(im_1[2420:2470, 2350:2390], vmin=50, vmax=800)  # centre at (2450, 2380) is a pretty good guess
xcen, ycen = 2450, 2380
xcenf, ycenf = shift_methods.centroid(im_1, ycen, xcen)
xcenf, ycenf = int(xcenf), int(ycenf)
for i in I_1:
    im_2 = fits.getdata(i)
    xshift, yshift = shift_methods.cross_image(im_1, im_2, xcen, ycen, 400)
    a              = shift_methods.shift_image(im_2, xshift, yshift)
    fits.writeto('shift_'+i, a, overwrite=True)
~~~

After importing necessary packages, I put the names of files I want to shift into a list of strings. While doing it manually like this is not ideal for when I'm working with all the data, this was just to test the algorithm and when I work out a better way to do this, the line defining I_1 will change. Next I take a look at the first image within that set, in order to get the position of a star with a good PSF. After some shifting around I came across a bright source near the centre of the image, and decided to use this for the input in the centroid and cross_image functions. Having this guess of the source's centre point I improve this by using the centroid algorithm from shift_methods, and turning its output into an integer. With this I have everything to do the shifting: begin a loop through the files, take out the next image data, call the cross_image function to find the shifts, then use these shifts in the shift_image function, and write the result to file. Doing all this after fixing bugs resulted in the following:

![shifting](3q8wky.gif)
Fig. 1: GIF showing the same region at the same scale of the aligned I-band images. While some shift is noticible for a couple of the frames, this is actually do to missing certain pixels while screenshotting and not actual shift between the images.

These results show my implementation is effective at generating images aligned to the first in the set. Several questions, however, remain open: which image (if any) should be picked as the reference? How can I automate selection of files to align to each other, and related, how do I determine how many files I need in a stack to get good photometry? Some of these questions seem to be answered in class, while others I will need to debug myself.

How do the functions in shift_methods.py work? There are three said functions: centroid(data_arr, xcen, ycen, nhalf=5, derivshift=1.), cross_image(im1, im2, centerx, centery, boxsize=400), and shift_image(image, xshift, yshift). The centroid returns the centre of a PSF: starting out with a data array and a centre guess, it cuts out a square of the array, nhalf above, below, left, and right of the centre guess. After some normalizing corrections it uses some weighting functions and factors to make estimates of, first the X then the Y derivative everywhere. From there it makes essentially an estimate of where '0' derivative is, and takes this to be the centroid. 

The cross_image function performs convolution between two arrays to find their relative shift. It begins by cutting out a square of side length twice boxsize, centred on the input centre. From there it subtracts off mean values from the arrays, takes out NANs, then finally performs the convolution. The maximum value of the convolution is a good estimate of the necessary shift, however this algorithm goes one step further by using the shift estimate as an input to the centroiding algorithm to improve the estimate of where the maximum is. The result from this centroiding is converted into a shift, and then is returned as the function output.

Finally, the shift_image function is very simple. It takes the image array and the shifts, which CAN be floats, and uses a scipy interpolation function to shift the image based on the inputs.

Based on reading this, I combined the three as outlined above: make a centre pixel guess, improve this with the centroiding, then use this as an input for cross correlation, finally taking the cross correlation output as the input for the shifts in the shift function. I am thus far satisfied with the results, although there are still outlying issues as noted above.

### Roadblocks Encountered and Their Solutions

One issue I encountered while attempting to shift images is that I had assumed the methods were meant to be used in the following way: make an initial guess for the central position of a star, do centroiding on this to correct this guess, then feed this position into the cross_image function to find the shifts. However, I was confused by earlier discussion on using integers versus floats in the shifting algorithm, and thought that meant cross_image could handle non-integer values. This turned out to not be true and it DOES require integer values, meaning I ran into many errors without understanding their source. Eventually I discovered my problem and fixed it by rounding the centroid's output to an integer before feeding it into the cross_image. I also had an issue where I was flipping my x and y coordinates, and did a quick fix by switching around variable names in the right places.

### Next Data Analysis Steps

Once my algorithm for implementing the functions in shift_methods is complete, I will need to learn about and implement sigma clipping in order to make stacked images from the shifted images. Then, having a method to fully reduce my images I will need a way to choose which sets of images to perform the stacking on to get the light curves I want. From there it's onto differential photometry and producing light curves!

## Back to Science

### Next Steps in Proposal Writing

I am pretty satisfied with my draft for the proposal, however there are several places that need work. First of all, the abstract is not completed, as it is lacking several important points I make in the science justification, which should be mentioned if only briefly. Additionally, the technical justification suffers from being incomplete; part of this is due to that several steps in the image reduction and processing of light curves have not been covered in class. Even so, with my current knowledge I could definitely expand on how I plan to create light curves, reduce the data, and what form the results should be in. When I get feedback on the proposal I can better evaluate what needs to be worked on, but for now I'd say fleshing out the technical justification is most important. Some claims in the science justification could also use more citations. And to make one last comment, I am trying to work with Johari on exchanging ideas to cover on the science justification and project goals in order to be a little more coordinated.

### Differential Photometry

Differential photometry is a technique used to measure differences in star brightness over a set of observations, as opposed to calibrated photometry used in 337, which focuses on measuring the calibrated magnitude of a set of stars, either for a single magnitude measurement or for several. If we wished to use isochrones or other comparisons to find out intrinsic characteristics about our stars, then differential photometry would not be helpful since differential photometry *only* measures differences from one night to another or some other time period, however we do have the benefit of not having to calibrate our magnitudes to a standard star. Additionally, several characteristics remain unchanged, for example we can compute a star's V-R colour index and it would turn out to be the same as using calibrated photometry as this is only dependent on the difference of instrumental magnitudes.

Computing magnitudes with differential photometry isn't 100% straightforward however: simply taking differences between instrumental magnitudes will not give us the results we want as several other factors can change the apparent brightness of a source other than real variations in absolute magnitude. For example, the sky may change brightness from night to night, which will factor in a similar brightness change in our magnitude measurements. To account for these, we employ a technique called *ensemble photometry*, which postulates that by measuring the variations of a group of stars, we can compute an estimate of *em(s)*, or the exposure magnitude, which is essentially a collection of magnitude measurements to try and approximate the night-to-night variations of the sky or exposure. By subtracting off this exposure magnitude from each stellar instrumental magnitude we can produce plots of night-to-night variation of *the star itself* rather than the combined variation of the star and the sky and other factors.
