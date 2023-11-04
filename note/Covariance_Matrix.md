# Covariance Matrix

[形象理解协方差矩阵 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/349802953)

设$\mathbf{x}=[x_1,\ldots,x_n]^T$，其协方差矩阵 $C=(c_{ij})=E[(x_i-E(x_i))(x_j-E(x_j))]$. **证明经过线性变换$A\mathbf{x}$后，$A\mathbf{x}$的协方差矩阵为$\overline{C}=ACA^T$**

协方差矩阵更加简洁的定义就是
$$
C=E[(\mathbf{x}-E(\mathbf{x}))(\mathbf{x}-E(\mathbf{x}))^T]=\begin{bmatrix}
E[(x_1-E(x_1))(x_1-E(x_1))] & E[(x_1-E(x_1))(x_2-E(x_2))] & \cdots & E[(x_1-E(x_1))(x_n-E(x_n))]\\
E[(x_2-E(x_2))(x_1-E(x_1))] & E[(x_2-E(x_2))(x_2-E(x_2))] & \cdots & E[(x_2-E(x_2))(x_n-E(x_n))]\\
\vdots & \vdots & \ddots & \vdots\\
E[(x_n-E(x_n))(x_1-E(x_1))] & E[(x_n-E(x_n))(x_2-E(x_2))] & \cdots & E[(x_n-E(x_n))(x_n-E(x_n))]\\
\end{bmatrix}
$$
符号描述
$$
\mathbf{x}=\begin{bmatrix}
x_1\\ x_2\\ \vdots \\ x_n
\end{bmatrix}
\quad
E(\mathbf{x})=\begin{bmatrix}
E(x_1)\\ E(x_2)\\ \vdots \\ E(x_n)
\end{bmatrix}
\quad
A=
\begin{bmatrix}
\vec{a}_1^T\\ \vec{a}_2^T\\ \vdots \\ \vec{a}_m^T
\end{bmatrix}
=
\begin{bmatrix}
a_{11} & a_{12} & \cdots & a_{1n}\\
a_{21} & a_{22} & \cdots & a_{2n}\\
\vdots & \vdots & \ddots & \vdots\\
a_{m1} & a_{m2} & \cdots & a_{mn}\\
\end{bmatrix}
\quad
\vec{a}_i^T = \begin{bmatrix}
a_{i1} \\ a_{i2} \\ \vdots \\ a_{in}  
\end{bmatrix}
$$
证明：
$$
A\mathbf{x}=
\begin{bmatrix}
a_{11} & a_{12} & \cdots & a_{1n}\\
a_{21} & a_{22} & \cdots & a_{2n}\\
\vdots & \vdots & \ddots & \vdots\\
a_{m1} & a_{m2} & \cdots & a_{mn}\\
\end{bmatrix}
\begin{bmatrix}
x_1\\ x_2\\ \vdots \\ x_n
\end{bmatrix}
=
\begin{bmatrix}
\vec{a}_1^T\\ \vec{a}_2^T\\ \vdots \\ \vec{a}_m^T
\end{bmatrix}
\mathbf{x}
=
\begin{bmatrix}
\vec{a}_1^T\mathbf{x} \\ \vec{a}_2^T\mathbf{x} \\ \vdots \\ \vec{a}_m^T\mathbf{x}
\end{bmatrix}_{m\times1}
$$
$A\mathbf{x}$的协方差矩阵的元素等于
$$
\begin{split}
\bar{c}_{ij}=E[(\vec{a}_i^T\mathbf{x}-E(\vec{a}_i^T\mathbf{x}))(\vec{a}_j^T\mathbf{x}-E(\vec{a}_j^T\mathbf{x}))]
\end{split}
$$
由于$E(\vec{a}_i^T\mathbf{x})=E(a_{i1}x_{1}+a_{i2}x_{2}+\cdots +a_{in}x_{n})=\vec{a}_i^TE(\mathbf{x})$
$$
\begin{split}
\bar{c}_{ij}&=E[(\vec{a}_i^T\mathbf{x}-E(\vec{a}_i^T\mathbf{x}))(\vec{a}_j^T\mathbf{x}-E(\vec{a}_j^T\mathbf{x}))]\\
&= E[(\vec{a}_i^T\mathbf{x}-\vec{a}_i^TE(\mathbf{x}))(\vec{a}_j^T\mathbf{x}-\vec{a}_j^TE(\mathbf{x}))]\\
&= E[\vec{a}_i^T(\mathbf{x}-E(\mathbf{x}))\vec{a}_j^T(\mathbf{x}-E(\mathbf{x}))]
\end{split}
$$
**$\vec{a}_j^T(\mathbf{x}-E(\mathbf{x}))$是一个标量**，因此$\vec{a}_j^T(\mathbf{x}-E(\mathbf{x}))=(\mathbf{x}-E(\mathbf{x}))^T\vec{a}_j$
$$
\begin{split}
\overline{c}_{ij}
&= E[\vec{a}_i^T(\mathbf{x}-E(\mathbf{x}))\vec{a}_j^T(\mathbf{x}-E(\mathbf{x}))]\\
&= E[\vec{a}_i^T(\mathbf{x}-E(\mathbf{x}))(\mathbf{x}-E(\mathbf{x}))^T\vec{a}_j]\\
&= \vec{a}_i^TE[(\mathbf{x}-E(\mathbf{x}))(\mathbf{x}-E(\mathbf{x}))^T]\vec{a}_j\\
\end{split}
$$
因为
$$
C=E[(\mathbf{x}-E(\mathbf{x}))(\mathbf{x}-E(\mathbf{x}))^T]
$$
故
$$
\begin{split}
\overline{c}_{ij}
&= \vec{a}_i^TC\vec{a}_j\\
\end{split}
$$
那么就有
$$
\overline{C}=
\begin{bmatrix}
\vec{a}_1^TC\vec{a}_1 & \vec{a}_1^TC\vec{a}_2 & \cdots & \vec{a}_1^TC\vec{a}_m \\
\vec{a}_2^TC\vec{a}_1 & \vec{a}_2^TC\vec{a}_2 & \cdots & \vec{a}_2^TC\vec{a}_m \\
\vdots & \vdots & \ddots & \vdots\\
\vec{a}_m^TC\vec{a}_1 & \vec{a}_m^TC\vec{a}_2 & \cdots & \vec{a}_m^TC\vec{a}_m \\
\end{bmatrix}
=\begin{bmatrix}
\vec{a}_1^T\\ \vec{a}_2^T\\ \vdots \\ \vec{a}_m^T
\end{bmatrix}
C
\begin{bmatrix}
\vec{a}_1 & \vec{a}_2 & \cdots & \vec{a}_m
\end{bmatrix}
=
ACA^T
$$








