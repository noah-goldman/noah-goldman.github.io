---
permalink: /Blog-Post-9.html
---
#Blog Post Week 9

## This Week's Work

### Updated Lightcurves: Python Photometry

This week I used the code in the class exercise on light curve generation as a base for plotting light curves over all targets, bands, using the stacked images prepared earlier (as described in previous blog posts). Here is an example of the code I used to do differential photometry on the R band images:

~~~ python
im                        = glob.glob('RSequence/*.fits')  # get red images
times, Photometry_initial = doPhotometry(im, xpos, ypos, aprad, skybuff, skywidth, timekey='MJD-OBS')  # aperture phot.
ePhotometry               = doPhotometryError(im,xpos, ypos, aprad, skybuff, skywidth, Photometry_initial, manual=True, xboxcorner=2000, yboxcorner=2000, boxsize=200)  # and error
Photometry, cPhotometry   = detrend(Photometry_initial, ePhotometry, nstars)  # detrend
most_accurate             = findComparisonStars(Photometry, cPhotometry, comp_num=12)  # find our comparisons
dPhotometry, edPhotometry, tePhotometry  = runDifferentialPhotometry(Photometry, ePhotometry, nstars, most_accurate)  # diff photometry
diffPhot_IndividualStars(datadir, memberlist, ra, dec, xpos, ypos, dPhotometry, edPhotometry, tePhotometry,times, 'Praesepe_1_R', wcs_image, most_accurate)  # photometry for targets
~~~

Note this is missing certain steps necessary for differential photometry: most notably source detections. This step was only done on the V band images for consistency; the source list and aperture placements were stored from the iteration for V band sources and reused in the R and I band images. Few significant choices of my own are made in this code, however there is one important one: the number of comparison stars, comp_num, located in line 6. I'll come back to this in my discussion on variation seen in these sources. In order to generate and save light curve plots from these data I use the following code, which saves a PDF containing the light curves:
~~~ python
with PdfPages('Praesepe_1_R.pdf') as pdf:
    for i in range(16):
        fig = plt.figure(num=1, figsize=(16, 16))
        fig.suptitle('Praesepe Targets R Band')
        fig.text(0.5, 0.04, 'Time (Days Since Beginning Observation)', ha='center')
        fig.text(0.04, 0.5, 'Rel. Flux', va='center', rotation='vertical')
        for j in range(4):
            plt.subplot(2, 2, j+1)
            plt.errorbar(dataR['time'], dataR['flux'][:, i*j], yerr=dataR['flux'][:, i*j], fmt='go')
        pdf.savefig()
        plt.close()
~~~
These piece of code was used to make a PDF for each band's light curves, and additionally a PDF for light curves containing all three bands simultaneously.

<embed src="https://noah-goldman.github.io/Praesepe_1_V.pdf" type="application/pdf" />

These are the light curves from the V photometry. I will be using this file to reference individual light curves in my below analysis.

### Interpretation of Light Curves

#### What kinds of variation are present?



#### How can we interpret variations in different bands?

### Periodogram Analysis

Now having light curves I can begin on the crucial part of the analysis: computation of rotation periods. As described previously, I'll be doing this using the Lomb-Scargle Periodogram on the light curve data. In class we did an exercise calculating such a periodogram for some sample data; below is the code from that activity adapted to a single V band light curve from my sample:
~~~ python
f, p = LombScargle(dataV['time'], dataV['flux'][:, 5], dataV['fluxerr'][:, 5]).autopower()
plt.plot(1/f*24, p, color='m')
plt.xlabel('Period [Hours]')
plt.ylabel('Power')
plt.xlim(0, 200)
~~~
This code has one major flaw: it cannot deal with nan values as whenever it encounters one (of which there are many) in the flux array, the entire power array is returned as zeros. Furthermore, the structure of the data file makes reassigning nans or avoiding them in the LS computation very difficult. In light of this, I only have to offer a single periodogram where there were no nans:

![periodogram](periodogram.png)

The periodogram itself doesn't seem to indicate a particularly strong periodic signal, particularly one that would indicate rotation. The periods we are looking for are on the order of the length of observations, or close to 200 hours. Instead, the peak is near 16 hours and the next at an even smaller period. The best possible rotation period seems to be the peak near 125 hours. I plotted its phase diagram:

![phase](phase.png)

There doesn't seem to be any indication of a (rotation induced) period here, so the likely explanations include that there is a flaw somewhere in my method, or that this source simply doesn't show rotations on the scale we're interested in. The next thing to do would be to compare this to the light curve, and also to do a periodogram for a source I am more convinced has rotation induced variability.

### Updated Table Matching
