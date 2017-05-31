线性回归可以说是机器学习中最基本的问题类型了，这里就对线性回归的原理和算法做一个小结。

# 1. 线性回归的模型函数和损失函数

线性回归遇到的问题一般是这样的。我们有m个样本，每个样本对应于n维特征和一个结果输出，如下：

$$(x^{(0)}_1,x^{(0)}_2,...x^{(0)}_n,y_0),(x^{(1)}_1,x^{(1)}_2,...x^{(1)}_n,y_1),...(x^{(m)}_1,x^{(m)}_2,...x^{(m)}_n,y_n)$$

我们的问题是，对于一个新的$$x = y$$, 他所对应的$$y_x$$是多少呢？ 如果这个问题里面的y是连续的，则是一个回归问题，否则是一个分类问题。

对于n维特征的样本数据，如果我们决定使用线性回归，那么对应的模型是这样的：

$$h_\theta (x_1,x_2,...x_n)=\theta_0+\theta_1x_1+...+\theta_nx_n$$, 其中$$\theta_i(i=0,1,2....n)$$为模型参数，$$x_i(i=0,1,2....n)$$为每个样本的n个特征值。这个表示可以简化，我们增加一个特征$$x_0=1$$，这样$$h_\theta (x_0,x_1,...x_n)=\sum_{i=0}^{n}\theta_ix_i$$。

进一步用矩阵形式表达更加简洁如下：

$$h_\theta(X)=X\theta$$

其中， 假设函数$$h_\theta(X)$$为mx1的向量,θ为nx1的向量，里面有n个代数法的模型参数。X为mxn维的矩阵。m代表样本的个数，n代表样本的特征数。

得到了模型，我们需要求出需要的损失函数，一般线性回归我们用均方误差作为损失函数。损失函数的代数法表示如下：

$$J(\theta_0,\theta_1....,\theta_n)=\sum_{i=0}^{m}(h_\theta(x_0,x_1,...x_n)-y_i)^2$$

进一步用矩阵形式表达损失函数：

$$J(\theta)=\frac{1}{2}(X\theta-Y）^T(X\theta-Y)$$

由于矩阵法表达比较的简洁，后面我们将统一采用矩阵方式表达模型函数和损失函数。

# 2. 线性回归的算法

对于线性回归的损失函数J\(θ\)=12\(Xθ−Y\)T\(Xθ−Y\)J\(θ\)=12\(Xθ−Y\)T\(Xθ−Y\)，我们常用的有两种方法来求损失函数最小化时候的θθ参数：一种是[**梯度下降法**](http://www.cnblogs.com/pinard/p/5970503.html)，一种是[**最小二乘法**](http://www.cnblogs.com/pinard/p/5976811.html)。由于已经在其它篇中单独介绍了梯度下降法和最小二乘法，可以点链接到对应的文章链接去阅读。

如果采用梯度下降法，则θθ的迭代公式是这样的：

θ=θ−αXT\(Xθ−Y\)θ=θ−αXT\(Xθ−Y\)

通过若干次迭代后，我们可以得到最终的θθ的结果

如果采用最小二乘法，则θθ的结果公式如下：

θ=\(XTX\)−1XTYθ=\(XTX\)−1XTY

当然线性回归，还有其他的常用算法，比如牛顿法和拟牛顿法，这里不详细描述。

# 3. 线性回归的推广：多项式回归

回到我们开始的线性模型，hθ\(x1,x2,...xn\)=θ0+θ1x1+...+θnxnhθ\(x1,x2,...xn\)=θ0+θ1x1+...+θnxn, 如果这里不仅仅是x的一次方，比如增加二次方，那么模型就变成了多项式回归。这里写一个只有两个特征的p次方多项式回归的模型：

hθ\(x1,x2\)=θ0+θ1x1+θ2x2+θ3x21+θ4x22+θ5x1x2hθ\(x1,x2\)=θ0+θ1x1+θ2x2+θ3x12+θ4x22+θ5x1x2

我们令x0=1,x1=x1,x2=x2,x3=x21,x4=x22,x5=x1x2x0=1,x1=x1,x2=x2,x3=x12,x4=x22,x5=x1x2,这样我们就得到了下式：

hθ\(x1,x2\)=θ0+θ1x1+θ2x2+θ3x3+θ4x4+θ5x5hθ\(x1,x2\)=θ0+θ1x1+θ2x2+θ3x3+θ4x4+θ5x5

可以发现，我们又重新回到了线性回归，这是一个五元线性回归，可以用线性回归的方法来完成算法。对于每个二元样本特征\(x1,x2\)\(x1,x2\),我们得到一个五元样本特征\(1,x1,x2,x21,x22,x1x2\)\(1,x1,x2,x12,x22,x1x2\)，通过这个改进的五元样本特征，我们重新把不是线性回归的函数变回线性回归。

# 4. 线性回归的推广：广义线性回归

在上一节的线性回归的推广中，我们对样本特征端做了推广，这里我们对于特征y做推广。比如我们的输出YY不满足和XX的线性关系，但是lnYlnY和XX满足线性关系，模型函数如下：

lnY=XθlnY=Xθ

这样对与每个样本的输入y，我们用 lny去对应， 从而仍然可以用线性回归的算法去处理这个问题。我们把 Iny一般化，假设这个函数是单调可微函数g\(.\)g\(.\),则一般化的广义线性回归形式是：

g\(Y\)=Xθg\(Y\)=Xθ或者 Y=g−1\(Xθ\)Y=g−1\(Xθ\)

这个函数g\(.\)g\(.\)我们通常称为联系函数。

# 5. 线性回归的正则化

为了防止模型的过拟合，我们在建立线性模型的时候经常需要加入正则化项。一般有L1正则化和L2正则化。

线性回归的L1正则化通常称为Lasso回归，它和一般线性回归的区别是在损失函数上增加了一个L1正则化的项，L1正则化的项有一个常数系数αα来调节损失函数的均方差项和正则化项的权重，具体Lasso回归的损失函数表达式如下：

J\(θ\)=12n\(Xθ−Y\)T\(Xθ−Y\)+α\|\|θ\|\|1J\(θ\)=12n\(Xθ−Y\)T\(Xθ−Y\)+α\|\|θ\|\|1

其中n为样本个数，αα为常数系数，需要进行调优。\|\|θ\|\|1\|\|θ\|\|1为L1范数。

Lasso回归可以使得一些特征的系数变小，甚至还是一些绝对值较小的系数直接变为0。增强模型的泛化能力。

Lasso回归的求解办法一般有坐标轴下降法（coordinate descent）和最小角回归法（ Least Angle Regression），由于它们比较复杂，在我的这篇文章单独讲述： [线程回归的正则化-Lasso回归小结](http://www.cnblogs.com/pinard/p/6018889.html)

线性回归的L2正则化通常称为Ridge回归，它和一般线性回归的区别是在损失函数上增加了一个L2正则化的项，和Lasso回归的区别是Ridge回归的正则化项是L2范数，而Lasso回归的正则化项是L1范数。具体Ridge回归的损失函数表达式如下：

J\(θ\)=12\(Xθ−Y\)T\(Xθ−Y\)+12α\|\|θ\|\|22J\(θ\)=12\(Xθ−Y\)T\(Xθ−Y\)+12α\|\|θ\|\|22

其中αα为常数系数，需要进行调优。\|\|θ\|\|2\|\|θ\|\|2为L2范数。

Ridge回归在不抛弃任何一个特征的情况下，缩小了回归系数，使得模型相对而言比较的稳定，但和Lasso回归比，这会使得模型的特征留的特别多，模型解释性差。

Ridge回归的求解比较简单，一般用最小二乘法。这里给出用最小二乘法的矩阵推导形式，和普通线性回归类似。

令J\(θ\)J\(θ\)的导数为0，得到下式：

XT\(Xθ−Y\)+αθ=0XT\(Xθ−Y\)+αθ=0

整理即可得到最后的θθ的结果：

θ=\(XTX+αE\)−1XTYθ=\(XTX+αE\)−1XTY

其中E为单位矩阵。
