# Post for discussion

https://colah.github.io/posts/2014-03-NN-Manifolds-Topology/

## Notes

The main takeaway here is that neural networks are fundamentally manipulating (n-dimensional) space to create linear
separability between two groups of data.  Linear separability is (loosely) defined as being able to draw a straight line
such that all items of category A are on the left, and all items of category B are on the right.

And of course, there are some constraints.

### Linear separability

The most important constraint with linear separability here (assuming we can even achieve linear separability - more on that
later in the knot theory section) is for N classes of data, we need at least N+1 nodes in our hidden layer.  Colah illustrates
this quite elegantly with two concentric circles on a plane - there does not exist any manipulation of the plane in two
dimensions such that we can achieve linear separability between these two circles.  If we add a third dimension, we can move
one of the circles "up" or "down", and then draw a plane between the two to achieve linear separability.  In practice, this
really means drawing a "hyperplane" between the two classes of data...and each class of data may actually have many more
classes within.

### Knot theory

There's a section on knot theory at the bottom, which is basically saying we can only achieve linear separability if we have
the aforementioned N+1 nodes in our hidden layer, AND if we have a "trivial knot".  Here, a trivial knot essentially means
a knot that can be "easily" undone into something topologically equivalent to a torus.  We can think of this as a configuration
of stuff that we get to in a twisted state, and with a series of easy untwisting (e.g. rotate backwards 90 degrees, then
rotate left 45 degrees, then push it under the overpass, etc.), we can obtain a donut shape.

### Hyperbolic tangent, affine transformations

The hyperbolic tangent function is used quite a bit as an activation function - why is this?  It has the nice property that it
takes any real-valued input, and outputs something between [-1, 1] (asymptotically).  It's also an affine transformation - 
something simplifies things greatly for us, and allows us to continue thinking of these things as lines, and not complicated
hypercurves on a hyperplane.

So what's an affine transformation?  It's an operation applied to a mathematical object (like a line, or a plane) that
preserves colinearity and distance ratios.  Colinearity means all points on the line before the transformation are there
after the transformation.  Distance ratio preservation means a midpoint remains a midpoint (and so on for other ratios).

It also has the nice property that is has an inverse defined, which (amongst other conditions), means we can use it to
deform our manifold without worrying about whether or not we are altering some fundamental property of our data.  Formally,
we need our topological transformation to be a homeomorphism - but we don't need to get into specifics here.

Why can't we use ReLU as an activation function for this problem?  Well, there's a graphical trick for finding an inverse
(which is directly related to the analytical method of determining an inverse).  First, you draw your original function,
whose inverse you want to find.  Then, you draw the line y=x.  Then you mirror the original function on the line y=x.  You'll
notice if you do this with ReLU, the inverse is not a function at all, since it fails the vertical line test!

### (Linear) Algebra

Colah mentions the following items:

1. Determinants
2. Linear transformations
3. Linear translations
4. Bijections (but not injections)

These are all important because they allow us to remain in linearland (instead of hypercurve hyperspace land), and they can
all be applied to the tanh activation function.  To quote:

```
1. A linear transformation by the “weight” matrix W
2. A translation by the vector b
3. Point-wise application of tanh.
```

So, for the items:

1. Our weight matrix has a determinant!  A determinant of zero means linear dependence, instead of linear independence.
Linear dependence for the weight matrix ultimately means we are not guaranteed to find a unique solution!  This means our
transformation is not convex, which may end up breaking gradient descent as a method of convergence.  More on that in a 
different session.
2. A linear transformation can be thought of as a rotation that warps the X-Y grid, and any points that were on the grid
move along with it.  I like to think of it as a rubber grid that gets warped as you tug one edge up and the other edge down.
3. A linear translation is an operation that shifts a set of points in one direction on the same plane.  Imagine a set of
points on the X-Y plane, and tilting the plane so that they all shift over to the left by the same amount.
4. Bijections are mappings that are one-to-one and onto (sometimes called an injective and a surjective 
mapping, respectively).  They take points from A (the domain) and map them onto B (the range).  This 
[Mathworld link](http://mathworld.wolfram.com/Injection.html) explains it much more intuitively via pictures than I ever
could with text.
