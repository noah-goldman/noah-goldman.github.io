---
permalink: /Blog-Post-1.html
---
# AST 341 Blog Post, Week 1

## Summary of the Past Week

We had an early start to the semester with a brief trip to Arizona beginning on January 17th in order to do observing at the 0.9 meter WIYN
telescope at Kitt Peak National Observatory. After four nights of observing, two successful and two rain-outs, we returned to Massachusetts
to begin the semester. After two weeks of classes, school is again in full swing. This means making the first steps towards performing research
using the data collected from WIYN.

### Prompts

#### What lessons did you learn about observing during the trip?

We learned how to operate the telescope: controlling the telescope and dome position, set up the telescope for dome flats or sky observing, putting away
the telescope come morning, etc. We also learned about doing the actual observations on astronomical targets: how long a target might stay near zenith,
switching between filters and wheels, taking images and viewing tables of their output. Personally, it was interesting to learn about the human aspect
of observing: what to expect in terms of sleep and food, whether there is usually a restroom in the observatory (there is), how to pass the time on a rainy
night, etc. It was also nice to see what observing is like for some of the world-class projects undertaken at KPNO, such as DESI and NEID.

#### As a student, what was your role during the observing run?

My role (no different from any of the any other students participating in this trip) was to learn as much as possible about the operation of
astronomical observatories while also gaining experience operating the 0.9 meter telescope. Considering the answer to the above question, it seems I was successful in these. 

#### What important information did you learn about HDI and the data we took?

HDI (Half Degree Imager) is the CCD used to make astronomical observations on the WIYN 0.9 meter. It covers (nearly) half of a degree of sky in each direction in each image. The commands for taking images with the HDI we ran on Emerald were written for HDI specifically (in Perl if memory serves). We took around 300 images for each (observing) night, each of which corresponding to a fits file, and this data has by now been uploaded for 341 students to download and use.

#### What steps will you need to perform to reduce your data? What software will you need/use?

For each of the data files, I will need to perform the standard reduction operations: prepare master bias files, prepare master flatfields in each band
for each night, bias subtract then flat normalize each science frame for my cluster, and finally shift and stack the reduced images. This can
all be done in python applying a variation of the reduction pipeline from last semester (AST 337), however I will need to be able to transfer the files for which I will need to get a portable storage device, and DS9 will be useful
for doing checks on each of the steps.

#### Go through logs and identify the data files (science AND calibrations) you’ll need for your project

Night | Bias | Flats | V | R | I
------|------|-------|---|---|---
Jan. 18 | 1-13 | 15-27, 29-30 | 135-139, 156-160, 177-181, 198-202 | 140-144, 161-165, 182-186, 203-207 | 145-149, 166-170, 187-191, 208-212
Jan. 19 | 235-245 | 246-250, 252-255, 2-5 | 148-154, 172-176, 194-197 | 155-159, 177-181, 198-202 | 160-164, 182-186, 203-207
Jan. 22 | 7-17 | 2-6(1), 2-6(2), 7-11(2) | 135-139, 174-178, 208-212 | 140-144, 179-183, 213-217 | 145-149, 184-188, 218-222
Jan. 23 | 1-11 | 277-291 | 169-173, 202-206, 235, 237-241 | 174-178, 207-211, 242-247 | 179-183, 212-216, 248-252
Jan. 24 | 319-329 | 304-318 | 132-136, 165-169, 198-202 | 137-141, 170-174, 203-207 | 142-146, 175-179, 208-212
Jan. 25 | 261-275 | 243-257 | 176-180, 209-213, 242-246 | 181-185, 214-218, 247-251 | 186-190, 219-223, 252-256
*Table 1: Data files needed for research project. Flats contains dome flats for VRI. Jan. 22 has data files from the previous UT date as well as the concurrent UT date in the flats, those marked with (1) are from the previous date and those marked with (2) are from the next.* 


## Getting Back to the Science

This past weekend (Feb. 1-2) I was assigned my project for AST 341. This involves looking at mass dependence of rotation in the intermediate-age Praesepe cluster (this is why only the Praesepe data is selected above). If time permits I will also be able to further analyze these data with GAIA proper motions and age determinations from relevant literature.

## Goals for next week

I need to get started on the draft for my research proposal to analyze the data in this way. Additionally, I'll need to have a way to download the data listed above by obtaining an SD card with sufficient space. Once this is done I'll start looking at the data and tweaking my reduction pipeline from last semester to better match the data for this project.
