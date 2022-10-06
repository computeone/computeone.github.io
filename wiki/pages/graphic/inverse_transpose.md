**Normal Transformation**\
In the last section, we saw that our computation of the cosine of the
angle of incidence has certain requirements. Namely, that the two
vectors involved, the surface normal and the light direction, are of
unit length. The light direction can be assumed to be of unit length,
since it is passed directly as a uniform.\
\
The surface normal can also be assumed to be of unit length. Initially.
However, the normal undergoes a transformation by an arbitrary matrix;
there is no guarantee that this transformation will not apply scaling or
other transformations to the vector that will result in a non-unit
vector.\
\
Of course, it is easy enough to correct this. The GLSL function
normalize will return a vector that is of unit length without changing
the direction of the input vector.\
\
And while mathematically this would function, geometrically, it would be
nonsense. For example, consider a 2D circle. We can apply a non-uniform
scale (different scales in different axes) to the positions on this
circle that will transform it into an ellipse:\

\
\
<https://paroj.github.io/gltut/Illumination/Tut09%20Normal%20Transformation.html>
