---
permalink: /Blog-Post-7.html
---
#Blog Post Week 7

## This Week's Work

## Reading Notes

### Fourier Transform

(Since I've previously watched *But what is the Fourier Transform? A visual introduction.* I'd rather give a different introduction to Fourier Transforms.)

A Fourier Transform is a functional that converts the input function from signal space to frequency space. In simpler terms, this is a functional, i.e. a function that takes a function as an input and also returns a function, that samples the function for repeating signals, and converts this function into one that peaks where frequencies of repeating signals are likely to be present. The mathematical form of this functional is the following: $$F(k)=\int_{\mathbb{R}}f(x)\exp(-2\pi ikx)dx$$ where f(x) is the original function. This turns out to be one of the most useful tools in science and mathematics, with applications in just about any field from pure mathematics to biology, computer science, and of course astronomy.

In order to understand a little better, consider the Fourier Transform of the cosine function: $f(x)=\cos(2\pi k_0x)$, which has a frequency of $k_0$ (first repeats when $x=\frac{1}{k_0}$). The transform of this worked out with the above expression is $F(k)=\frac{1}{2}(\delta(k-k_0)+\delta(k+k_0))$. Note this function is nonzero only twice: at $x=\pm k_0$, which is of course the only frequency of this cosine function; there is no spread as this is exactly the frequency. Additionally, the integral over this function is equal to one. Based on these properties one might conclude the Fourier Transform of a function is a probability distribution; while this is not exactly true, it is analogous, and in some applications one can interpret the Fourier Transform as the probability distribution of frequencies present in the function.

When doing science that relies on data and smooth, continuous functions are not available, we can use the Fast Fourier Transform (FFT) algorithm to approximate the functionality of the Fourier Transform on the real line. The drawback is that instead of resulting in infinite peaks exclusively at frequencies present in the function, we end up with finite peaks spread out over a range of values. But if the transform is nonzero at an infinite number of locations, how can one tell where the frequencies are? This is where the probability density interpretation comes in handy: by integrating over certain regions, one can estimate where exactly the peaks are, and how strong they are relative to each other and in this way determine the signal and noise of estimated frequencies. 

One more piece to the FT puzzle is needed before we can talk about the relevant application: traditional FFT algorithms require evenly spaced sampling points. In astronomy however, we are typically not so blessed outside of the laboratory. Instead a modified algorithm is used, known as the Lomb-Scargle Periodogram. While one could easily go into detail on how the LS Periodogram is produced, it is sufficient here to say that it is an optimal tool for the application of finding the period of brightness variation from light curve points: since we take many observations of a source per night, and the observations are not evenly spaced, the LS Periodogram can interpolate between missing points and in this way produce the frequency spectrum of a light curve's brightness variations. For this reason we will be using the LS Periodogram in class to estimate periods for our detected sources.


### Time Series Analysis of Variable Star Data

Interpretation of time-domain data has a long history in science, maths, and astronomy. The culmination of research in this area was the discovery of the Fourier Transform and FFT in the 19th and 20th centuries. For some time dependent data $x(t)$ (written f(x) in my above analysis) one can compute the Fourier Transform by calculating an integral over the real line. With the complex exponential present in the functional this actually acts as splitting sine and cosine components into imaginary and real parts of the integral. One can also compute a data fourier transform (FFT) by approximating the integral by summing over sampled data. In this case the quality of the transform is dependent on the sampling rate. The Nyquist frequency is the smallest detectable frequency based on the number of samples and total time period over which the samples were taken; to "detect" a frequency one must have a maximum and a minimum although certain techniques (e.g. aliasing mentioned in the text) can allow even smaller frequencies to be detected.

As is to be expected, errors in the data will propogate into errors in the fourier transform. The effect this has on the transform takes the form of small, noisy peaks scattered at all frequencies. Determining errors in frequency estimates from the fourier transform is a complicated task, and numerous algorithms and packages are available to perform this task.

Of the many Fourier Transform algorithms, the ones we are mainly interested in are the FFT and LS Periodogram mentioned above. FFT has the benefit of being computationally inexpensive while requiring evenly spaced data points; LS is not restricted in this way however it is a much slower algorithm. Indeed, we have actually used FFT before in class for our alignment algorithm, however this will not be an option with our unevenly spaced photometric data. On the other hand, by doing FTs using the LS Periodogram, we can detect brightness variation periods present in our data. If there are multiple periods present, we can also detect more than one at once by finding the multiple peaks in the Fourier Transform. 

### Paper Discussion