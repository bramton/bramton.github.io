---
layout: default
---

# Frequency domain
Learning outcomes for this chapter are:
  * describe the relation between the three parameters of a cosine and the frequency spectrum
  * sketch the spectrum given a time-domain function consisting of weighted cosines
  * use MATLAB or Python to tranform a signal to the frequency domain and plot the corresponding spectrum with a correct frequency axis

## An example
An important engineering tool is the Fourier transform. This transform maps a signal from the time domain into the frequency domain. This new representation of the signal can provide valuable insights. As an example, consider an audio fragment which has been distorted with an interference frequency. An example of a distorted audio fragment is provided below:
<audio controls>
	<source src="/assets/audio_distorted.flac" type="audio/flac" />
	<p>Your web browser does not support the HTML5 audio element.</p>
</audio>

The interference is rather annoying and it would be nice if it could be filtered out. In order to design a filter the exact frequency of the interference needs to be know. A naive first attempt to determine the interference frequency could be to plot the audio signal:
<figure>
	<img src="/assets/audio_time_domain.png" alt="Audio in time domain" width="400"/>
	<figcaption>
		Audio fragment plotted in the time domain.
	</figcaption>
</figure>
This plot shows the time on the x-axis and the amplitude of the audio signal on the y-axis. Looking at this plot it is impossible to determine the frequency of the interference signal. Luckily the engineer facing this problem has some DSP knowledge and decided to transform the audio signal to the frequency domain and visualise this. 

<figure>
	<img src="/assets/audio_frequency_domain.png" alt="Audio in frequency domain" width="400"/>
	<figcaption>
		Audio fragment transformed to the frequency domain.
	</figcaption>
</figure>
This plot might be a bit hard to interpret at first, it shows the frequency on the x-axis and the proportion of this frequency present in the signal. The larger the the value on the y-axis, the more dominant this specific frequency is present in the signal.  As we can see we have a large spike at 6 kHz, which corresponds to the until now unkown interference frequency. Later a filter will be designed to filter out a specific frequency, this is called a [notch](todo) filter.

## Frequency domain essentials

A very nice explanation why negative frequencies must exist is given on [StackExchange](https://dsp.stackexchange.com/a/449).

## MATLAB and Python
This section will describe how to obtain a visualisation of the frequency domain using two popular scripting languages, MATLAB and Python. This visualisation is usually called the spectrum. Both scripting languages use the `FFT` function, which stands for Fast Fourier Transform. An important parameter to the FFT function is `N`, this will tell the FFT function to evaluate the presence of `N` discrete frequencies within the signal. These `N` discrete frequency components are obtaind within the range of the sampling frequency $f_s$. This span usually ranges from $-\frac{f_s}{2}$ till $\frac{f_s}{2}$. For example if the sampling frequency is 100Hz and $N=10$ the precence of the following frequencies is evaluated:

$$
-50, -40, -30, -20, -10, 0, 10, 20, 30, 40
$$

As you can see also negative frequencies are considered but they are usually omitted when plotting the spectrum, as the spectrum is symmetric. If only the positive frequencies are plotted it is called the single-sided spectrum, if negative frequencies are plotted as well it is called a double-sided spectrum. The FFT function returns an array of `N` elements which contain the complex Fourier coefficients. A complex number can describe a magnitude and an angle (the phase) at the same time. Both MATLAB and Python list the coeffiecient for positive frequencies first, followed by the coeffiecient of the negative frequencies. As an example, given the following time-domain function 
$f(t) = 3 + 2cos(2 \pi 20 t + \pi/4)$ which is sampled at 100 Hz. The FFT is applied with `N = 10` and will return the following Fourier coefficients:

| Array index | Frequency component (Hz)| Fourier coefficient |
|-------------| ------------------------| ------------------- |
| 0           | 0                       | 3 + 0j              |
| 1           | 10                      | 0 + 0j              |
| 2           | 20                      | 0.71 + 0.71 j       |
| 3           | 30                      | 0 + 0j              |
| 4           | 40                      | 0 + 0j              |
| 5           | -50                     | 0 + 0j              |
| 6           | -40                     | 0 + 0j              |
| 7           | -30                     | 0 + 0j              |
| 8           | -20                     | 0.71 - 0.71j        |
| 9           | -10                     | 0 + 0j              |

For example, the Fourier coefficient at array index 2 equals `0.71 + 0.71j` if we look at the magnitude of this complex number it will be 1 and if we look at the angle of this complex number it will be $\pi/4$. The angle is exactly the same as the phase of the cosine, but the magnitude does not match the amplitude of the cosine. This is because the energy is divided equally amongst negative and positive frequencies, hence both 20 and -20 Hz have a magnitude of 1. The frequency 0 Hz is the DC component (also called the bias sometimes) of the signal and in the example has a magnitude of 3.

Positive frequencies are listed first to easily plot single-sided spectra, the array needs to be indexed from 0 till 4 in this case.

To make optimal use of the _Fast_ of the FFT function the parameter `N` should be a power of 2. On a normal desktop/laptop it will be hardly noticable, but when working on an embedded system or if performance is really an issue it is something to remember.

### MATLAB
Onwards to the fun part, the code. This section shows how to plot a double-sided spectrum of a signal. It is the same signal as in the previous section.
~~~ MATLAB
fs = 100;
N = 10;
spec = fft(x, N)/N;

freq_axis = (-5:1:4)*(fs/N);
stem(freq_axis, fftshift(abs(spec)))
xlabel('f (Hz)')
ylabel('Magnitude')
~~~

The tricky part when plotting the spectrum is to get the frequency axis correct. We've already seen that the frequency span $f_s$ is divided into `N` discrete frequencies, hence the step size is $f_s /N$. Taking the absolute value of a complex number will return the magnitude. The `fftshift` function in the sample code is there to rearange the values within the array, it will take the coefficients corresponding to the negative frequencies and will place them in front of the positive frequencies. The reader is encouraged to run `fftshift(1:10)` on the MATLAB command line and reason the result. The `stem` function is used to plot the result because the x-axis consists of discrete values.

<figure>
	<img src="/assets/freq_spectrum_MATLAB.png" alt="Spectum plotted with MATLAB" width="400"/>
	<figcaption>
		Spectrum plotted with MATLAB
	</figcaption>
</figure>

### Python
This section show howto plot a double-spectrum using Python in combination with the Numpy and Matplotlib libraries.
~~~ Python
fs = 100
N = 10
spec = np.fft.fft(x, N)/N
freq_axis = np.fft.fftfreq(N, 1/fs)
plt.figure
plt.stem(freq_axis, np.abs(spec), basefmt=" ")
plt.xlabel('f (Hz)')
plt.ylabel('Magnitude')
~~~

Luckily Numpy provides a `fftfreq` which is a nice convenience function to get the tricky frequency axis correct. This also saves us doing an `fftshift` operation. The `basefmt` argument to the `plt.stem` function prevents drawing an unnesecary baseline in the plot. The final result can be seen in the figure below.

<figure>
	<img src="/assets/freq_spectrum_Python.png" alt="Spectum plotted with Python" width="400"/>
	<figcaption>
		Spectrum plotted with Python
	</figcaption>
</figure>

## Test your knowledge
<iframe src="https://h5p.org/h5p/embed/382337" width="1091" height="207" frameborder="0" allowfullscreen="allowfullscreen"></iframe>
<script src="https://h5p.org/sites/all/modules/h5p/library/js/h5p-resizer.js" charset="UTF-8"></script>