---
layout: default
---

# Frequency domain
Learning outcomes for this chapter are:
  * la
  * la

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
		Audio plotted in the time domain.
	</figcaption>
</figure>
This plot shows the time on the x-axis and the amplitude of the audio signal on the y-axis. Looking at this plot it is impossible to determine the frequency of the interference signal. Luckily the engineer facing this problem has some DSP knowledge and decided to transform the audio signal to the frequency domain and visualise this. 

<figure>
	<img src="/assets/audio_frequency_domain.png" alt="Audio in frequency domain" width="400"/>
	<figcaption>
		Audio plotted in the frequency domain.
	</figcaption>
</figure>
This 


