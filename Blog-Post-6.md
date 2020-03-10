---
permalink: /Blog-Post-5.html
---
#Blog Post Week 6

## This Week's Work

### Reducing Remaining Nights' Data

My first draft of the full reduction process, with stacking, is now complete for all nights' data. I now have complete notebooks for sorting, bias correcting, flatfielding, aligning, and stacking the data for each night in the observing run. Updates since last week's status can be seen further down in the blog. Here I discuss some results from the final reduction. For each night, there were around 3-4 sequences of five images in V, R, I taken for Praesepe. Since I decided to stack based on sequence, this meant there are only 3-4 stacks from which to pull differential photometry per night. Given the data set however it seems this choice is optimal: deeper stacks will result in fewer light curve points while trying to pull out more stacks will result in lower signal to noise as well as the distance between light curve points would be less meaningful. 

There are some interesting (or concerning) features to some of the stacks. For example, many of the I stacks have "fringing" or alternating bright and dark bands that appear sometimes in near-infrared images due to some diffraction phenomenon. Below is an example of fringing in an I band stack from night 7:

![Istack](Istack.png)

The effect from fringing is clearly very faint, with a difference of ~20 ADU between peaks and troughs of the fringes, hardly noticible over the pixel to pixel variation already present in the image. In a project where higher SNR is required it might be worthwhile to take another step to remove the fringing, but for our purposes it shouldn't be necessary to do so. A more concerning phenomenon seen in the stacked images is a smearing of the stacks for the second night:

![Vstack](Vstack.png)

![Rstack](Rstack.png)

These are a V band stack and an R band stack respectively from night 2. Since this is present across bands and sequences, there's no single bad image that can be removed to fix the smearing. The aligning for these stacks also seems to be fine, light from the same sources seems to land on the same pixels. I may have to look for a fix for this if this causes trouble during the photometry step. For the moment, I will continue to look for a fix for this issue and check with other students to see if they also see the same issue.

### What is AstroImageJ and How Does it Work?

### Making a Light Curve with AstroImageJ

### Last Changes to Reduction Pipeline

### Comparison with Partner's Code
