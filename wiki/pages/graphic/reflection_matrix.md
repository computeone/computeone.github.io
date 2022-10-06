反射矩阵（reflection matrix）推导
设平面为(nx,ny,nz,d)，则以此平面为镜面的列主序反射矩阵如下：

推导如下：

一，平面的表示：

如图所示，过点p，法向量为n的平面，可表示为：

np+d=0

其中d为平面到原点的有向距离。如果平面面向原点，则d为正，如果平面背向原点，则d为负。

于是平面可以表示为四维向量（nx,ny,nz,d）。

二，reflection matrix推导：

如图平面为np+d=0，Q为空间任一点，Q\'为Q在平面上的投影，Q\'\'为Q关于平面的对称点，有如下关系：

r=Q-p

a=(rn)n

b=r-a

c=-a

Q\'=p+b

Q\'\'=Q\'+c

np+d=0

综合以上各式，得：

Q\'\'=Q-2(Qn+d)n

写成分量形式即：

Q\'\'x=Qx-2(Qx\*nx+Qy\*ny+Qz\*nz+d)\*nx

Q\'\'y=Qy-2(Qx\*nx+Qy\*ny+Qz\*nz+d)\*ny

Q\'\'z=Qz-2(Qx\*nx+Qy\*ny+Qz\*nz+d)\*nz

整理得：

Q\'\'x=Qx(1-2nx\*nx)+Qy(-2ny\*nx)+Qz(-2nz\*nx)-2d\*nx

Q\'\'y=Qx(-2nx\*ny)+Qy(1-2ny\*ny)+Qz(-2nz\*ny)-2d\*ny

Q\'\'z=Qx(-2nx\*nz)+Qy(-2ny\*nz)+Qz(1-2nz\*nz)-2d\*nz

写成矩阵形式即：

这样就得到了reflection matrix。

unity standard assets里的Water.cs中有下面一段计算reflection
matrix的代码，与上面结果一致： 
```
 // Calculates reflection matrix
around the given plane

          static void CalculateReflectionMatrix(ref Matrix4x4 reflectionMat, Vector4 plane)
          {
              reflectionMat.m00 = (1F - 2F * plane[0] * plane[0]);
              reflectionMat.m01 = (- 2F * plane[0] * plane[1]);
              reflectionMat.m02 = (- 2F * plane[0] * plane[2]);
              reflectionMat.m03 = (- 2F * plane[3] * plane[0]);

              reflectionMat.m10 = (- 2F * plane[1] * plane[0]);
              reflectionMat.m11 = (1F - 2F * plane[1] * plane[1]);
              reflectionMat.m12 = (- 2F * plane[1] * plane[2]);
              reflectionMat.m13 = (- 2F * plane[3] * plane[1]);

              reflectionMat.m20 = (- 2F * plane[2] * plane[0]);
              reflectionMat.m21 = (- 2F * plane[2] * plane[1]);
              reflectionMat.m22 = (1F - 2F * plane[2] * plane[2]);
              reflectionMat.m23 = (- 2F * plane[3] * plane[2]);

              reflectionMat.m30 = 0F;
              reflectionMat.m31 = 0F;
              reflectionMat.m32 = 0F;
              reflectionMat.m33 = 1F;
          }
          


```

