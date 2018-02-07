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
An arbitrary signal x(t) can always be expressed as a sum of an even signal and an odd signal.

$$
x(t) = x_e(t) + x_o(t)
$$

Where the even part of the signal $x_e(t)$ is given by

$$
x_e(t) = \frac{1}{2} \left[ x(t) + x(-t) \right]
$$

and the odd part of the signal $x_o (t)$ is given by

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

