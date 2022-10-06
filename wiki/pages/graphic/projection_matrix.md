3、DepthBuffer 顶点的 z 值在进行透视变换后为

`zclip=−zviewf+nf−n−2nff−n`

经过齐次除法后NDC空间的

`zndc=zclipwclip=f+nf−n+2nf(f−n)zview`

由Viewport Transform可知DepthBuffer中的 `zdepth=1/2⋅zndc+1/2`

代入 zndc 可得：

`zview=1f−nfnd−1n`

取反后除以 f 即可映射到 \[0,1\] 中。

Some math I did \... (not 100% verified, but looks like it works)\

```
 n = near

f = far

z = depth buffer Z-value

EZ = eye Z value

LZ = depth buffer Z-value remapped to a linear \[0..1\] range (near
plane to far plane)

LZ2 = depth buffer Z-value remapped to a linear \[0..1\] range (eye to
far plane)

DX:

EZ = (n \* f) / (f - z \* (f - n))

LZ = (eyeZ - n) / (f - n) = z / (f - z \* (f - n))

LZ2 = eyeZ / f = n / (f - z \* (f - n))

GL:

EZ = (2 \* n \* f) / (f + n - z \* (f - n))

LZ = (eyeZ - n) / (f - n) = n \* (z + 1.0) / (f + n - z \* (f - n))\'\'

LZ2 = eyeZ / f = (2 \* n) / (f + n - z \* (f - n))\'\'

LZ2 in two instructions:

LZ2 = 1.0 / (c0 \* z + c1)

DX:

    c1 = f / n
    c0 = 1.0 - c1

GL:

    c0 = (1 - f / n) / 2
    c1 = (1 + f / n) / 2


```
\
\
[投影矩阵的推到公式](http://blog.csdn.net/pizi0475/article/details/46794209)\
http://blog.csdn.net/NotMz/article/details/73692932(各种变换公式）\
