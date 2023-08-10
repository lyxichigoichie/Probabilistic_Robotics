# Matrix Differentiation

## 矩阵求导分子分母布局

https://zhuanlan.zhihu.com/p/263777564

- **向量变元**的**实值标量函数**的分布

  记向量为列向量$\boldsymbol{x} = [x_1,x_2,...,x_n]^T$

  1. 行向量偏导
     $$
     \boldsymbol{D}_{\boldsymbol{x}}f(\boldsymbol{x})=\frac{\partial f(\boldsymbol{x})}{\partial \boldsymbol{x}^T}=[\frac{\partial f}{\partial x_1},\frac{\partial f}{\partial x_2},...\frac{\partial f}{\partial x_n}]
     $$

  2. 梯度向量偏导
     $$
     \nabla_{\boldsymbol{x}}f(\boldsymbol{x})=\frac{\partial f(\boldsymbol{x})}{\partial \boldsymbol{x}}=[\frac{\partial f}{\partial x_1},\frac{\partial f}{\partial x_2},...\frac{\partial f}{\partial x_n}]^T
     $$

- **矩阵变元**的**实值标量函数**的分布

  记矩阵变元为
  $$
  \mathbf{X}_{m\times n}=\begin{bmatrix}
  x_{11} & x_{12} & \cdots & x_{1n}\\
  x_{21} & x_{22} & \cdots & x_{2n}\\
  \vdots & \vdots & \ddots & \vdots\\
  x_{m1} & x_{m2} & \cdots & x_{mn}\\
  \end{bmatrix}_{m\times n}
  $$

  1. $Jacobian$矩阵形式

     先把矩阵变元$\mathbf{X}$进行转置，再对**转置后**的每个位置的元素逐个求偏导，**结果布局和转置后的布局一致**
     $$
     \mathbf{D}_{\mathbf{X}}=\frac{\partial f(\mathbf{X})}{\partial \mathbf{X}^T_{m\times n}}=
     \begin{bmatrix}
     \frac{\partial f}{x_{11}} & \frac{\partial f}{x_{21}} & \cdots & \frac{\partial f}{x_{m1}}\\
     \frac{\partial f}{x_{12}} & \frac{\partial f}{x_{22}} & \cdots & \frac{\partial f}{x_{m2}}\\
     \vdots & \vdots & \ddots & \vdots \\
     \frac{\partial f}{x_{1n}} & \frac{\partial f}{x_{2n}} & \cdots & \frac{\partial f}{x_{mn}}\\
     \end{bmatrix}_{n\times m}
     $$
     
  2. 梯度矩阵形式
  
     直接对原矩阵变元$\mathbf{X}$的每个位置的元素逐个求偏导，结果**布局与原矩阵布局一样**
     $$
     \nabla_{\mathbf{X}}f(\mathbf{X})=\frac{f(\mathbf{X})}{\partial \mathbf{X}_{m\times n}}=\begin{bmatrix}
     \frac{\partial f}{\partial x_{11}} & \frac{\partial f}{\partial x_{12}} & \cdots & \frac{\partial f}{\partial x_{1n}}\\
     \frac{\partial f}{\partial x_{21}} & \frac{\partial f}{\partial x_{22}} & \cdots & \frac{\partial f}{\partial x_{2n}}\\
     \vdots & \vdots & \ddots & \vdots\\
     \frac{\partial f}{\partial x_{m1}} & \frac{\partial f}{\partial x_{m2}} & \cdots & \frac{\partial f}{\partial x_{mn}}\\
     \end{bmatrix}_{\m\times n}
     $$

## 向量变元的实值标量函数、矩阵变元的实值标量函数的几个公式

### 向量变元的实值标量函数

使用梯度向量的形式
$$
\boldsymbol{x}=[x_1,x_2,\cdots, x_n]^T\\
\nabla_{\boldsymbol{x}}f(\boldsymbol{x})=[\frac{\partial f}{\partial x_1},\frac{\partial f}{\partial x_2},\cdots, \frac{\partial f}{\partial x_n}]^T
$$

#### 四个法则

1. 常数求导
   $$
   \frac{\partial c}{\partial \boldsymbol{x}}=\boldsymbol{0}_{n\times 1}
   $$

2. 线性法则
   $$
   \frac{c_1f(\boldsymbol{x})+c_2g(\boldsymbol{x})}{\partial \boldsymbol{x}}=c_1\frac{\partial f(x)}{\partial \boldsymbol{x}}+c_2\frac{\partial g(\boldsymbol{x})}{\partial \boldsymbol{x}}
   $$

3. 乘积法则
   $$
   \frac{\partial [f(\boldsymbol{x})g(\boldsymbol{x})]}{\partial \boldsymbol{x}}
   = \frac{\partial f(\boldsymbol{x})}{\partial \boldsymbol{x}}g(\boldsymbol{x})+f(\boldsymbol{x})\frac{\partial g(\boldsymbol{x})}{\partial \boldsymbol{x}}
   $$

4. 商法则
   $$
   \frac{\partial\Big[\frac{f(\boldsymbol{x})}{g(\boldsymbol{x})}\Big]}{\partial \boldsymbol{x}}=\frac{1}{g^2(\boldsymbol{x})}\Big[\frac{\partial f(\boldsymbol{x})}{\partial \boldsymbol{x}}g(\boldsymbol{x})-f(\boldsymbol{x})\frac{\partial g(\boldsymbol{x})}{\partial \boldsymbol{x}}\Big]
   $$

#### 四个公式

1. 
   $$
   \frac{\partial(\boldsymbol{x}^T\boldsymbol{a})}{\partial \boldsymbol{x}}=\frac{\boldsymbol{a}^T\boldsymbol{x}}{\partial \boldsymbol{x}}=\boldsymbol{a}\\
   here \qquad \boldsymbol{a}=[a_1,a_2,\cdots, a_n]^T
   $$

2. 
   $$
   \frac{\partial(\boldsymbol{x}^T\boldsymbol{x})}{\partial \boldsymbol{x}}=2\boldsymbol{x}
   $$

3. 
   $$
   \frac{\partial(\boldsymbol{x}^T\boldsymbol{A}\boldsymbol{x})}{\partial \boldsymbol{x}}=\boldsymbol{A}\boldsymbol{x}+\boldsymbol{A}^T\boldsymbol{x}\\
   here \qquad \boldsymbol{A}_{n\times n}\space is \space constant \space matrix
   $$

4. 
   $$
   \frac{\partial(\boldsymbol{a}^T\boldsymbol{x}\boldsymbol{x}^T\boldsymbol{b})}{\partial \boldsymbol{x}}=\boldsymbol{a}\boldsymbol{b}^T\boldsymbol{x}+\boldsymbol{b}\boldsymbol{a}^T\boldsymbol{x}\\
   here \qquad \boldsymbol{a}=[a_1,a_2,\cdots, a_n]^T,\quad \boldsymbol{b}=[b_1,b_2,\cdots, b_n]^T
   $$

### 矩阵变元的实值标量函数

使用梯度向量的形式
$$
\nabla_{\boldsymbol{X}}f(\boldsymbol{X})=\frac{\partial f(\boldsymbol{X})}{\partial \boldsymbol{X}_{m\times n}}=\begin{bmatrix}
\frac{\partial f}{x_{11}} & \frac{\partial f}{x_{12}} & \cdots & \frac{\partial f}{x_{1n}}\\
\frac{\partial f}{x_{21}} & \frac{\partial f}{x_{22}} & \cdots & \frac{\partial f}{x_{2n}}\\
\vdots & \vdots & \ddots & \vdots\\
\frac{\partial f}{x_{m1}} & \frac{\partial f}{x_{m2}} & \cdots & \frac{\partial f}{x_{mn}}\\
\end{bmatrix}_{m\times n}
$$
#### 四个法则

1. 常数求导
   $$
   \frac{\partial c}{\partial \boldsymbol{X}}=\boldsymbol{0}_{m\times n}
   $$

2. 线性法则
   $$
   \frac{c_1f(\boldsymbol{X})+c_2g(\boldsymbol{X})}{\partial \boldsymbol{X}}=c_1\frac{\partial f(\boldsymbol{X})}{\partial \boldsymbol{X}}+c_2\frac{\partial g(\boldsymbol{X})}{\partial \boldsymbol{X}}
   $$

3. 乘积法则
   $$
   \frac{\partial [f(\boldsymbol{X})g(\boldsymbol{X})]}{\partial \boldsymbol{X}}
   = \frac{\partial f(\boldsymbol{X})}{\partial \boldsymbol{X}}g(\boldsymbol{X})+f(\boldsymbol{X})\frac{\partial g(\boldsymbol{X})}{\partial \boldsymbol{X}}
   $$

4. 商法则
   $$
   \frac{\partial\Big[\frac{f(\boldsymbol{X})}{g(\boldsymbol{X})}\Big]}{\partial \boldsymbol{X}}=\frac{1}{g^2(\boldsymbol{X})}\Big[\frac{\partial f(\boldsymbol{X})}{\partial \boldsymbol{X}}g(\boldsymbol{X})-f(\boldsymbol{X})\frac{\partial g(\boldsymbol{X})}{\partial \boldsymbol{X}}\Big]
   $$

#### 四个公式

1. 
   $$
   \frac{\partial(\boldsymbol{a}^T\boldsymbol{X}\boldsymbol{b})}{\partial \boldsymbol{X}}=\boldsymbol{a}\boldsymbol{b}^T\\
   $$
   here, $\boldsymbol{X}'s$ dimension is $m\times n$. so 
   $$
   \boldsymbol{a}=[a_1,a_2,\cdots, a_m]^T,\quad \boldsymbol{b}=[b_1,b_2,\cdots, b_n]^T
   $$

2. 
   $$
   \frac{\partial(\boldsymbol{a}^T\boldsymbol{X}^T\boldsymbol{b})}{\partial \boldsymbol{X}}=\boldsymbol{b}\boldsymbol{a}^T\\
   $$

3. 
   $$
       \frac{\partial(\boldsymbol{a}^T\boldsymbol{X}\boldsymbol{X}^T\boldsymbol{b})}{\partial \boldsymbol{X}}=\boldsymbol{a}\boldsymbol{b}^T\boldsymbol{X}+\boldsymbol{b}\boldsymbol{a}^T\boldsymbol{X}
   $$
   since the dimension of $\boldsymbol{X}\boldsymbol{X}^T$ is $m\times m$, the dimension of $\boldsymbol{a},\boldsymbol{b}$ is
   $$
   \boldsymbol{a}=[a_1,a_2,\cdots, a_m]^T,\quad \boldsymbol{b}=[b_1,b_2,\cdots, b_m]^T
   $$
4. 
   $$
   \frac{\partial(\boldsymbol{a}^T\boldsymbol{X}^T\boldsymbol{X}\boldsymbol{b})}{\partial \boldsymbol{X}}=\boldsymbol{X}\boldsymbol{b}\boldsymbol{a}^T+\boldsymbol{X}\boldsymbol{a}\boldsymbol{b}^T
   $$
   since the dimension of $\boldsymbol{X}^T\boldsymbol{X}$ is $n\times n$, the dimension of $\boldsymbol{a},\boldsymbol{b}$ is
   $$
   \boldsymbol{a}=[a_1,a_2,\cdots, a_n]^T,\quad \boldsymbol{b}=[b_1,b_2,\cdots, b_n]^T
   $$

## 矩阵求导公式推导

核心公式，对于矩阵变元的实值标量函数的全微分
$$
\dd f(\boldsymbol{X})=\tr(\frac{\partial f(\boldsymbol{X})}{\partial \boldsymbol{X}^T} \dd {\boldsymbol{X}})
$$
对于标量函数，它的trace就是它本身，故
$$
\dd f(\boldsymbol{X})=\dd \tr(f(\boldsymbol{X}))
$$
矩阵变元的实值标量函数的全微分是如下形式
$$
\dd f(\boldsymbol{X})=\sum_{i,j}\frac{\partial f}{\partial x_{i,j}}\dd x_{i,j}
$$
它是个标量，不是矩阵，对于标量$x$，trace有性质
$$
\tr(x)=x
$$
因此有
$$
\dd f(\boldsymbol{X})=\tr(\dd f(\boldsymbol{X}))
$$
又因为对于全微分，可以写成
$$
\begin{split}
\dd f(\boldsymbol{X})
&= \frac{\partial f}{\partial x_{11}}\dd x_{11} + \frac{\partial f}{\partial x_{12}}+\cdots + \frac{\partial f}{\partial x_{1n}}\dd x_{1n}\\
&+ \frac{\partial f}{\partial x_{21}}\dd x_{21} + \frac{\partial f}{\partial x_{22}}+\cdots + \frac{\partial f}{\partial x_{2n}}\dd x_{2n}\\
&+ \cdots \\
&+ \frac{\partial f}{\partial x_{m1}}\dd x_{m1} + \frac{\partial f}{\partial x_{m2}}+\cdots + \frac{\partial f}{\partial x_{mn}}\dd x_{mn}\\
&= \tr(
\begin{bmatrix}
\frac{\partial f}{\partial x_{11}} & \frac{\partial f}{\partial x_{21}} & \cdots & \frac{\partial f}{\partial x_{m1}}\\
\frac{\partial f}{\partial x_{12}} & \frac{\partial f}{\partial x_{22}} & \cdots & \frac{\partial f}{\partial x_{m2}}\\
\vdots & \vdots & \ddots & \vdots\\
\frac{\partial f}{\partial x_{1n}} & \frac{\partial f}{\partial x_{2n}} & \cdots & \frac{\partial f}{\partial x_{mn}}\\
\end{bmatrix}_{n\times m}
\begin{bmatrix}
\dd x_{11} & \dd x_{12} & \cdots  & \dd x_{1n}\\
\dd x_{21} & \dd x_{22} & \cdots  & \dd x_{2n}\\
\vdots & \vdots & \ddots & \vdots\\
\dd x_{m1} & \dd x_{m2} & \cdots  & \dd x_{mn}\\
\end{bmatrix}_{m\times n}
)\\
&= \tr(\frac{\partial f(\boldsymbol{X})}{\partial \boldsymbol{X}^T} \space \dd {\boldsymbol{X}})\\
&= \tr(\mathbf{D}_{\boldsymbol{X}}f(\boldsymbol{X}) \space \dd {\boldsymbol{X}})
\end{split}
$$
因此有
$$
\tr(\dd f(\boldsymbol{X}))=\tr(\frac{\partial f(\boldsymbol{X})}{\partial \boldsymbol{X}^T} \space \dd {\boldsymbol{X}})
$$
那么将$\tr(\dd f(\boldsymbol{X}))$里面$\dd f(\boldsymbol{X})$部分化简成$(...\space \dd {\boldsymbol{X}})$的形式，前面的部分就是这个矩阵变元标量函数的$Jacobian$

化简的过程需要用到trace的性质和一些微分公式，太多了，这里就不列举出来了，查看https://zhuanlan.zhihu.com/p/288541909





















