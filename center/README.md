## Center distance

These density functions give a value that increases with the horizontal distance from the center of the world.

Credit for the method used goes to **starmute**, who insisted the impossible should become possible.

###### Method

This works by using the divergence of a noise when it is sampled at two different xz scales.
At 0,0 the noise is being sampled at the same position, so the values are exactly the same.
As the coordinates increase, the positions being sampled are further apart, so the
magnitude of the difference will tend to increase.

In this case, four noises are used and the differences are averaged to provide a consistent value
regardless of the number of noises.

The value will tend to increase consistently until about 2^(-1 - `firstOctave`) blocks, where it will
then vary randomly, but will _usually_ not reach a very low value, especially with many noises being averaged.

The `noises` folder contains the noise files (that would usually be in `<namespace>/noise`),
which are just noises with a `firstOctave` of a convenient scale and one octave of amplitude 1.

The range and behavior of the value should be tested before using it, in order to see what
scaling or transformation should be done when using it for a particular purpose.