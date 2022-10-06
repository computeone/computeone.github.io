在数学的数值分析领域中，**贝济埃曲线（英语：Bézier
curve，亦作"贝塞尔"）**是计算机图形学中相当重要的参数曲线。更高维度的广泛化贝济埃曲线就称作贝济埃曲面，其中贝济埃三角是一种特殊的实例。\
贝济埃曲线于1962年，由法国工程师皮埃尔·贝济埃（Pierre
Bézier）所广泛发表，他运用贝济埃曲线来为汽车的主体进行设计。贝济埃曲线最初由Paul
de Casteljau于1959年运用de
Casteljau算法开发，以稳定数值的方法求出贝济埃曲线。\
\
The curve shown in Figure 4.14 has three control points, A, B, and C. A
and C are the endpoints of the curve and B defines the shape of the
curve. If we join points A and B with one line and points B and C
together with another line, then we can interpolate along the two lines
using a simple linear interpolation to find a new pair of points, D and
E. Now, given these two points, we can join them with yet another line
and interpolate along it to find a new point, P. As we vary our
interpolation parameter, t, point P will move in a smooth curved path
from A to D. Expressed mathematically, this is 
```
 D = A + t(B −
A) E = B + t(C − B) P = D + t(E − D)


```
 Substituting for D and E and doing a little crunching, we come
up with the following:\

```


P = A + t(B − A)+ t[^1]) − (A + t(B − A)))) P = A + t(B − A)+ tB +
t\^2(C − B) − tA − t\^2(B − A) P = A + t(B − A + B − A)+ t\^2(C − B −
B + A) P = A +2t(B − A)+ t\^2(C − 2B + A)


```
 You should recognize this as a quadratic equation in t. The
curve that it describes is known as a quadratic Bézier curve. We can
actually implement this very easily in GLSL using the mix function, as
all we're doing is linearly interpolating (mixing) the results of two
previous interpolations. 
```


vec4 quadratic_bezier(vec4 A, vec4 B, vec4 C, float t)

{

       vec4 D = mix(A, B, t);     D = A + t(B - A)

       vec4 E = mix(B, C, t);    E = B + t(C - B)

       vec4 P = mix(D, E, t);     P = D + t(E - D)

       return P;

}


```
\
\
<https://zh.wikipedia.org/wiki/%E8%B2%9D%E8%8C%B2%E6%9B%B2%E7%B7%9A>

[^1]: B +(t(C − B
