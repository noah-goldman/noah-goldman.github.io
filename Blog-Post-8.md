---
permalink: /Blog-Post-8.html
---
#Blog Post Week 8

## This Week's Work

### Light Curves of Matched Sources

## Reading

### Summary of "Evidence from stellar rotation for early disc dispersal owing to close companions"

In order to gain better understanding of the scientific basis for my project, I was assigned this paper by S. Messina. Based on the title and abstract they seem to discuss the observational effects on premature disruption of the disk by means of a binary companion or otherwise,

For otherwise similar G, K, M spectral type stars, the rotation rate dependence on mass varies at young ages, however at ~0.6 Gyr the distribution narrows into a roughly one to one correspondence. Phenomena that affect the rotation period for younger sources include disk locking and disk lifetime: for the latter, early disk dispersal can result in a higher rotation rate. Furthermore, a common source of early disk dispersal is the presence of a binary companion, thus the author's intent is to use a novel data set from the ~8 Myr Upper Sco. region to study how relationships between rotation period and binary parameters.

As a first the author discusses previous analysis done to select binary stars in Upper Sco. specifically Tokovinin & Briceño's 2018 paper, which found 70 relevant binaries by selecting sources with multiple periods. The subset used in this paper is then narrowed down to 49 sources as only M spectral types are relevant here. 

The next section is the longest of the paper, and is where the author goes into detail on how relation between mass and rotation rate for binaries is computed. This is best explained through Fig. 2 in the paper,

![Fig 2](fig2.png)

As described in the caption, individual and binary sources are plotted by period versus V-K colour, with primary and secondary binary sources singled out, and the whole relation fit with a linear regression. Colour index can often be used as a proxy for mass, which seems to be done here. The author then seeks to see how sources that are part of a binary component behave (with respect to how well they are period predicted by the fit relation) differently compared to individual sources and how different mass ratios correspond to different periods. A large portion of the analysis section is spent detailing how colour indices of each binary component are estimated, which is of course necessary for comparison but is omitted here for brevity. Next the main analysis is this: separate the data into bins for binaries with similar mass components (M1/M2>0.9) and more different mass components (0.8<M1/M2<0.9), then for each source compute the fit residual, i.e. the difference between the period computed through light curve periodograms and the period computed by matching the colour to the fit line. In the end, the author finds similar mass binaries have periods shorter than individual stars by ~0.4 days on average while those in different mass binaries have periods shorter by ~1-2 days. After this is computed the author additionally finds average differences of periods between the two sources in each binary, finding a difference of ~0.8 day for similar mass binaries and ~0.2 day for different mass binaries. Finally, the author compares disk fractions for individual and binary sources, and finds 28% for the former and 14% for the latter. 

Some questions I might have for the authors include the following:

* Based on other publications I've had the impression the disk-locking mechanism has some controversy surrounding it, yet the author here seems to take it as a given, is this the intention or does this issue have more consensus that I've been led to believe?
* How confident can we be that a periodogram with multiple peaks indicates a binary system rather than simply a more complex variability or even a factor of error (i.e. aliasing, inherent repeated signals, etc.)?
* While general trends agree with previous studies, both observational and theoretical, do the numerical results agree with those found previously for other regions, or with theoretical predictions?
* 

Considering how the paper largely concerns disk objects (specifically ~8 Myr) this paper sadly will not have much relevance to my project (concerning Praesepe, at ~650 Myr) other than the comment in the introduction about how the period-mass relation for late type stars stabilizes at this age. However if there are any binary sources in the field then there could be portions worth looking at, e.g. finding a similar mass-colour relation for older stars and seeing how well it predicts the binary's periods. 

