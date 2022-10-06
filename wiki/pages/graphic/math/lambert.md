
```
 *其中Ia 表示环境光强度，Kd(0\<K\<1)为材质对环境光的反射系数，
*Iambdiff是漫反射体与环境光交互反射的光强。
*其中Il是点光源强度，θ是入射光方向与顶点法线的夹角，称入射角(0\<=A\<=90°)，
*Ildiff是漫反射体与方向光交互反射的光强，若 N为顶点单位法向量，
//L表示从顶点指向光源的单位向量(注意顶点指向光源)，则Cos(θ)等价于dot(N,L)，故又有：

Iambdiff = Kd\*Ia Ildiff = Kd \* Il \* dot(N,L) Idiff = Iambdiff +
Ildiff = Kd \* Ia + Kd \* Il \* dot(N,L) 
```

