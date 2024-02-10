https://www.grc.nasa.gov/www/k-12/Numbers/Math/documents/Tensors_TM2002211716.pdf

A Vector has *both* a magnitude and a direction. A velocity specified as '5 mph due east', is a vector: '5mph' is the magnitude, 'east' is the direction. Contrast with a 'scalar', which is a single discrete value, or magnitude.

A 2D vector can be represented on a simple coordinate plane. We might take the length of the vector to represent its magnitude, and the axis along which it travels to represent direction (N, S, E, W). In that case the example above would look like:

```chart
	type: line
	labels: [0,1,2,3,4,5,6,7,8,9]
	series: 
	- title: Vector A
	  data: [1,1,1,1,1]
```

Vectors are not concerned with absolute position, so the two vectors described below are equivalent, and would both be written as $\begin{bmatrix} 5 \\ 0 \end{bmatrix}$:

```chart
	type: line
	labels: [0,1,2,3,4,5,6,7,8,9]
	series: 
	- title: Vector A
	  data: [1,1,1,1,1]
	- title: Vector B
	  data: [null,3,3,3,3,3,3]
```

Vectors can be written as coordinate tuples, where each value in the tuple is the vector's magnitude in a given direction. The direction for each magnitude is derived from its position in the tuple. We can denote `Vector A` above as $\vec{A} = (5,0) = \begin{bmatrix} 5 \\ 0 \end{bmatrix}$ , where the first number is the magnitude in the left-right dimension (`x`), and the second number is the magnitude in the up-down dimension (`y`). 

The total magnitude of a vector is derived from its constituent magnitudes. Consider $\vec{A} = \begin{bmatrix} 3 \\ 4 \end{bmatrix}$ :
```chart
	type: line
	labels: [0,1,2,3,4,5,6,7,8,9]
	spanGaps: true
	series: 
	- title: Vector A
	  data: [0,null,null,4]
```

The total magnitude is the length of the vector, which in this case is the hypotenuse of a 3,4,5 right triangle, so we know that the combined magnitude is 5.

2- and 3-dimensional vectors are easiest to visualize, but the dimensionality of a vector space is in principle unlimited.

## Unit Vectors
A 'unit vector' is a special kind of vector that defines the space in which other vectors operate. A unit vector has a magnitude of exactly 1 and is used to specify direction. For example, in the list of directions '2 blocks east, 1 block north, and 2 floors up', {2,1,2} are scalars, and {east,north,up} can be generalized as (e.g.)  unit vectors _i_, _j_, and _k_, each corresponding to one dimension in a 3-dimensional space.

## Dimensionality
The 'coordinate space' above can be denoted as $\mathbb{R}^2$, where $\mathbb{R}$ symbolizes the set of all real numbers. Intuitively the area of the Cartesian plane whose y-values are every value in $\mathbb{R}$ and whose x-values are every value in $\mathbb{R}$ is $\mathbb{R}^2$.  So the 'two-dimensional real coordinate space' is every possible real-valued 2-tuple. This is extensible to `n` dimensions, so the n-dimensional real coordinate space is written $\mathbb{R}^n$. 

## Operations

### Addition
To add 2 or more vectors that are in the same coordinate space, simple add add the magnitudes of each direction. E.g. if $\vec{A} = \begin{bmatrix} -2 \\ 4 \end{bmatrix}$  and $\vec{B} = \begin{bmatrix} 7 \\ 5 \end{bmatrix}$ , then $\vec{A} + \vec{B} = \begin{bmatrix} 5 \\ 9 \end{bmatrix}$. Visualize this in a 2D coordinate space by drawing the first vector, then drawing the second vector with its 'tail' beginning at the 'head' of the first vector. A vector drawn from the 'tail' of the first vector to head of the second vector is the solution vector.

### Scalar multiplication
To multiple a vector by a scalar, simply multiply each member of the vector by the scalar. E.g. if $\vec{A} = \begin{bmatrix} 3 \\ 2 \end{bmatrix}$, then $3\vec{A} = \begin{bmatrix} 9 \\ 6 \end{bmatrix}$. NB that this increases the magnitude of the vector, but does not change its direction. This is hinted at by the word 'scalar': a standalone number used to scale a vector without modifying its direction. Multiplying by a negative number will reverse the direction and (if the negative scalar < -1 ) increase the magnitude in the new direction.