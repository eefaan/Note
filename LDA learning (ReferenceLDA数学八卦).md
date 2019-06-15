# LDA learning (Reference:LDA数学八卦)

## 1 基础函数

### 1.1 Gamma函数与Gamma分布

​	Gamma函数：
$$
\Gamma(x)=\int_0^\infty t^{x-1}e^{-t}dt
$$
​	其定义满足：
$$
\Gamma(x)=(n-1)!
$$
​	note：选择该定义的原因可能是如此定义后，其与后出现的Beta函数有如下关系：$\Beta(m,n)=\frac{\Gamma(m)\Gamma(n)}{\Gamma(m+n)}$，Gamma函数使得(1/2)!的计算具有意义，拓展了其他概念诸如分数阶的导数运算。Gamma函数与黎曼函数$\zeta(s)$有密切联系，而$\zeta(s)$又涉及了黎曼猜想和素数分布定理。

​	Gamma函数在概率统计中出现频繁，包括常见的统计学三大分布(t分布，$\chi^2$分布，$F$分布)、Beta分布、Dirichlet分布的密度公式种都有Gamma函数的身影。当然最直接联系的概率分布是直接由Gamma函数变换得到的Gamma分布。Gamma分布的一般形式：
$$
Gamma(t|\alpha,\beta)=\frac{\beta^\alpha t^{\alpha-1}e^{-\beta t}}{\Gamma(\alpha)}
$$
​	其中$\alpha$称为shape parameter，主要决定了分布曲线的形状；而$\beta$称为rate parameter或者inverse scale parameter($\frac{1}{\beta}$称为scale parameter)，主要决定曲线有多陡。

​	以下主要关注$\beta=1$的Gamma分布。

### 1.2 二项分布联系Gamma分布与Poisson分布

​	首先容易发现Gamma分布的概率密度和Poisson分布在数学形式上具有高度的一致性：参数为$\lambda$的Poisson分布，概率写为
$$
Poisson(X=k|\lambda)=\frac{\lambda ^k e^{-\lambda}}{k!}
$$
在Gamma分布的密度中取$\alpha=k+1$得到
$$
Gamma(x|\alpha =k+1)=\frac{x^ke^{-x}}{\Gamma(k+1)}=\frac{x^ke^{-x}}{k!}
$$
所以两个分布在数学形式上是一致的，只是Poisson分布是离散的，Gamma分布是连续的，可以直观的认为Gamma分布是Poisson分布在正实数集上的连续化版本。

​	另外从二项分布出发，能够得到：
$$
Poisson(X\leq k|\lambda)+\int_0^\lambda \frac{x^ke^{-x}}{k!}dx=1
$$
可以看到Poisson分布的概率累积函数和Gamma分布的概率累积函数有互补的关系。

### 1.3 Beta分布与Dirichlet分布 

​	网站链接：[Beta分布Demo](http://www.aiaccess.net/English/Glossaries/GlosMod/e_gm_beta_distri.htm)

​	Beta分布可以是凹的、凸的、单调上升、下降、直线或曲线，均匀分布也是特殊的Beta分布。由于Beta分布能够你和如此之多的形状，其在统计数据拟合和贝叶斯分析中被广泛使用。

​	以Algorithm为例理解分布：

​	1.Beta分布：$X_{1...n}$~$Uniform(0,1)$，n个随机变量排序后，$X_{(k)}$的分布？

​	2.Beta-Binomial共轭：$X_{1...n}$~$Uniform(0,1)$，n个随机变量排序后，猜测$p=X_{(k)}$？同时：$Y_{1...n}$~$Uniform(0,1)$，其中$m_1$个比$p$小$m_2$个比$p$大。$P(p|Y_1,Y_2,\cdots,Y_m)$的分布？

​	3.Dirichlet-Multinomial共轭：$X_{1...n}$~$Uniform(0,1)$，n个随机变量排序后，$(X_{(k)},X_{(k_1+k_2)})$的联合分布？

​	对于Beta分布，均值可以用$\frac{\alpha}{\alpha+\beta}$来估计。Dirichlet分布也有类似的结论。

##2 MCMC和Gibbs Sampling

​	随机模拟又叫蒙特卡罗方法(Monte Carlo Simulation)。

​	统计模拟的一个重要问题：给定一个概率分布$p(x)$，如何在计算机中生成他的样本。一般而言基于均匀分布$Uniform(0,1)$，无论是连续还是离散的分布，都可以生成。但当$p(x)$的形式很复杂或是高纬分布时，就需要使用一些更加复杂的随机模拟方法来生成样本，例如MCMC(Markov Chain Monte Carlo)和Gibbs Sampling算法就是最常用的一种，这两个方法在现代贝叶斯分析中被广泛使用。

###2.1 马氏链及其平稳分布

## 3 文本建模

###3.1 Unigram Model

###3.2 Topic Model和PLSA



## 4 LDA文本建模

