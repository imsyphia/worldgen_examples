Round allows rounding numbers to the nearest integer by adding and subtracting a magic number (2^52).

The magic number is m and n is the negative of it, for more convenient (and performant) subtracting.

The add and subtract only works properly for positive numbers, negative numbers need to be handled differently.

For negative numbers, generate a value 1 or -1 depending on the sign of the number by clamping the input
to -0.5, 0.5 (values within this range will round to 0, so the number doesn't matter) and multiplying by 2. (see examples)

Multiply the above value by the rounded (+ m + n) absolute value of the input to restore its sign.