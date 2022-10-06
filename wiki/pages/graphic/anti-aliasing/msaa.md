**多重采样抗锯齿**\
\
多重采样抗锯齿（MultiSampling
Anti-Aliasing，简称MSAA）是一种特殊的超级采样抗锯齿（SSAA）。MSAA首先来自于OpenGL。具体是MSAA只对Z缓存（Z-Buffer）和模板缓存（Stencil
Buffer）中的数据进行超级采样抗锯齿的处理。可以简单理解为只对多边形的边缘进行抗锯齿处理。这样的话，相比SSAA对画面中所有数据进行处理，MSAA对资源的消耗需求大幅减少，不过在画质上可能稍有不如SSAA。\
这是最常见的反锯齿，差不多所有游戏都支持MSAA。\
