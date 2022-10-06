**Parallax mapping (also called offset mapping or virtual displacement
mapping)** is an enhancement of the bump mapping or normal mapping
techniques applied to textures in 3D rendering applications such as
video games. To the end user, this means that textures such as stone
walls will have more apparent depth and thus greater realism with less
of an influence on the performance of the simulation. Parallax mapping
was introduced by Tomomichi Kaneko et al., in 2001.\[1\]\
\
Parallax mapping is implemented by displacing the texture coordinates at
a point on the rendered polygon by a function of the view angle in
tangent space (the angle relative to the surface normal) and the value
of the height map at that point. At steeper view-angles, the texture
coordinates are displaced more, giving the illusion of depth due to
parallax effects as the view changes.\
\
Parallax mapping described by Kaneko is a single step process that does
not account for occlusion. Subsequent enhancements have been made to the
algorithm incorporating iterative approaches to allow for occlusion and
accurate silhouette rendering.\[2\]\
\
fixed4 frag(v2f i) : SV_Target\
{\
//unity自身的diffuse也是带了环境光，这里我们也增加一下环境光\
fixed3 ambient = UNITY_LIGHTMODEL_AMBIENT.xyz \* \_Diffuse.xyz;\
float2 uvOffset = CaculateParallaxUV(i);\
i.uv += uvOffset;\
//直接解出切线空间法线\
float3 tangentNormal = UnpackNormal(tex2D(\_BumpMap, i.uv));\
//normalize一下切线空间的光照方向\
float3 tangentLight = normalize(i.lightDir);\
//兰伯特光照\
fixed3 lambert = saturate(dot(tangentNormal, tangentLight));\
//最终输出颜色为lambert光强\*材质diffuse颜色\*光颜色\
fixed3 diffuse = lambert \* \_Diffuse.xyz \* \_LightColor0.xyz +
ambient;\

                  //进行纹理采样  \\
                  fixed4 color = tex2D(_MainTex, i.uv);  \\
                  return fixed4(diffuse * color.rgb, 1.0);  \\
              }  \\

\
\
<http://blog.csdn.net/puppet_master/article/details/57125379>
