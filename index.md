## Analog to Digital conversion

### Quantisation noise
<figure>
	<img src="assets/quant_error_distribution.png" alt="Histogram of the quantisation noise." width="400"/>
	<figcaption>
	Histogram of the quantisation noise.
	</figcaption>
</figure>

A simple model to describe the error introduced by the quantiser is an additive model.

$$
e[n] = x_q[n] - x[n]
$$
This error is often called quantisation noise.

The signal-to-quantisation-noise (SQNR) can be expressed in decibels as:

$$
SQNR = 10\log_{10}\frac{P_x}{P_n}
$$

Where $P_x$ is the signal power and $P_n$ is the power of the quantisation noise. The quantisation noise power can be derived from its probability density function.

$$
P_n = \sigma_e^2 = \int_{-\infty}^{\infty} e^2 p(e) de = \frac{1}{\Delta} \int_{-\frac{\Delta}{2}}^{\frac{\Delta}{2}} e^2 de = \frac{\Delta^2}{12}
$$



## Fourier transform

$$
x(t) = c_0 + \sum_{n=1}^\infty A_n \cos(n\omega_0t + \phi_n)
$$

Where $c_0$, $A_n$ and $\phi_n$ are based on the complex Fourier coefficients $c_n$.

## Symmetry
Symmetry of signals is a useful property for analysing signals and has an important role in the theory of power series and Fourier series. 

### Even symmetry
A signal is said to be even symmetric if it is identical to the reflection about the origin.

$$
x(t) = x(-t)
$$

<figure>
	<img src="assets/function_cos.png" alt="Cosine function" width="200"/>
	<img src="assets/function_abs.png" alt="Absolute function" width="200"/>
	<img src="assets/function_square.png" alt="Square function" width="200"/>
	<figcaption>
	Three examples of even functions.
	</figcaption>
</figure>

### Odd symmetry
A signal is said to be odd symmetric if:

$$
x(t) = -x(-t)
$$

<figure>
	<img src="assets/function_sin.png" alt="Sine function" width="200"/>
	<img src="assets/function_sigmoid.png" alt="Sigmoid function" width="200"/>
	<img src="assets/function_cube_poly.png" alt="Cube function" width="200"/>
	<figcaption>
	Three examples of odd functions.
	</figcaption>
</figure>

### Decomposition
An arbitrary signal $x(t)$ can always be expressed as a sum of an even signal and an odd signal.

$$
x(t) = x_e(t) + x_o(t)
$$

Where the even part of the signal $x_e(t)$ is given by

$$
x_e(t) = \frac{1}{2} \left[ x(t) + x(-t) \right]
$$

and the odd part of the signal $x_o(t)$ is given by

$$
x_e(t) = \frac{1}{2} \left[ x(t) - x(-t) \right]
$$


~~~ matlab
y = fft(x)
% comment
~~~

Nog wat tekst  bal bla.

> This is a block quote ?
> Met een
> # Header ? huh
> * een
> * twee

En een regel.

