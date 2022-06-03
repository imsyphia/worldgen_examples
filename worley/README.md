## Worley Noise

These density functions generate two-dimensional worley noise.

Dependencies:
- round
- dfcoord (https://github.com/imsyphia/dfcoord)

###### Algorithm Description

The basic algorithm is fairly simple.

The algorithm can be thought of as dividing space into a grid, and placing a point at a random location in each grid cell.
The noise value of a given location is the distance to the nearest point (distance squared for performance in this case).

###### Implementation

The implementation is, of course, more complicated.

Files or collections of files that implement parts are marked in \[\] where / indicates a folder, e.g. \[xb, xs\] or \[xf/\]

Firstly, observe that the closest point to a location is most often either in the same grid cell or in one of the 8 neighboring cells.
It is possible for that to not be the case, however this is a very good approximation. (A restriction on the range of a point's position could guarantee this)

Because of the above, a given location only needs to know the position of the points of the current cell and its neighbors.
A point's position can be deterministically generated based on the location of its cell by some function of the cell's coordinates. (cell coords are \[xb zb\])
I use a method I quickly hacked together to accomplish this, which is `(x, z) = (abs((x + a) * (z + b)) * c + d) mod 1, z = (g * x + h) mod 1`, \[r/ f/ r2/ f2/\]
where a, b, c, d, g, h are constant semi-random numbers. Adding a constant to x and z prevents issues when x or z is 0.

It is also trivial to calculate the cell coordinates of adjacent cells from a given cell, simply by adding or subtracting 1 from x and z, \[xf/ zf/\]
because a cell is defined as being 1 unit square (for convenience)

The above means that, from a location, it is possible calculate the position of points in the current and all neighboring cells,
which allows calculating the square of the distance to each point by adding the squares of the distances on the x and z axes \[d/\].
Finding the square root is inaccurate and computationally expensive, so that is not done here.

From here all that is needed is taking the minimum of all those distances \[worley\]

Scaling the input to the noise \[s xs zs\] allows adjusting the scale of the noise relative to the input coordinates.
e.g. if worley is sampled at (x, z) in game, every block would be an entire grid cell, which is undesirable.
However if you scale input by 0.05, the coordinates have to change by 20 to move an entire grid cell,
which makes the noise much "larger" in relation to the world.

###### If you made it this far

Fun fact: This alone has 3x more files than the entire vanilla worldgen df folder (although it is smaller due to a lack of splines)