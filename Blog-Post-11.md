---
permalink: /Blog-Post-11.html
---
# Blog post: Week 11

## Worked on this Week

### Updating figures for the final poster

Reaching the final stages of the project, I'm finally getting around to deciding on values to use for period calculations. Tweaking things around on the flux measurement side of things, my final inputs for aperture and annulus size are 10 pixel aperture, 20 pixel inner radius and 40 pixel outer radius (or 10 pixel buffer and 20 pixel radius difference). A FWHM of four pixels and sigma detection threshold of 4 were selected for source detection. Doing this along with fixing a bug in light curve plotting improved my typical error bars from +/- 1 rel. flux to +/- 0.5 rel. flux. Some points still retained extremely high errors, typically night 2 and night 8 fluxes, which agrees with my previous discussion on quality in the photometry over the run, so these points were taken out of the computation for the later portion: periodogram analysis. The main change in the code I made here is that while at first I was distrusting of seeing periodogram peaks corresponding to periods of less than ~2 days, however having revisited the literature, periods this short are actually in line with what we might expect for our sample. Thus, I removed the limit forcing matched periods to be higher and reran the period computations, taking everything it would return. In the end, periods were able to be produced for 51 objects. The histogram of periods lies below:

![histogram](histogram.png)

With these I could match with my previous table matches from Vizier: the table from "The Factory and the Beehive: Activity and Rotation in Praesepe and the Hyades" (Douglas, 2014) containing mass estimates (among other quantities) and photometric data from 2MASS; as mentioned in a previous blog, both tables matches with our entire pre-matched source list. Then with periods, I could begin making plots of interest. Here's my plot of period versus mass, using the mass computations from Douglas, 2014:

![periodmass](periodmass.png)

And here's a plot of period versus J-K color from 2MASS data:

![periodcolor](periodcolor.png)

I'm currently in the process of checking with my partner on how he's prepared similar plots and whether we should go ahead and try to put these on the final presentation. 

### Notes on reading relevant science papers

One paper I've been meaning to get to for while is the one mentioned above talking about mass estimates: "The Factory and The Beehive" (Douglas, 2014). I've relied on this paper for several small things in previous blogs and assignments, however I've never really gotten around to actually going through it, so I figure now is as good a time as any, especially if I'm using their esimate for mass or other quantities in my final poster. Specifically what I want to get out of this is how they go about calculating quantities that might be useful here. 

### Notes on preparing for presentation
