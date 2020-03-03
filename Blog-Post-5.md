---
permalink: /Blog-Post-5.html
---
# Blog Post Week 5

## This Week's Work

### Finalizing Reduction Code

I've settled on methods for bias subtraction, flatfielding, and aligning images. Bias and flatfield corrections have not changed since previous discussion on them, however I've been trying to improve on the way I align images. Below is currently my typical usage of the module for aligning data applied to the Praesepe data set:

~~~ python
rframes = glob.glob('*flatb*.fits')  # get reduced science frames
for j in rframes:
    im, h          = fits.getdata(j, header=True)
    xshift, yshift = shift_methods.cross_image(pstack, im, xcenf, ycenf, 400)
    print(xshift, yshift)
    shifted        = shift_methods.shift_image(np.nan_to_num(im), xshift, yshift)
    print('Writing shift_'+j)
    fits.writeto('shift_'+j, shifted, h, overwrite=True)
~~~

There are some differences between here and last week's example, but the idea is the same. This piece of code is run for each night of data, stacking each image to 'pstack' which is the praesepe stacked image used in the in-class exercise. It prints out the x-shift and y-shift for each image to keep track in case this will be useful later. Shifting is performed and the result is saved to a file with its header copied.

Typical values for shifting were roughly -10 to -30 in xshift and -10 to -130 in yshift. While this does sometimes cut off a decent number of potential sources (I count around ~20 PSFs) it is necessary as many of the images are spaced very far from each other inherently. To reduce overall shifts, I first shifted the Praesepe stack image to one of the I-band images so there would be better alignment before shifting all images to the Praesepe stack.

I've played around a litle bit with stacking images myself, however I'm trying to hold out for the sigma clipping algorithm that we'll be using in the final version of the code. To summarize my current efforts, my method is simply to glob up the images I want to and use the mediancombine function on the group. The results aren't all that interesting to visualize since I couldn't glean anything from them that I couldn't already from the original reduced images.

### Roadblocks Encountered and How They Were Solved

My code has a strange consequence: when aligning the images, it seems to do 2/3 bands perfectly fine, however when treating the other band, usually V but in at least one case R, the returned shifted array is simply an all-NaN array. Trying all sorts of finding and removing NaNs and trying different shifts all resulted in naught. One strategy that did seem to work is to use the scipy interpolation module with spline order 0, this effectively removes the interpolation part of the algorithm and just does a shift; by doing this we solve the issue of the mysterious NaNs however instead we deal with the lack of interpolation. Whether this has significant negative effects in future analysis has yet to be determined. For the moment I am sticking with the order 0 shifting, but I will be working with Sarah on finding a proper solution.

### How Many Stars in the Field?

Playing around with the inputs for the star extraction algorithm gave around 300-900 sources found in the stacked image; matching to the online catalogue from the class exercise gave ~60-70 sources pretty consistently. Looking at the spectral classes for these objects I was relatively surprised: I was expecting almost entirely M1-10 sources, but these only contributed a small portion of the total population; G and K stars seemed just as common with F not far behind. Otherwise, there isn't much to see of the statistics at least initially, although proper motions and 2MASS ID (which could be used to pull out data) could potentially be very interesting.

## Back To Science

### More Paper Summaries

One interesting paper I've come across is Scholz' *The first rotation periods in Praesepe* (2007). The authors spend a lot of time discussing Praesepe and why it's an important locale to study rotation rates. It seems many of the papers I've encountered seem to be much more focused on Taurus and similarly young regions, and the information they present will be useful when discussing Praesepe and motivating the study of its stellar objects. This paper also discusses differences between rotation rates in Praesepe and the similar Hyades, which is analysis I would also like to do in my project, time permitting. Interestingly the co-author on this paper, Eislöfel, is one of the main authors on a 2018 paper covering low mass members of Hyades, so this should also be a good source.
 
Another interesting read is "K2 Rotation Periods for Low-mass Hyads and a Quantitative Comparison of the Distribution of Slow Rotators in the Hyades and Praesepe" by Douglas et al. (2019), which is well described by its title. It has some nice plots going into comparison between the clusters and also analysis on Gyrochronology, which is a topic I would like to explore in my project.

## Looking Ahead

### Next Data Analysis Steps

Once I solve the issue of NaNs and have the code for doing the stacking, there will be one main reduction step: actually performing the stacking. This is still uncertain to me as there are issues with how many frames should I be combining for each of my stacked images to perform photometry on, and I believe this will be covered in the next class. My first would be to combine each set of ~5 frames taken in each interval, for the ~4 intervals in each night to get as complete and accurate light curve as possible, but I will check before going full in on this. Once that is done, it'll finally be time to do differential photometry, which I also lack the information to do completely. Finally, once relative fluxes are assigned to each source, we can produce light curves by pulling out temporal information from the fits headers. 
