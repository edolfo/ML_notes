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

### Linear algebra

