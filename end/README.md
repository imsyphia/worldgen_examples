## Center End Island Re-implementation

The `fake_end_islands` density function recreates the behavior of the hardcoded `end_islands` density function
type for the center end island. The outer island behavior is not recreated.

Dependencies:
- dfcoord (https://github.com/imsyphia/dfcoord)

###### Method

The below is moderately technical because I'm not in the business of explaining mathetmatical
concepts that are well documented, such as distance calculation or what a
[Taylor series](https://en.wikipedia.org/wiki/Taylor_series) is.

The center of `end_islands` is a radial gradient that is greatest at the center of the world
and reaches a minimum about 180 blocks away.

To recreate this, the `distance_squared` function calculates the square of the distance from
the center, and the `distance` function approximates the square root of it, so the actual distance,
using a partial sum of a Taylor series written as a standard form cubic polynomial.

There's some additional code in `fake_end_islands` which handles the specific details of
`end_islands`, such as the scaling and offset of the value, as well as the maximum
being at 20 blocks from the center and minimum being at 180.