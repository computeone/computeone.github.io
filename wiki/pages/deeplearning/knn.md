在模式识别领域中，**最近邻居法（KNN算法，又译K-近邻算法）**是一种用于分类和回归的非参数统计方法。\[1\]在这两种情况下，输入包含特征空间中的k个最接近的训练样本。\
\
在k-NN分类中，输出是一个分类族群。一个对象的分类是由其邻居的"多数表决"确定的，k个最近邻居（k为正整数，通常较小）中最常见的分类决定了赋予该对象的类别。若k
= 1，则该对象的类别直接由最近的一个节点赋予。\
在k-NN回归中，输出是该对象的属性值。该值是其k个最近邻居的值的平均值。\
最近邻居法采用向量空间模型来分类，概念为相同类别的案例，彼此的相似度高，而可以借由计算与已知类别案例之相似度，来评估未知类别案例可能的分类。\
K-NN是一种基于实例的学习，或者是局部近似和将所有计算推迟到分类之后的惰性学习。k-近邻算法是所有的机器学习算法中最简单的之一。
无论是分类还是回归，衡量邻居的权重都非常有用，使较近邻居的权重比较远邻居的权重大。例如，一种常见的加权方案是给每个邻居权重赋值为1/
d，其中d是到邻居的距离。\[2\]\
邻居都取自一组已经正确分类（在回归的情况下，指属性值正确）的对象。虽然没要求明确的训练步骤，但这也可以当作是此算法的一个训练样本集。\
k-近邻算法的缺点是对数据的局部结构非常敏感。本算法与K-平均算法（另一流行的机器学习技术）没有任何关系，请勿与之混淆。\
\
**算法流程**

1.  准备数据，对数据进行预处理
2.  选用合适的数据结构存储训练数据和测试元组
3.  设定参数，如k
4.  维护一个大小为k的的按距离由大到小的优先级队列，用于存储最近邻训练元组。随机从训练元组中选取k个元组作为初始的最近邻元组，分别计算测试元组到这k个元组的距离，将训练元组标号和距离存入优先级队列
5.  遍历训练元组集，计算当前训练元组与测试元组的距离，将所得距离L
    与优先级队列中的最大距离Lmax
6.  进行比较。若L\>=Lmax，则舍弃该元组，遍历下一个元组。若L \<
    Lmax，删除优先级队列中最大距离的元组，将当前训练元组存入优先级队列。
7.  遍历完毕，计算优先级队列中k
    个元组的多数类，并将其作为测试元组的类别。
8.  测试元组集测试完毕后计算误差率，继续设定不同的k值重新进行训练，最后取误差率最小的k
    值。\[1\]