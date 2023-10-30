# IMU Model

参考 [从零开始的 IMU 状态模型推导](https://fzheng.me/2016/11/20/imu_model_eq/)

包括IMU运动模型、IMU观测和噪声模型、IMU状态估计误差模型三部分

下面是关于本文档的符号的说明，十分重要，当初看不懂教程就是符号太多，不理解

- IMU的状态量：$\mathrm{X}_{IMU}=[^I_G\bar{q}^T,\mathrm{b}_g^T,^G\mathrm{v}^T_I,\mathrm{b}_a^T,^G\mathrm{p}_I^T]$

  - $\{I\}$表示IMU坐标系，$\{G\}$表示参考坐标系global，参考坐标系也就是$(1,0,0),(0,1,0),(0,0,1)$
  - 旋转量$^I_G\bar{q}^T$ 和 平移量$^G\mathrm{p}_I^T$ 共同表示IMU的姿态
  - 旋转量$^I_G\bar{q}^T$ **是一个单位四元数**，表示**将任意向量从$\{G\}$坐标映射到$\{I\}$坐标的旋转量**
  - $R(^I_G\bar{q}^T)$表示该四元数对应的旋转矩阵
  - 平移量$^G\mathrm{p}_I^T$ 表示IMU在{G}下的三维位置
  - $^G\mathrm{v}^T_I$ 表示**在{G}下**的**平移**速度
  - $\mathrm{b}_a^T,\mathrm{b}_g^T$ 分别表示 加速度计 和 陀螺仪(角速度计) 的bias

- 上面的量有以下关系
  $$
  \begin{split}
  &平移量p\xrightarrow[]{求导}平移速度v\xrightarrow[]{求导}加速度a\\
  &旋转量R\xrightarrow[]{求导}角速度\omega\xrightarrow[]{求导}角加速度\\
  &偏置bias \xrightarrow[]{求导}噪声n
  \end{split}
  $$
  

- 角速度矢量表示为 $\mathbf{\omega}=\dot{\theta}\mathbf{u}$，其中$\mathbf{u}$是旋转轴的单位向量，$\dot{\theta}$是对角度$\theta$求导，也即角速度的标量值。这样定义角速度矢量的目的是 当考虑一个**从原点出发**的向量$\mathrm{r}$**绕单位轴$\mathbf{u}$旋转**，角速度大小为$\dot{\theta}$，角速度矢量$\omega$与向量$\mathbf{r}$**叉积**的结果**等于角速度的方向与大小**   注意区分角速度和角速度矢量

- 公式(1.0)上面有一句话，$[\mathbf{i}_B,\mathbf{j}_B,\mathbf{k}_B]$实际上就是坐标系{B}相对于参考坐标系global的旋转矩阵$\mathbf{R}$。这里给出说明是哪里旋转到哪里(从{B}旋转到参考坐标系)

  参考坐标系为
  $$
  \mathbf{e}_1=[1,0,0]^T,\quad \mathbf{e}_2=[0,1,0]^T, \quad \mathbf{e}_3=[0,0,1]^T
  $$
  **坐标系{B}的三个坐标轴在参考坐标系下的坐标分别为$\mathbf{i}_B,\mathbf{j}_B,\mathbf{k}_B$**，那么就有关系
  $$
  [\mathbf{e}_1,\mathbf{e}_2,\mathbf{e}_3]\begin{bmatrix}
  x_{global}\\ y_{global}\\ z_{global}\\
  \end{bmatrix}
  =[\mathbf{i}_B,\mathbf{j}_B,\mathbf{k}_B]\begin{bmatrix}
  x_{B}\\ y_{B}\\ z_{B}\\
  \end{bmatrix}
  $$
  由于$[\mathbf{e}_1,\mathbf{e}_2,\mathbf{e}_3]$是单位矩阵，所以上式可以写成
  $$
  \begin{bmatrix}
  x_{global}\\ y_{global}\\ z_{global}\\
  \end{bmatrix}
  =[\mathbf{i}_B,\mathbf{j}_B,\mathbf{k}_B]\begin{bmatrix}
  x_{B}\\ y_{B}\\ z_{B}\\
  \end{bmatrix}
  =\mathbf{R}\begin{bmatrix}
  x_{B}\\ y_{B}\\ z_{B}\\
  \end{bmatrix}
  $$
  因此，**$\mathbf{R}$是从坐标系{B}旋转到参考坐标系global的旋转矩阵**，所以$\mathbf{R}$与$^I_G\bar{q}^T$的旋转方向是相反的。

- 地球自转角速度$\mathbf{\omega}_G$，重力加速度$^G\mathbf{g}$，都是在参考坐标系global下

- 陀螺仪(角速度)$\mathbf{\omega}_m$，加速度$\mathbf{a}_m$，都是在IMU坐标系{I}下的。这里的m是measurement的意思。