# Gauss-Newton Iteration with Automatic Derivatives

## Ref

- [Automatic Derivatives — Ceres Solver (ceres-solver.org)](http://ceres-solver.org/automatic_derivatives.html)

- [对偶数 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/358146509)
- 视觉slam十四讲 P128

## 自动微分

### 对偶数

数学是一个逻辑的学科，只要自洽，数学就可以作出很多超越常识的定义。比如，复数。

对于复数，我们引入虚数单元$i$，并且将它定义为$i^2=-1$，然后将复数定义为$a+ib$，**根据这个定义，那么复数的加减乘除，指数，对数运算，都可以被定义出来**
$$
\begin{split}
(a_1+ib_1)\pm(a_2+ib_2) &= (a_1\pm a_2)+i(b_1\pm b_2)\\
(a_1+ib_1)*(a_2+ib_2) &=(a_1a_2-b_1b_2)+i(a_1b_2+a_2b_1)\\
\frac{a_1+ib_1}{a_2+ib_2} &= \frac{(a_1a_2+b_1b_2)+i(a_2b_1-a_1b_2)}{a_2^2+b_2^2}\\
\cdots \cdots
\end{split}
$$
那么同理，**类似于复数**，我们定义**对偶数单元**，记为$\epsilon$，它的定义为$\epsilon^2=0$，一个**对偶数**就定义为$a+\epsilon b$，它可以与复数做以下类比
$$
\begin{split}
\epsilon &\rightarrow j\\
\epsilon^2 = 0 &\rightarrow j^2 = -1\\
a+\epsilon b &\rightarrow a+jb
\end{split}
$$
那么，**根据$\epsilon^2=0$的定义，就可以定义出对偶数的四则运算，指数，对数，幂次等运算**
$$
\begin{split}
(a_1+\epsilon b_1)\pm(a_2+\epsilon b_2) &= (a_1\pm a_2)+\epsilon (b_1\pm b_2)\\
(a_1+\epsilon b_1)*(a_2+\epsilon b_2) &=a_1a_2+\epsilon (a_1b_2+a_2b_1)+\underbrace{\epsilon^2}_{=0}b_1b_2\\
&=a_1a_2+\epsilon (a_1b_2+a_2b_1)\\
\frac{a_1+\epsilon b_1}{a_2+\epsilon b_2}&= \frac{(a_1+\epsilon b_1)(a_2-\epsilon b_2)}{a_2^2-\epsilon^2 b_2^2} \\
&= \frac{a_1a_2+\epsilon(a_2b_1-a_1b_2)}{a_2^2}\\
e^{a+\epsilon b}&=e^a\cdot e^{\epsilon b}=e^a+\epsilon be^a\\
\ln(a+\epsilon b)&= \ln(a)+\epsilon\frac{b}{a}\\
\sin(a+\epsilon b) &= \sin(a)+\epsilon b\cos(a)\\
\cos(a+\epsilon b) &= \cos(a) - \epsilon b\sin(a)
\end{split}
$$
证明 $e^{a+\epsilon b}=e^a\cdot e^{\epsilon b}=e^a+\epsilon be^a$

$e^x$的泰勒展开式为($e^x$求n次导数都等于$e^x$)，注意，泰勒展开是等号，这里没有删去高阶项做近似
$$
e^{x+\Delta x}=e^x + \frac{1}{1!}e^x\Delta x+\frac{1}{2!}e^x\Delta x^2+\cdots
$$
那么 $e^{a+\epsilon b}$ 就可以写成
$$
e^{a+\epsilon b} =e^a + \frac{1}{1!}e^a\epsilon b+\frac{1}{2!}e^a\epsilon^2 b^2+ \frac{1}{3!}e^a\epsilon^3 b^3 +\cdots
$$
由于
$$
\epsilon^2=0\rightarrow \epsilon^3=\epsilon\cdot\epsilon^2=0\rightarrow \cdots
$$
所以泰勒展开式二阶项及其后面的项都等于0，所以
$$
e^{a+\epsilon b} =e^a + e^a\epsilon b=e^a(1+\epsilon b)
$$
**其它的式子都可以用泰勒展开来证明**

### 自动微分原理

类似$e^{a+\epsilon b}=e^a\cdot e^{\epsilon b}=e^a+\epsilon be^a$的证明

目的是得到函数$f(x)$在点$x=a$处的导数值$f(a)$，可以通过**计算$f(a+\epsilon b)$在$x=a$处的泰勒展开式**
$$
f(a+\epsilon b)=f(a)+\frac{1}{1!}f'(a)b\epsilon + \frac{1}{2!}f''(a)\space (b\epsilon)^2+\cdots
$$
由于
$$
\epsilon^2=0\rightarrow \epsilon^3=\epsilon\cdot\epsilon^2=0\rightarrow \cdots
$$
故
$$
f(a+\epsilon b)=f(a)+f'(a)b\epsilon
$$
当取$b=1$时
$$
f(a+\epsilon)=f(a)+f'(a)\epsilon
$$
$\epsilon$的系数就是$f(x)$在点$x=a$处的导数值$f(a)$

因此，可以**通过使用$\epsilon$的计算法则来计算$f(a+\epsilon)$，$\epsilon$的系数就是$f(x)$在点$x=a$处的导数值$f(a)$**

### 注意

使用对偶数计算**得到的只是$f(x)$在$a$点的导数值，而不是$f'(x)$的解析式**

### 使用自动微分求偏导

计算$f(x_1,x_2,\ldots,x_n)$在点$(x_1^k,x_2^k,\ldots,x_n^k)$处的各个偏导数。

记
$$
\Delta x_m=x_m-x_m^k
$$

$$
\begin{split}
f(x_1,x_2,\ldots,x_n)=& f(x_1^k,x_2^k,\ldots,x_n^k)\\
&+ \frac{1}{1!}f'_{x_1}(x_1^k,x_2^k,\ldots,x_n^k)\Delta x_1+\cdots+\frac{1}{1!}f'_{x_n}(x_1^k,x_2^k,\ldots,x_n^k)\Delta x_n\\
&+ \frac{1}{2!}f''_{x_1}(x_1^k,x_2^k,\ldots,x_n^k)\Delta x_1^2+\frac{1}{2!}f''_{x_1x_2}(x_1^k,x_2^k,\ldots,x_n^k)\Delta x_1\Delta x_2+\frac{1}{2!}f''_{x_1x_3}\cdot\Delta x_1\Delta x_3+\cdots\\
&+ \frac{1}{2!}f''_{x_2x_1}(x_1^k,x_2^k,\ldots,x_n^k)\Delta x_2\Delta x_1+\frac{1}{2!}f''_{x_2}(x_1^k,x_2^k,\ldots,x_n^k)\Delta x_2^2+\frac{1}{2!}f''_{x_2x_3}\cdot\Delta x_2\Delta x_3+\cdots\\
&+ \cdots\\
&+ \frac{1}{2!}f''_{x_nx_1}\Delta x_n\Delta x_1+\frac{1}{2!}f''_{x_nx_2}\Delta x_n\Delta x_2+\cdots+\frac{1}{2!}f''_{x_n}\cdot \Delta x_n^2\\
&+ o(\mathbf{x})\\
\end{split}
$$

此时，我们令$x_m$为一个实部为$x_m^k$，虚部为1的对偶数
$$
x_m=x_m^k+\epsilon \quad \rightarrow \quad \Delta x_m=x_m-x_m^k=\epsilon
$$
那么就有
$$
\Delta x_i\Delta x_j=\epsilon^2=0\\
\Delta x_i\Delta x_j\Delta x_k=\epsilon^3=\epsilon\cdot\epsilon^2=0\\
\cdots \cdots
$$
那么多元泰勒展开式的二次项及更高阶的项都变成0
$$
\begin{split}
f(x_1,x_2,\ldots,x_n)=f(\begin{bmatrix}x_1^k\\x_2^k \\ \vdots\\ x_n^k\end{bmatrix}+\begin{bmatrix}\epsilon \\ \epsilon \\ \vdots \\ \epsilon\end{bmatrix})
=& f(x_1^k,x_2^k,\ldots,x_n^k) + \frac{1}{1!}f'_{x_1}(x_1^k,x_2^k,\ldots,x_n^k)\Delta x_1+\cdots+\frac{1}{1!}f'_{x_n}(x_1^k,x_2^k,\ldots,x_n^k)\Delta x_n\\
=& f(x_1^k,x_2^k,\ldots,x_n^k) + f'_{x_1}(x_1^k,x_2^k,\ldots,x_n^k)\epsilon+\cdots+f'_{x_n}(x_1^k,x_2^k,\ldots,x_n^k)\epsilon\\
\end{split}
$$
但是这样，$\epsilon$的系数就是各元偏导数相加了，那么
$$
\begin{split}
f(x_1,x_2,\ldots,x_n)=f(\begin{bmatrix}x_1^k\\x_2^k \\ \vdots\\ x_n^k\end{bmatrix}+\begin{bmatrix}\epsilon \\ 0 \\ \vdots \\ 0\end{bmatrix})
=& f(x_1^k,x_2^k,\ldots,x_n^k) + \frac{1}{1!}f'_{x_1}(x_1^k,x_2^k,\ldots,x_n^k)\Delta x_1+\cdots+\frac{1}{1!}f'_{x_n}(x_1^k,x_2^k,\ldots,x_n^k)\Delta x_n\\
=& f(x_1^k,x_2^k,\ldots,x_n^k) + f'_{x_1}(x_1^k,x_2^k,\ldots,x_n^k)\epsilon\\
\end{split}
$$
即可，以此类推

## 高斯-牛顿迭代与自动微分

高斯牛顿迭代的介绍请看视觉slam十四讲 P128

我们可以得到迭代的增量公式
$$
\Delta \mathbf{x}=-(\mathbf{J}(\mathbf{x})\mathbf{J}^T(\mathbf{x}))^{-1}\mathbf{J}(\mathbf{x}) f(\mathbf{x})
$$
看起来很吓人，要求出$f(\mathbf{x})$的雅可比$\mathbf{J}(\mathbf{x})$的解析式，再**计算在这个点$\mathbf{x}$时的雅可比的值**,再雅可比的值来计算增量。那么我们换个思路，**能不能直接计算雅可比的值，而不计算雅可比的解析式？**自动微分就帮我们解决了这个问题，而且这也规避掉了计算雅可比过于复杂，甚至说函数$f(\mathbf{x})$根本无法写出表达式的情况。

## 例子

A-LOAM











