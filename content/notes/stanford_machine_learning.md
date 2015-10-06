Title: Machine Learning
Date: 2015-08-29 20:20
Modified: 2015-08-29 20:20
Slug: machine-learning
Authors: Joey Huang
Summary: Notes of Stanford Machine Learning, by Andrew Ng, on www.coursera.org
Status: draft

[TOC]

## 机器学习

课程在 [Coursera][1] 上, 讲师是 Andrew Ng。PDF 格式的课件在 [Stanford 网站][2]上。课程讨论组在[这里][3]可以找到。

## Week 1 机器学习介绍

### What is Machine Learning?

Two definitions of Machine Learning are offered. Arthur Samuel described it as: "the field of study that gives computers the ability to learn without being explicitly programmed." This is an older, informal definition.

Tom Mitchell provides a more modern definition: "A computer program is said to learn from experience E with respect to some class of tasks T and performance measure P, if its performance at tasks in T, as measured by P, improves with experience E."

Example: playing checkers.

* E = the experience of playing many games of checkers
* T = the task of playing checkers.
* P = the probability that the program will win the next game.

### Supervised learning

> In supervised learning, we are given a data set and already know what our correct output should look like, having the idea that there is a relationship between the input and the output.

> Supervised learning problems are categorized into "regression" and "classification" problems. In a regression problem, we are trying to predict results within a continuous output, meaning that we are trying to map input variables to some continuous function. In a classification problem, we are instead trying to predict results in a discrete output. In other words, we are trying to map input variables into discrete categories.

1. Supervised learning: 结果形式己知的机器学习。比如，从过往销售数据，预测未来三个月的销售数据。
1. Classfication learning: 输出结果是离散的。
2. Regression learning: 输出结果是连续的。

### Unsupervised learning

> Unsupervised learning, on the other hand, allows us to approach problems with little or no idea what our results should look like. We can derive structure from data where we don't necessarily know the effect of the variables.

> With unsupervised learning there is no feedback based on the prediction results, i.e., there is no teacher to correct you. It’s not just about clustering.

数据挖掘，从给定的数据集合里去发现规律，进行模式匹配。结果形式不可知。计算结果无法对数据进行反馈。

**例子：声音处理**
从一个有背景音乐的吵杂的会议中演讲的录音文件中，通过数据挖掘和特征匹配来处理这段录音，最终分离出演讲录音和音乐。

* Supervised learning: Given email labed as spam/not spam; learn a email filter.
* Unsupervised learning: Given as set of news articles found on web, group them as a set of articles about the same story.
* Unsupervised learning: Given a set of customer data, automatically discover the market segment and group customers into different market segment.
* Supervised learning: Given a dataset of patients diagnosed as either having diabets or not, learn to classify new patients as having diabets or not.

### 线性回归算法

* Cost Function: 成本函数，用来测量模型的准确度。成本函数把把建模问题转换为求成本函数的极小值。
* Contour plots: 等高线。多参数的成本函数里，有一组参数的值会有相同的成本。这些参数联接起来就是成本函数的等高线。
* Gradient Descent: 阶梯下降，假设的模型逐步逼近真实数据的过程

REF:
1. [Linear Regression with One Variable][4]
2. [Partial derivative in gradient descent for two variables][5]

根据上面两个链接推导出阶梯下降函数。

### 数学

* [微积分][5] 四个最简单的规则
	* 针对 $F(x) = cx^n$，其导函数是 $F'(x) = cn\times{x^{(n-1)}}$
	* 常数的导数是 0
	* 导函数可以穿透累加器，即 $\displaystyle\frac{\partial}{\partial x_0}\sum_{i=0}^nF(x_i) = \sum_{i=0}^n\frac{\partial}{\partial x_0}F(x_i)$
	* 微分传导机制，即$\displaystyle\frac{\partial}{\partial x}g(f(x)) = g'(f(x))\times f'(x)$
* [线性代数][6]
* [最小二阶乘数拟合数据][7]
* 概率论复习

### 术语

* Calculus: 微积分
* Partial derivatives: 偏导数
* Derivatives: 导数
* Gradient Descent: 梯度下降
* Cost Function: 成本函数
* Contour plots: 等高线
* Least Mean Squares: LSM, 最小均方

### TODO

* 使用 markdown + MathJax 来书写数学公式
    * [MathJax 简明中文教程][13] 这是一个质量很高的博客文章
    * [LaTex 教程][8]
    * [LaTex 支持的所有符号列表][9]
* 推导出模型参数的梯度下降公式 (Gradient Descent)
* 推导出 LSM (Widrow-Hoff学习算法)

## Week 2 多变量梯度下降算法

### 多变量梯度下降算法

预测函数：
$$
h(\theta) = \theta_0 + \theta_1 x_1 + \theta_2 x_2 + ... + \theta_n + x_n = \theta^T x^{(i)}
$$
其中，$x_0 = 1$，$x^{(i)}$ 是训练数据集里的第 i 个数据。$\theta_T$ 是 n + 1 维列向量；$x^{(i)}$ 是 n + 1 维行向量。

成本函数：
$$
J(\theta) = \frac{1}{2m} \sum_{(i=0)}^n \left( h_\theta(x^{(i)}) - y^{(i)} \right)^2
$$

迭代函数：
$$
\theta_j = \theta_j - \alpha \frac{1}{m} \sum_{i=0}^m \left(\left(h(x^{(i)}) - y^{(i)}\right) x_j^{(i)}\right)
$$

### 变量缩放 Feature Scaling

当变量在 [-1, 1] 这个范围内时，梯度下降算法能较快地收敛。可以使用下面的公式来缩放变量，以让变量在快速收敛的范围内：

$$
x_i := \frac{x_i - \mu_i}{s_i}
$$

其中，$\mu_i$ 是 $x_i$ 的平均值，即 $\mu_i = \frac{1}{n} \sum_{i=1}^n x_i$， $s_i$ 是 $x_i$ 的范围，即 $s_i = max(x_i) - min(x_i)$。

经过这样的转换，变量的范围全部落在 [-0.5, 0.5] 之间。

### 学习率

使用 $\alpha$ 来表示学习率，值太高会导致无法收敛，太低收敛又太慢。一个好的办法是画出成本函数 $J(\theta)$ 随着迭代次数不断变化的曲线。这样可以直观地观察到随着迭代地不断进行，成本函数的值的变化情况。在实际情况中，可以从几个经验值里去偿试，比如 0.0001, 0.0003, 0.001, 0.003, 0.01, 0.03, 0.1, 0.3, 1。


### 标准方程 Normal Equalation

通过微分公式可以知道，我们要求成本函数 $J(\theta)$ 的最小值，只需要令其偏导数为零，即：
$$
\frac\partial{\partial{\theta_j}}J(\theta) := 0
$$

把 $J(\theta)$ 用矩阵来表示，并根据矩阵运算定律最终可以推导出下面的方程式：

$$
\theta = \left( X^T X \right)^{-1} X^T y
$$

推导过程可参阅 [cs229-notes1.pdf][10]。推导过程会用到大量的矩阵运算知识。其中 X 是训练数据集，y 是结果数据向量。这样我们就可以通过直接计算的方式，而不是线性回归的方式来求得参数 $\theta$ 的值。


### Octave 教程

#### Octave 基本教程

可以和 numpy, scipy 等结合起来学习。实际上接口较为类似。

#### 向量化

向量化可以让代码运算更简洁，效率更高。比如，我们的预测函数的普通形式可以写成：

$$
h_\theta(x) = \sum_{i=0}^{n} \theta_ix^{(i)}
$$

那么其 Octave 代码如下：

```matlab
prediction = 0.0
for i=1:n+1,
    prediction = predicition + theta(i) * x(i)
end;
```

我们也可以把预测函数向量化：

$$
h_\theta(x) = \theta^T x
$$

这样，我们的预测函数可以实现如下：

```matlab
prediction = theta' * x
```

另外一个例子是梯度下降算法里的参数迭代函数：

$$
\theta_j = \theta_j - \alpha \frac{1}{m} \sum_{i=1}^{m} \left( h_\theta(x^{(i)}) -y^{(i)} \right) x_j^{(i)}
$$

我们可以向量化为：

$$
\theta = \theta - \alpha \delta
$$

其中，$\theta$ 是个 n + 1 维向量；$\alpha$ 是一个标量；$\delta$ 是一个 n + 1 维向量。$\delta$ 可以向量化为：

$$
\delta = \frac{1}{m} \sum_{i=1}^{m} \left( h_\theta(x^{(i)}) - y^{(i)} \right) x^{(i)}
$$

其中，$\left( h_\theta(x^{(i)}) - y^{(i)} \right)$ 是个标量；$x^{(i)}$ 是个 n + 1 维向量，其行元素为 $x^{(i)}_0, x^{(i)}_1, x^{(i)}_2 ... x^{(i)}_n$，其上标为第 i 项训练样例数据，下标为第 j 项变量；而 m 项求和，实际上可以看成是一个线性方程组的表达形式。

#### 标准方程和奇异矩阵

$$
\theta = (X^T X)^{-1} X^T y
$$

这是我们的通用方程，当训练数据集较少时，利用矩阵运算可以较快的算出参数 $\theta$ 的值。但如果 $X^T X$ 是奇异矩阵的话，它就没有逆矩阵存在，这个时候通用方程的解是什么呢？答案是，在 octave 里用 `pinv` 来代替 `inv` 来计算逆矩阵。这样即使 $X^T X$ 是奇异矩阵，`pinv` 也能算出其"伪"逆矩阵，从而顺利算出通用方向的解。

那么，物理上讲，$X^T X$ 如果为奇异矩阵的话，到底代表什么意思呢？

* 模型变量之间线性相关
  比如，在房价预测模型里，$x_1$ 代表房子的长度，$x_2$ 代表房子的宽度，而 $x_3$ 代表房子的面积，这里假设房子是方形的，那么实际上 $x_3$ 和 $x_1, x_2$ 是线性相关的。
* 训练样例少于变量个数，即 m < n
  这种情况下，需要减少变量个数来解决问题

### TODO

1. 如何从数学上证明变量绽放后能较快收敛？
2. 可以使用 `pylab` 的等高线在二维平面上画出成本函数和两个参数的关系图
3. 找一个数据集，选择不同的学习率来实现，画出不同学习率时的成本函数随着迭代次数的变化情况
4. 总结 matlab/octave 和 scipy/numpy 在数值计算上的差异和优缺点

## Week 3 分类回归算法 Logistic Regression

### 分类预测函数及其表现形式 Classification and Representation

#### 引言 为什么需要分类回归算法

分类问题的值是离散的，如果考虑二元分类总是，则其值是 0 或 1。如果用 linear regresstion 来作为分类问题的预测函数是不合理的。因为因为预测出来的数值可能远小于 0 或远大于 1。我们需要找出一个预测函数模型，使其值的输出在 [0, 1] 之间。

#### 逻辑回归预测函数的表现形式 Hypothesis Representation

**逻辑回归预测函数**

线性回归算法的预测函数是 $h_\theta(x) = \theta^T x$，为了让预测函数的输出值在 [0, 1] 之间，我们给定逻辑回归模型 (Logistic Regression Model) $g(z) = \frac{1}{1 + e^{-z}}$，则我们的逻辑回归模型的预测函数如下：

$$
h_\theta(x) = g(\theta^T x) = \frac{1}{1 + e^{-\theta^T x}}
$$

**解读逻辑回归预测函数的输出值**

$h_\theta(x)$ 表示针对输入值 $x$ 以及参数 $\theta$ 的前提条件下，$y=1$ 的概率。用概率论的公式可以写成：

$$
h_\theta(x) = P(y=1 \vert x; \theta)
$$

上面的概率公式可以读成：**在输入 $x$ 及参数 $\theta$ 条件下 $y=1$ 的概率**。由概率论的知识可以推导出，

$$
P(y=1 \vert x; \theta) + P(y=0 \vert x; \theta) = 1
$$

#### 判定边界 Decision Boundary

**从逻辑回归公式说起**

逻辑回归预测函数由下面两个公式给出的：

$$
h_\theta(x) = g(\theta^T x)
$$

$$
g(z) = \frac{1}{1 + e^{-z}}
$$

假定 $y=1$ 的判定条件是 $h_\theta(x) \geq 0.5$，$y=0$ 的判定条件是 $h_\theta(x) < 0.5$，则我们可以推导出 $y=1$ 的判定条件就是 $\theta^T x \geq 0$，$y=0$ 的判定条件就是 $\theta^T x < 0$。所以，$\theta^T x = 0$ 即是我们的判定边界。

**判定边界**

假定我们有两个变量 $x_1, x_2$，其逻辑回归预测函数是 $h_\theta(x) = g(\theta_0 + \theta_1 x_1 + \theta_2 x_2)$。假设我们给定参数

$$
\theta = \begin{bmatrix} -3 \\\\ 1 \\\\ 1 \end{bmatrix}
$$

那么我们可以得到判定边界 $-3 + x_1 + x_2 = 0$，即 $x_1 + x_2 = 3$，如果以 $x_1$ 为横坐标，$x_2$ 为纵坐标，这个函数画出来就是一个通过 (0, 3) 和 (3, 0) 两个点的斜线。这条线就是我们的判定边界。

**非线性判定边界**

如果预测函数是多项式 $h_\theta(x) = g(\theta_0 + \theta_1 x_1 + \theta_2 x_2 + \theta_3 x_1^2 + \theta_4 x_2^2)$，且给定 $\theta^T = \left[ -1 0 0 1 1\right]$，则可以得到判定边界函数

$$
x_1^2 + x_2^2 = 1
$$

还是以 $x_1$ 为横坐标，$x_2$ 为纵坐标，则这是一个半径为 1 的圆。这是二阶多项式的情况，更一般的多阶多项式可以表达出更复杂的判定边界。

### 逻辑回归的成本函数

线性回归的成本函数是 $J(\theta) = \frac{1}{m} \sum_{i=1}^m \frac{1}{2} \left (h_\theta(x^{(i)}) - y^{(i)} \right)^2 $，如果我们按照线性回归的成本函数来计算逻辑回归的成本函数，那么我们最终会很可能会得到一个非凸函数 (non-convex function)，这样我们就无法通过梯度下降算法算出成本函数的最低值。

为了让成本函数是个凸函数 (convex function)，以便容易求出成本函数的最小值，我们定义逻辑回归的成本函数如下：

$$
Cost(h_\theta(x), y) = \begin{cases}
    -log(h_\theta(x)), & \text{if $y$ = 1} \\\\
    -log(1 - h_\theta(x)), & \text{if $y$ = 0} \\\\
\end{cases}
$$

**成本函数的解读**
如果 $y = 1, h_\theta(x) = 1$，那么成本为 $Cost = 0$；如果 $y = 1, h_\theta(x) \rightarrow 0$，那么成本将是无穷大 $Cost \rightarrow \infty$。
如果 $y = 0, h_\theta(x) = 0$，那么成本为 $Cost = 0$；如果 $y = 0, h_\theta(x) \rightarrow 1$，那么成本将是无穷大 $Cost \rightarrow \infty$。

#### 逻辑回归成本函数定义

由于 $y \in [0, 1]$ 的离散值，可以把两个成本函数合并起来：

$$
J(\theta) = -\frac{1}{m} \left[ \sum_{i=1}^m log(h_\theta(x^{(i)})) + (1 - y^{(i)}) log(1 - h_\theta(x^{(i)})) \right]
$$

把 $y = 0, y = 1$ 两种情况代入上式，很容易可以验证成本函数合并的等价性。使用梯度下降算法进行参数迭代的公式如下：

$$
\begin{align}
\theta_j & = \theta_j - \alpha \frac\partial{\partial{\theta_j}}J(\theta) \\\\
& =  \theta_j - \alpha \frac{1}{m} \sum_{i=1}^m \left( h_\theta(x^{(i)}) - y^{(i)} \right) x_j^{(i)}
\end{align}
$$

这个公式的形式和母性回归算法的参数迭代公式是一样的。当然，由于这里 $h_\theta(x) = \frac{1}{1 + e^{-\theta^T x}}$，而线性回归算法里 $h_\theta(x) = \theta^T x$。所以，两者的形式一样，但数值计算完全不同。

### 算法优化

梯度下降算法的效率是比较低，优化的梯度下降算法有 Conjugate Gradient, BFGS, L-BFGS 等。这些算法比较复杂，实现这些算法是数值计算专家的工作，一般工程人员只需要大概知道这些算法是怎么优化的以及怎么使用这些算法即可。

octave 里提供了 `fminunc` 函数，可以查阅文档来学习函数用法，从而学会使用优化过的梯度下降算法，以提高计算效率。

### 多元分类算法

除了二元分类算法外，还有多元分类问题，比如需要给邮件打标签，则可能有多个标签需要考虑。这个时候需要使用 one-vs-all (one-vs-rest) 的方法。即把要分类的一种类别和其他所有类别区分开来的，这样就把多元分类问题转化为二元分类问题，这样就可以使用上文总结的所有二元分类问题的算法。

针对 $y = i$，求解针对 i 的预测函数 $h_\theta^{(i)}(x)$。如果有 n 个类别，则需要求解 n 个预测函数。

### 正则化 Regularization

#### 线性回归里的欠拟合和过拟合

* 欠拟合 (underfitting)
  使用的变量过少导致成本函数过高。
* 过拟合 (overfitting)
  使用多个变量建模的预测函数非常完美地拟合了数据，其成本函数的值接近于零，但无法对新的实例进行良好的预测。

**变量太多，而训练样本数据太少，则很可能出现过拟合**。下面是一些解决过拟合问题的方法：

* 减少变量个数
    * 手动减少变量个数
    * 模型选择算法
* 正则化
    * 保留所有的变量，去所有变量的权重 $\theta_j$ 的值
    * 当每个变量 $x_i$ 对预测值 $y$ 都有少量的贡献时，这样的模型可以良好地工作

这就是正则化的目的，为了解决变量过多时的过拟合问题。

#### 正则化

$$
J(\theta) = \frac{1}{2m} \left[ \sum_{i=1}^m \left( h_\theta(x^{(i)}) - y^{(i)} \right)^2 + \lambda \sum_{j=1}^n \theta_j^2 \right]
$$

其中 $\lambda$ 的值有两个目的，即要维持对训练样本的拟合，又避免对训练样本的过拟合。如果 $\lambda$ 太大，则能确保不出现过拟合，但可能会导致对现有训练样本出现欠拟合。

利用正则化的成本函数，可以推导出参数迭代函数：

$$
\begin{align}
\theta_j & = \theta_j - \alpha \frac{1}{m} \sum_{i=1}^m \left[ \left(\left(h(x^{(i)}) - y^{(i)}\right) x_j^{(i)}\right) + \frac{\lambda}{m} \theta_j \right] \\\\
& = \theta_j (1 - \alpha \frac{\lambda}{m}) - \alpha \frac{1}{m} \sum_{i=1}^m \left(\left(h(x^{(i)}) - y^{(i)}\right) x_j^{(i)}\right)
\end{align}
$$

$(1 - \alpha \frac{\lambda}{m})$ 因子在每次迭代时都将把 $\theta_j$ 收缩。因为 $\alpha$ 和 $\lambda$ 是正数，而 m 是训练样例的个数，是个比较大的正整数。

#### 通用方程的正则化

$$
\theta = (X^T X)^{-1} X^T y
$$

这是还没有正则化的通用方程，我们用它来快速求解。

$$
\theta = (X^T X + \lambda Z)^{-1} X^T y
$$

其中，Z 是 (n + 1) x (n + 1) 矩阵

$$
Z =
\begin{bmatrix}
0 \\\\
& 1 \\\\
& & 1 \\\\
& & & \ddots \\\\
& & & & 1
\end{bmatrix}
$$

正则化的通用方程实际上解决了两个问题。一个是确保不发生过拟合，另外一个也解决了 $X^T X$ 的奇异矩阵问题。当 m < n 时，$X^T X$ 将是一个奇异矩阵，使用 octave 里的 `pinv` 函数我们可以求出近似逆矩阵的值，但如果在其他编程语言里，是没有办法求出奇异矩阵的逆矩阵的。而从数学上可以证明，加上 $\lambda Z$ 后，结果将是一个非奇异矩阵。

通用方程的正则化公式推导过程复杂，过程从略。

#### 逻辑回归成本函数的正则化

$$
J(\theta) = -\frac{1}{m} \left[ \sum_{i=1}^m log(h_\theta(x^{(i)})) + (1 - y^{(i)}) log(1 - h_\theta(x^{(i)})) \right] + \frac{\lambda}{2m} \sum_{j=1}^n \theta_j^2
$$

相应地，正则化后的参数迭代公式


$$
\begin{align}
\theta_j & = \theta_j - \alpha \frac\partial{\partial{\theta_j}}J(\theta) \\\\
& = \theta_j - \alpha \left[ \frac{1}{m} \sum_{i=1}^m \left( h_\theta(x^{(i)}) - y^{(i)} \right) x_j^{(i)} + \frac{\lambda}{m} \theta_j \right] \\\\
& = \theta_j (1 - \alpha \frac{\lambda}{m}) - \alpha \frac{1}{m} \sum_{i=1}^m \left(\left(h(x^{(i)}) - y^{(i)}\right) x_j^{(i)}\right)
\end{align}
$$

需要注意的是，上式中 $j \geq 1$，因为 $\theta_0$ 没有参与正则化。另外需要留意，逻辑回归和线性回归的参数迭代算法看起来形式是一样的，即公式 (4) 和公式 (7) 形式一样，但其实他们的算法是不一样的，因为两个式子的预测函数 $h_\theta(x)$ 是不一样的。针对线性回归，$h_\theta(x) = \theta^T x$，而针对逻辑回归 $h_\theta(x) = \frac{1}{1 + e^{-\theta^T x}}$。

根据正则化的，新的成本函数的参数迭代函数来实现 CostFunction，然后利用 octave 里的 `fminunc` 函数来求解，这样可以达到最高的运算效率。因为 `fminunc` 会使用优化过的梯度下降算法 Conjugate Gradient, BFGS, L-BFGS 等来提高运算效率。

> 学到这里，你基本上可以使用线性回归逻辑回归解决一些现实问题了。我看到硅谷有大量的公司使用机器算法来构建伟大的产品，那些机器学习工程师在这些公司获得了很好的职业发展并且赚了不少钱。--- Andrew Ng

老师除了教得好，还要会鼓励，让学生保持学习的热情和兴趣。学完三周，瞬间高大上了，可以走上硅谷机器学习工程师的职业道路了~~。我的看法是，学到了不少知识，但依然任重道远。

### TODO

1. 使用 pylab/octave 画出逻辑回归预测函数的图形
2. 是否有类似 MathJax 类似的，使用 JavaScript 来在网页上画图的库呢？[这里][12]有个相似的问题。
3. 复习[概率论][11]基础知识
4. 使用 pylab/octave 画出逻辑回归成本函数的图形
5. 复习微积分知识，推导出逻辑回归算法的参数迭代函数
6. 理解 Conjugate Gradient, BFGS, L-BFGS 的原理
7. 查阅 octave 文档学习 `fminunc` 函数以及 scipy 里对应的函数
8. 通用方程的正则化的数学推导过程


## Week 4 神经网络表示 Neural Networks: Presentation

### 动机 Motivations

为什么我们需要神经网络？

对非线性分类问题，当特征的个数很大的时候，计算量将会非常大。比如对有 100 个特征（$x_1, x_2, \cdots, x_100$）的问题，如果我们只算二阶多项多项式，我们将得到大概 5000 个特征 ($O(n^2)$)。而如果按照三阶多项式来模拟，将得到将近 300,000 个特征 ($O(n^3)$)。再比如，针对一个 100 x 100 分辨率的图片，我们假设每个象素点只用黑白来表示，那么将得到 100,000 个特征值。这个时候如果用二阶多项式来拟合，我们将得到 50,000,000,000 个特征值组合。这是非常巨大的计算量。

显然，用线性回归和逻辑回归来解决这类问题是不现实的。

### 神经网络模型

神经网络模型是依照大脑的神经网络的结构建模的。即多个神经元构成一个层，这些神经元是输入，层的目标值为输出。一个神经网络包含多个层。神经元是神经网络中的运算单位。

#### 神经元

神经元是神经网络中的最小运算单位，多个神经元构成一个层。神经网络依然使用概率回归里介绍的 Sigmoid Function 作为基本模型。

$$
g(z) = \frac{1}{1 + e^{-z}} \\\\
z = \theta^T x \\\\
h_\theta(x) = \frac{1}{1 + e^{-\theta^T x}}
$$

其中，$x$ 称作神经元的输入 (input wires or Dendrite)，是个列向量 $[x_1, x_2, ... x_n]$。$\theta$ 称为权重 (weights)，也可以类似逻辑回归里称为参数 (parameters)。$h_\theta(x)$ 称为输出 (output wires or Axon)。这个是神经网络模型中的基本运算单元。

类似逻辑回归，我们也会增加一个输入 $x_0$，在这里称作偏置单元 (bias unit)。

#### 神经网络

神经网络可以划分成多个层，每个层有一定数量的神经元。其中第一层叫输入层，最后一层叫输出层，一个或多个中间层叫隐藏层。

![neural networks](https://raw.githubusercontent.com/kamidox/blogs/master/images/neural_networks.png)

**几个索引的含义**

$a_i^{(j)}$: 表示第 j 层的第 i 个神经元 unit i in layer j
$\Theta^{(j)}$: 控制神经元网络中从第 j 层转化到第 j + 1 层的权重矩阵。这个矩阵里的元素经常写成 $\Theta_{jk}^{(j)}$ 其中 j 表示第 j 层，k 表示第 j 层神经元的输入个数。

$$
a_1^{(2)} = g(\Theta_{10}^{(1)} x_0 + \Theta_{11}^{(1)} x_1 + \Theta_{12}^{(1)} x_2 + \Theta_{13}^{(1)} x_3) \\\\
a_2^{(2)} = g(\Theta_{20}^{(1)} x_0 + \Theta_{21}^{(1)} x_1 + \Theta_{22}^{(1)} x_2 + \Theta_{23}^{(1)} x_3) \\\\
a_3^{(2)} = g(\Theta_{30}^{(1)} x_0 + \Theta_{31}^{(1)} x_1 + \Theta_{32}^{(1)} x_2 + \Theta_{33}^{(1)} x_3) \\\\
h_\Theta(x) = a_1^{(3)} = g(\Theta_{10}^{(2)} a_0 + \Theta_{11}^{(2)} a_1 + \Theta_{12}^{(2)} a_2 + \Theta_{13}^{(2)} a_3)
$$

假设 j 层有 $s_j$ 个单元，j + 1 层有 $s_{j+1}$ 个单元。那么 $\Theta^{(j)}$ 将是一个 $s_{j+1}$ x $(s_j + 1)$ 的矩阵。

#### 向前传播算法的向量化实现 Forward Propagation: Vectorized Implementation

$$
let: z_1^{(2)} = \Theta_{10}^{(1)} x_0 + \Theta_{11}^{(1)} x_1 + \Theta_{12}^{(1)} x_2 + \Theta_{13}^{(1)} x_3 = \Theta^{(1)} x \\\\
\Rightarrow a_1^{(2)} = g\left( z_1^{(2)} \right) \\\\
a_2^{(2)} = g\left( z_2^{(2)} \right) \\\\
a_3^{(2)} = g\left( z_3^{(2)} \right) \\\\
\Rightarrow a^{(2)} = g\left( z^{(2)} \right) \\\\
z^{(3)} = \Theta^{(2)} a^{(2)} \\\\
\Rightarrow h_\Theta(x) = a^{(3)} = g\left( z^{(3)} \right)
$$

更一般的情况，假设待训练的数据集 $X$ 是 m x n 矩阵，记作 $X \in R^{m,n}$，其中 m 是数据集个数，n 是一个数据组的特征数，此处假设 $X$ 里已经加入了偏置单元 (bias unit)。假设隐藏层有 s2 个单元，$\Theta^{(1)}$ 为输入层到隐藏层的转换参数。则 $\Theta^{(1)} \in R^{s2, n}$。输出层有 s3 个单元，$\Theta^{(2)}$ 为隐藏层到输出层的转换参数。则 $\Theta^{(2)} \in R^{s3, s2 + 1}$。我们记 $a^{(2)}$ 为隐藏层，$a^{(3)}$ 为输出层，则：

$$
a^{(2)} = g\left( X * \left( \Theta^{(1)} \right)^T \right)
$$

算出后，给 $a^{(2)}$ 加上偏置单元。为了书写方便，此处我们仍然将加上偏置单元后的隐藏层记作 $a^{(2)}$。则：

$$
a^{(3)} = g\left( a^{(2)} * \left( \Theta^{(2)} \right)^T \right)
$$

这几个公式就是神经网络向量化运算的重要规则。其中 $g(z) = \frac{1}{1 + e^{-z}}$ 是 Sigmoid Function。

**神经网络通过学习来决定其特征**

单单从 $h_\Theta(x) = g\left(\Theta^{(2)} a^{(2)}\right)$ 式子来看，神经网络的输出就是由特征 $a_1^{(2)}, a_2^{(2)}, a_3^{(2)}$ 的逻辑回归模型表述的。但这里的每个特征 $a_1^{(2)}, a_2^{(2)}, a_3^{(2)}$ 都是分别由 $x_1, x_2, x_3$ 的逻辑回归模型学习出来的。这就是神经网络的精髓所在。

### 神经网络的应用实例

#### 运用神经网络来模拟逻辑运算

假设 $\Theta = [-30, 20, 20]$，

$$
h_\Theta(x) = g(\Theta^T x) = g(-30 + 20x_1 + 20x_2)
$$

$g(z)$ 是 Sigmoid Function，其图形近似于 S 形。假设 $x_1, x_2 \exists {0, 1}$ 是逻辑值。当 $x_1 = 0, x_2 = 0$ 时，$h_\Theta(x) = g(-30) \approx 0$。同理可以写出下面的真值表：

x_1  | x_2 | h(x)
-----|-----|-----
0    | 0   | 0
1    | 0   | 0
0    | 1   | 0
1    | 1   | 1

这样就模拟了逻辑 AND 的运算，即 h(x) = x1 AND x2。同理可以推算出当 $\Theta = [-10, 20, 20]$ 时，h(x) = x1 OR x2。还可以推断出当 $\Theta = [10, -20, -20]$ 时，h(x) = (NOT x1) AND (NOT x2)。当需要计算 x1 NXOR x2 时，可以用神经网络模型，即 x1 NXOR x2 = (x1 AND x2) OR ((NOT x1) AND (NOT x2))。我们把 x1, x2 当作输入，a1 = (x1 AND x2), a2 = (NOT x1) AND (NOT x2) 当作隐藏层，而最终的输出由 a1 OR a2 来计算得来了。

#### 运用神经网络来处理多类别的分类问题

上文介绍的神经网络只能输出入 0, 1 二元问题。扩展到多个类别时，我们输出一个向量，比如针对最终结果是四种类别的问题时，输出 [1, 0, 0, 0] 表示第一种类别，输出 [0, 1, 0, 0] 表示是第二种类别，依此类推。

问题：为什么不用 1, 2, 3, 4 四个不同的值来表示四种类别，而要用一个四维的向量来表示？

## Week 5 神经网络学习 Neural Networks: Learning

### 成本函数

针对分类问题的神经网络的输出层

$$
h_\Theta(x) \in R^K; \left( h_\Theta(x) \right)_k = k^{th} output
$$

其中 K 是输出层的的单元个数，K >= 3。因为如果 K < 3 则可以直接用一个单元表示。其成本函数是：

$$
J(\Theta) = - \frac{1}{m} \left[ \sum_{i=1}^m \sum_{k=1}^K y_k^{(i)} log(h_k^{(i)}) + (1 - y_k^{(i)}) log(1 - h_k^{(i)}) \right] + \frac{\lambda}{2m} \sum_{l=1}^{L-1} \sum_{i=1}^{s_l} \sum_{j=1}^{s_{l+1}} (\Theta_{ji}^l)^2
$$

其中 $h_k^{(i)} = {h_\Theta(x^{(i)})}_k$ 是 $k^{th}$ 层针对 $i^{th}$ 训练样本的预测值。$L$ 是神经网络的层数，$s_l$ 是指第 $l$ 层的单元个数。公式的前半部分是未与正则化的成本函数，后半部分是正则项，加起来就是正则化的成本公式。注意正则项部分求和时是从 $i=1$ 开始的，即我们不把偏置变量正则化。

!!! warnning "MathJax 的缺陷"
    这个公式我写了 20 分钟。它已经复杂到我不得不把 $h_k^{(i)}$ 独立写出来了，如果全部写一个公式里，公式将无法正确显示。不服的可以自己试看看。

### 向后传播算法

我们把 $\delta_j^{(l)}$ 记作神经网络中第 $l$ 层，第 $j$ 个节点的误差。针对输出层，我们有

$$
\delta_j^{(L)} = a_j^{(L)} - y_j
$$

按照向量化写法，我们得到

$$
\delta^{(L)} = a^{(L)} - y
$$

针对第 $L-1$ 层，我们把误差定义为

$$
\delta^{(L-1)} = (\Theta^{(L-1)})^T \delta^{(L)} .* g'(z^{(L-1)})
$$

可以从数学上证明 $g'(z^{(L-1)}) = a^{(L-1)} .* (1 - a^{(L-1)})$ 成立。这样我们算出输出层的误差，然后一层层往前推导，算出各层的误差，就是我们向后传播算法名字的由来。需要注意的是，不存在 $\delta^{(1)}$，因为神经网络的第 1 层是我们的输入项，不存在误差问题。

从数学上可以证明，如果忽略正则项，即 $\lambda = 0$时

$$
\frac{\partial}{\partial \Theta_{ij}^{(l)}} J(\Theta) = a_j^{(l)} \delta_i^{(l+1)}
$$

最后，针对训练样本 ${ (x^{(1)}, y^{(1)}), (x^{(2)}, y^{(2)}), ... (x^{(m)}, y^{(m)}),}$，我们可以把向后传播算法用伪代码描述如下：

set $\Delta_{ij}^{(l)} = 0$, for all $l, i, j$
for i = 1 to m
  set $a^{(1)} = x^{(1)}$
  perform forward propagation to compute $a^{(l)}$ for $l = 2, 3, ... , L$
  using $y^{(i)}$, compute $\delta^{(L)} = a^{(L)} - y^{(i)}$
  compute $\delta^{(L-1)}, \delta^{(L-2)}, ..., \delta^{(2)}$ by using back propagation of error term
  $\Delta_{ij}^{(l)} = \Delta_{ij}^{(l)} + a_j^{(l)} \delta_i^{(l+1)}$
end for

加入正则项后，我们有

$$
D_{ij}^{(l)} = \frac{1}{m} \Delta_{ij}^{(l)} + \lambda \Theta_{ij}^{(l)}, if j \ne 0 \\\\
D_{ij}^{(l)} = \frac{1}{m} \Delta_{ij}^{(l)}, if j = 0
$$

从数学上可以证明

$$
\frac{\partial}{\partial \Theta_{ij}^{(l)}} J(\Theta) = D_{ij}^{(l)}
$$

这样我们就算出来了神经网络模型的成本函数微分项。有了成本函数和成本函数微分项，我们就可以使用线性回归或其他高级算法来计算神经网络成本函数的最小值，从而求解神经网络中各层激励的参数。


### TODO

1. 使用 scipy 实现手写数字识别程序
2. 从数学上证明 $g'(z^{(L-1)}) = a^{(L-1)} .* (1 - a^{(L-1)})$
3. 从数学上证明 $\frac{\partial}{\partial \Theta_{ij}^{(l)}} J(\Theta) = a_j^{(l)} \delta_i^{(l+1)}$
4. 从数学上证明 $\frac{\partial}{\partial \Theta_{ij}^{(l)}} J(\Theta) = D_{ij}^{(l)}$

[1]: https://www.coursera.org/learn/machine-learning/home/welcome
[2]: http://cs229.stanford.edu/materials.html
[3]: https://www.coursera.org/learn/machine-learning/discussions?sort=lastActivityAtDesc&page=1
[4]: https://www.coursera.org/learn/machine-learning/supplement/Mc0tF/linear-regression-with-one-variable
[5]: http://math.stackexchange.com/questions/70728/partial-derivative-in-gradient-descent-for-two-variables/189792#189792
[6]: https://www.coursera.org/learn/machine-learning/supplement/NMXXL/linear-algebra-review
[7]: https://en.wikipedia.org/wiki/Linear_least_squares_%28mathematics%29#Derivation_of_the_normal_equations
[8]: http://www.forkosh.com/mathtextutorial.html
[9]: http://mirrors.ctan.org/info/symbols/math/maths-symbols.pdf
[10]: http://cs229.stanford.edu/notes/cs229-notes1.pdf
[11]: http://cs229.stanford.edu/section/cs229-prob.pdf
[12]: http://stackoverflow.com/questions/119969/javascript-chart-library
[13]: http://mlworks.cn/posts/introduction-to-mathjax-and-latex-expression/