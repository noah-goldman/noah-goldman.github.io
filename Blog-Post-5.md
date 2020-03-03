---
permalink: /Blog-Post-5.html
---
# Blog Post Week 5

## This Week's Work

### Finalizing Reduction Code

I've settled on methods for bias subtraction, flatfielding, and aligning images. Bias and flatfield corrections have not changed since previous discussion on them, however I've been trying to improve on the way I align images. Below is currently my typical usage of the module for aligning data applied to the Praesepe data set:

~~~ python
rframes = glob.glob('*flatb*.fits')  # get reduced flat frames
for j in rframes:
    im, h          = fits.getdata(j, header=True)
    xshift, yshift = shift_methods.cross_image(pstack, im, xcen, ycen, 400)
    print(xshift, yshift)
    shifted        = shift_methods.shift_image(im, xshift, yshift)
    print('Writing shift_'+j+'.fits')
    fits.writeto('shift_'+j, shifted, h, overwrite=True)
~~~

There are some differences between here and last week's example, but the idea is the same. This piece of code is run for each night of data, stacking each image to 'pstack' which is the praesepe stacked image used in the in-class exercise. It prints out the x-shift and y-shift for each image to keep track in case this will be useful later. Shifting is performed and the result is saved to a file with its header copied.

Typical values for shifting were roughly -10 to -30 in xshift and -10 to -130 in yshift. While this does sometimes cut off a decent number of potential sources (I count around ~20 PSFs) it is necessary as many of the images are spaced very far from each other inherently. To reduce overall shifts, I first shifted the Praesepe stack image to one of the I-band images so there would be better alignment before shifting all images to the Praesepe stack.

I've played around a litle bit with stacking images myself, however I'm trying to hold out for the sigma clipping algorithm that we'll be using in the final version of the code. To summarize my current efforts, my method is simply to glob up the images I want to and use the mediancombine function on the group.

### Roadblocks Encountered and How They Were Solved

My code seemed to struggle with aligning V band images, initially generating frames filled with NaN values, but when I tried a second time it worked as expected. The strange part is that I didn't change anything, and additionally, there was no such problem for any of the R or I filter images, despite that the problem occured for V band images across all nights. I'll continue trying to look into why V band might be different and if my results really are what I expect or if there is some kind of underlying error that I'm not seeing but for the moment I believe what I have will do.

### How Many Stars in the Field?

## Back To Science

### More Paper Summaries

## Looking Ahead

### Next Data Analysis Steps

Once I get the 
