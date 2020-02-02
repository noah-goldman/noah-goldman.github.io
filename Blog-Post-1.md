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
astronomical observatories while also gaining experience operating the 0.9 meter telescope.

#### What important information did you learn about HDI and the data we took?

#### What steps will you need to perform to reduce your data? What software will you need/use?

For each of the data files, I will need to perform the standard reduction operations: prepare master bias files, prepare master flatfields in each band
for each night, bias subtract then flat normalize each science frame for my cluster, and finally shift and stack the reduced images. This can
all be done in python applying a variation of the reduction pipeline from last semester (AST 337), however I will need to be able to transfer the files for which I will need to get a portable storage device, and DS9 will be useful
for doing checks on each of the steps.

#### Go through logs and identify the data files (science AND calibrations) you’ll need for your project

