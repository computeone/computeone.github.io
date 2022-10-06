**Phong着色法**，三维电脑图像的绘图技巧之一，结合了多边形物体表面反射光的亮度，并以特定位置的表面法线作为像素参考值，以插值方式来估计其他位置像素的色值。\
\
最近在钻研Unity3D
Shader中的各种渲染效果，自然涉及到各种光照模型的使用，还记得三年前Computer
Graphic课有讲过，不得不感慨How time fly\...废话少说，进入正题：\
\
Lambert漫反射光照模型属于经验模型，主要用来简单模拟粗糙物体表面的光照现象,此模型假设物体表面为理想漫反射体（也就是只产生漫反射现象，也成为Lambert反射体），同时，场景中存在两种光，一种为环境光，一种为方向光，然后我们分别计算这两种光照射到粗糙物体表面所产生的光照现象，最后再将两个结果相加，得出反射后的光强值。\
\
首先是计算环境光的公式：\
I_ambdiff = K_d \* I_a;\
其中，K_d为粗糙物体表面材质对光的反射系数，这个系数由程序编写者在宿主程序中给出，I_a为环境光的光强，也就是环境光的颜色数值，一般是一个float3型的变量。\
\
然后是计算方向光的公式：\
I_ldiff = K_d \* I_l \* cosa;\
其中I_l为方向光的光强，也就是其颜色值，一般是float3型的变量。这个公式与计算环境光的不同，对于环境光，我们不关心它的方向，因为环境光也没有方向，它给予物体的光照在各个顶点处均是一样的。而方向光则需要关注其方向，例如一个聚光灯，灯从不同的角度来照射物体所产生的效果也是不一样的，光线方向越靠近法线，漫反射出来的光就越强，反之则越弱。公式中的a就是光线方向与顶点法线的夹角，同时要注意，入射光的方向在这里定义为顶点到光源位置。但是计算cosa会比较麻烦，所以在这里要变换一下公式，方便程序的书写。假设N为顶点的单位法向量，L为入射光的单位法向量（再次提醒一下，L的方向是由顶点指向光源的）这样，由向量的点积公式可得：cosa
= N﹒L,所以计算方向光的公式就变为:\
I_ldiff = K_d \* I_l \* (N﹒L);\
\
综上，得出漫反射后的光强为：\
I_diff = K_d \* I_a + K_d \* I_l \* (N﹒L);\
下面给出使用Cg语言的Lambert漫反射光照模型顶点着色程序：\
\
\[cpp\] view plain copy\

```
 struct vertex_In {

     float4 in_Position : POSITION;  
     float4 in_Normal   : NORMAL;  

}; struct vertex_Out {

     float4 out_Position : POSITION;  
     float4 out_Color    : COLOR0;  

}; void main_v(vertex_In vertexI,out vertex_Out vertexO,

              uniform float4*4 modelViewProj,  
              uniform float4*4 worldMatrix,  
              uniform float4*4 worldMatrix_IT,  
              uniform float3 globalAmbient,//全局光光强  
              uniform float3 lightPosition,  
              uniform float3 lightColor,  
              uniform float3 K_d//漫反射体反射系数)  

{

      vertexO.out_Position = mul(modelViewProj , vertexI.in_Position);//进行投影变换  
      float3 worldPosition = mul(worldMatrix , vertexI.in_Position).xyz;//计算顶点的世界位置  
      float3 N = mul(worldMatrix_IT , vertexI.in_Normal).xyz;//计算顶点的法向量  
      N = normalize(N);//向量规范化  
      //计算方向光方向  
      float3 L = lightPosition - worldPosition;  
      L = normalize(L);//向量规范化  
      //计算环境光漫反射光强  
      float3 ambColor = Kd * globalAmbient;  
      //计算方向光漫反射光强  
      float3 dirColor = Kd * lightColor * max(dot(N , L) , 0);  
      vertexO.out_color.rgb = ambColor + dirColor;  
      vertexO.out_color.a = 1;  

}


```


对于纸张、粗糙墙壁等等来说，Lambert模型或许够用，但对于金属这样的光滑表面来说，我们就需要使用Phong模型来模拟光滑表面对光线的镜面反射现象。同Lambert一样，这个模型也是经验模型，而且在程序中，我们经常同时使用Lambert和Phong两个模型，因为在现实世界中，任何表面都会同时发生漫反射和镜面反射两种现象，因此我们就要使用两种模型分别计算两种反射后的光强（也就是顶点颜色值），是渲染的效果看起来真实一些。但要注意，这样做并不会带来真正真实的渲染效果，毕竟这两种模型都是经验模型，考虑的都是理想情况下。而Blinn-phong光照模型是基于Phong的修正模型，因此就一并总结了。\
\
我们知道，在理想状况下，镜面反射后的光之集中在一条线上，因此我们的视线离这条线的距离越近，射入我们眼中的光线就越多，我们看到的光强也就越强。同时，镜面反射也与物体表面的高光指数（物体表面光泽程度）有关，其数值越大，反射后的光线越集中，反之则越分散，这里可能会有人想：如果将高光指数设置的很大，也就是光线极其分散，Phong是否可以用来代替Lambert？我想答案肯定是不行的，原因是漫反射是将光线反射到各个角度，而镜面反射即使反射光线再分散，它们依旧被限制在一个90度的区域中，因此与漫反射的效果是不一样的。
下面给出公式：\
\
I_spec = k_z \* I_l(V • R)\^n_s\
其中：k_z为表面材质的镜面反射系数，n_s是高光指数，V表示顶点到视点的向量，R表示反射光的单位向量。\
但是在实际的程序编写中，我们一般都会更容易得到入射光线的单位向量L，所以我们最好转换一下公式。设顶点的单位法向量为N，有公式：
R + L = (2N • L)N （这里再次提醒一下，L的方向是由顶点指向光源的）\
由这个可以推出：\
R = (2N • L)N - L\
所以模型公式可以变为：\
I_spec = k_z \* I_l(V • [^1]\^n_s\
下面是用Cg语言实现Phong模型的代码：\
\
\[cpp\] view plain copy\

```
 struct vertex_In {

      float4 in_Position : POSITION;  
      float4 in_Normal   : NORMAL;  

} struct vertex_Out {

      float4 out_Position : POSITION;  
      float4 out_Color    : COLOR0;  

} void main_v(vertex_In vertexI,

              out vertex_Out vertexO,  
              uniform float4*4 modelViewProj,  
              uniform float4*4 worldMatrix,  
              uniform float4*4 worldMatrix_IT,  
              uniform float3 globalAmbient,  
              uniform float3 eyePosition,  
              uniform float3 lightPosition,  
              uniform float3 lightColor,  
              uniform float3 K_d,  
              uniform float3 K_s,  
              uniform float N_s)  

{

      vertexO.out_Position = mul(modelViewProj , vertexI.in_Position);//计算输出定点位置  
      float3 worldPosition = mul(worldMatrix , vertexI.in_Position).xyz;//计算定点世界位置  
      float3 N = normalize(mul(worldMatrix , vertexI.in_Normal).xyz);//计算定点法线向量  
      float3 V = normalize(eyePosition - worldPosition);//计算定点到视点的方向  
      float3 L = normalize(lightPosition - worldPosition);//计算入射光方向  
      float3 R = normalize(N*max(dot(2*N , L) , 0) - L);//计算反射光方向  
      float3 diffuseColor = K_d*globalAmbient + K_d*lightColor*max(dot(N , L) , 0);//计算漫反射光强  
      float3 specularColor = K_s*lightColor*pow(max(dot(V , R) , 0) , N_s);//计算镜面反射光强  
      vertexO.out_Color.rgb = diffuseColor + specularColor;  
      vertexO.out_Color.a = 1;  

}


```


以上代码只使用了顶点着色程序，因此只对几何顶点进行渲染，而不对片段内部的点进行处理，因此如果用来渲染低精度模型效果会很不好，因此我们就要再加入片段着色程序。
代码如下： \[cpp\] view plain copy\

```
 struct vertex_In {

      float4 in_Position : POSITION;  
      float4 in_Normal   : NORMAL;  

} struct vertex_Out {

      float4 out_Position     : POSITION;  
      float4 out_objecPos     : TEXCOORD0;  
      float4 out_objectNormal : TEXCOORD1;  

} void main_v(vertex_In vertexI,

              vertex_Out vertexO,  
              uniform float4*4 modelViewProj  
              )//顶点着色程序入口  

{

      vertexO.out_Position = mul(modelViewProj , vertexI.in_Position);//计算输出定点位置      
      vertexO.out_objectPos = vertexI.in_Position;  
      vertexO.out_objectNormal = vertexI.in_Normal;  

} void main_f(vertex_Out vertexI,

              out float4 colorO : COLOR,  
              uniform float4*4 worldMatrix,  
              uniform float4*4 worldMatrix_IT,  
              uniform float3 globalAmbient,  
              uniform float3 eyePosition,  
              uniform float3 lightPosition,  
              uniform float3 lightColor,  
              uniform float3 K_d,  
              uniform float3 K_s,  
              uniform float N_s  
              )//片段着色程序入口  

{

      float3 worldPos = mul(worldMatrix , vertexI.out_objecPos).xyz;//计算定点世界位置  
      float3 N = normalize(mul(worldMatrix , vertexI.out_objectNormal).xyz);//计算定点法线向量      
      float3 V = normalize(eyePosition - worldPosition);//计算定点到视点的方向  
      float3 L = normalize(lightPosition - worldPosition);//计算入射光方向  
      float3 R = normalize(N*max(dot(2*N , L) , 0) - L);//计算反射光方向  
      float3 diffuseColor = K_d*globalAmbient + K_d*lightColor*max(dot(N , L) , 0);//计算漫反射光强  
      float3 specularColor = K_s*lightColor*pow(max(dot(V , R) , 0) , N_s);//计算镜面反射光强  
      colorO.rgb = diffuseColor + specularColor;  
      colorO.a = 1;  

} 
```
\
这样的话程序就会对片段中的点也进行处理，渲染效果也会好一些。\
相比较Phong模型，Blinn-phong模型只适用N•H替换了V•R，但却获得了明显的提高，它能提供比Phong更柔和、更平滑的高光，而且速度上也更快，因此成为很多CG软件中默认的光照渲染方法，同时也被集成到大多数的图形芯片中，而且在OpenGL和DirectX
3D的渲染管线中，它也是默认的光照模型。\
\
由于这两个光照模型公式基本相同，所以只解释一下N•H：\
N与前面相同，是顶点的单位法向量，而H则是入射光L和顶点到视点的单位向量的角平分线单位向量，通常也成为半角向量。其计算方法为：\
H = (L + V) / (\|L + V\|)\
\
半角向量广泛应用于各类关照模型，其中蕴含了很重要的信息（@@至于是什么，不得而知）。\
Blinn-phong光照模型的代码与Phong几乎一样，这里也就不给出了。\

\
\
<http://www.cnblogs.com/bluebean/p/5299358.html> **(两种phong)**\
<http://blog.csdn.net/aquathinker/article/details/8176442>\

[^1]: 2N • L)N - L
