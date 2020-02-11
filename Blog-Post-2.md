---
permalink: /Blog-Post-2.html
---
# Blog Post Week 2


## This Week's Work

### Bias Correction: What is it and why is it necessary?

There are numerous sources of error related to estimating the flux of a source. One of the major sources is bias: this is the voltage or "counts" that occurs between exposure and readout, i.e. over a very brief period. This will include sources such as cosmic rays, but for the most part consists of "readout noise" which takes the form of a constant added to each pixel, varying slightly with respect to position within the frame. Pixels closer to the readout location tend to receive lower bias voltage than those further away. Because this is a source of noise in each frame we wish to simply subtract it off. We do this by taking several zero second exposures, the bias frames, and median combine these frames to get a master bias, which is a good approximation to the map of bias values in each frame taken over the course of the night. To better this approximation, if the other frames taken during observing have an overscan, i.e. extra pixels where the readout noise is measured, then we multiply the master bias frame by an average overscan value divided by an average master bias value before subtracting off this so-called custom bias from the frame. By doing this we substantially lower the signal to noise of a source. See below for a science image pre- and post- bias subtraction, and an example of improvement of signal to noise.

### What does the code look like for the bias correction?

~~~ python
def bias_subtract(filename, path_to_bias):
    '''
    This function takes filename file (the bias frames) and subtract the custom bias.
    '''
    # Load in data for a given file
    dat_load = fits.getdata(filename)
    # Read header for that file
    dat_header = fits.getheader(filename)
    # Load in data for master bias frame
    master_bias = fits.getdata(path_to_bias)
    # Make custom bias: get median overscan and scale
    med_overscan = np.median(dat_load[os_1:, os_2:].flatten())
    med_bias     = np.median(master_bias.flatten())
    custom_bias  = master_bias[:os_1, :os_2]*med_overscan/med_bias
    # Subtract master bias from an input FITS 'filename'
    sub_frame = dat_load[:os_1, :os_2] - custom_bias
    #finish this code too to save the FITS. Make sure it has the correct header!
    fits.writeto('b_' + filename, sub_frame, dat_header, overwrite = True)
    return
~~~
This is the function in my module used to perform the bias subtraction on each frame. For the most part this is identical to the analogous function used in A337, with the difference under "Make custom bias" as here we compute the median overscan, median master bias value, and rescale the master bias by multiplying out the median overscan over the median master bias. This is essentially the same as outlined in my pseudo code for the class exercise.

### After applying the correction to an image, how does it appear?

Below is a raw science frame, image 137 from 2020/01/19, a visual band praesepe frame. The scale is zscale and represents the entire frame:

![before](137raw.png)

And we see the same image, also zscaled, after we perform bias subtraction:

![after](b_137.png)

As we would expect, the values seem to be approximately uniformly reduced. However, note the median sort of values of the background, i.e. the lowest bins given in the scaling: they land around ~50 ADU after bias correction, compared to ~3000 before. In contrast to this, a typical source we're interested in might have ~600 counts after versus ~3600 counts before; a marked improvement in signal to noise, despite a very rough measurement.


## Proposal Outline: feedback and goals

Last class (Feb. 5) we received feedback on research proposal outlines. Positive feedback for my outline included how concise it was, and that my plan for doing the research was well laid out. However, there were some key errors. The name for the project referenced YSOs in Praesepe, however considering its age Praesepe has nearly no YSOs; I had meant to refer to low mass stars or M dwarfs, but having a precise title is very important, so this is something I will need to check and modify. Another point where I can improve is explaining the "whys" of the research: the proposal outline was largely based on the brief prompt for the research I'll be doing, however my failure to look deeper into the questions related to why each part of the prompt was important left the reader wondering these questions. In other words, I should explain why I am only interested in VRI and not H alpha, why I'm interested in looking into mass-rotation relations, and what does it mean to look into these relations (what is my "money plot" with respect to this question)?

Thus, my goals for the proposal draft include the following:
* Rewrite the proposal in the proposal template form, filling out the boxes for abstract, justification, etc. rather than simply have a bulleted list.
* Show interest in the science! My justification should justify *why* we're interested in this research, and the feasibility should explain *why* each step in the process is important and why we are choosing these steps.
* Find more sources to back up my claims, and use figures from those sources for better visualization.
* Look into how certain quantities (i.e. mass) are estimated in relevant literature so I can explain how/why the VRI bands can be used to make this estimate.


## Papers found relevant to project

Boudreault, S. et al. “Brown Dwarfs and Very Low Mass Stars in the Praesepe Open Cluster: a Dynamically Unevolved Mass Function?” Astronomy and Astrophysics 510 (2010): A27. Crossref. Web.

This paper by Boudreault seems to be very relevant to my project, and should be useful for background information on the cluster and comparison of results. I used it in my proposal outline to quote the number of M dwarfs and BDs they detected however at some point I plan to read it in more detail so I can use the paper to check against other results I find in my work.
