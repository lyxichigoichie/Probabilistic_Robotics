# problem unsolved

1. in extended Kalman filter page 58, why it only expand variable $x_{t-1}$ and do not expand variable $u_t$. $g$ is function of $u_t$ and $x_{t-1}$

   Answer:

   It actually expands both. But we think that the motion $u_t$ is accurate and we expand the function on point $u_t=u_t$
   $$
   g(x_{t-1},u_t)=g(\mu_{t-1},u_t)+\frac{\partial g}{\partial x_{t-1}}\Delta x+\frac{\partial g}{\partial u_t}\Delta u
   $$
   and
   $$
   \Delta u=u_t-u_t=0
   $$

2. In beam models of range finder page 157, how to realize that the measurement distribution can be mixed by a weighted average such a linear combination. In real world, it should be that addition of the four errors. why the addition of the errors caused the addition of probability of errors.

3. In likelihood fields for range finders, why the probability of sensor measurements is modeled by zero-centered Gaussian not $z_t^k$ centered.

4. In landmark measurement page 178, whom the i-th feature is belong to??  Is the j-th landmark a feature of the map???  why corresponding the i-th feature to the j-th landmark not the j-th landmark???

   Answer:

   It based on the assumption that the map is known.

   For example, there 6 landmarks in the map and they are [rabbit, dog, cat, bird]. Rabbit is the $1^{th}$ landmark. Dog is the $2^{th}$ landmark. Cat... Bird... At this time $t=t$, we observe 2 feature $z_t = [z_t^1,z_t^2]$. Which landmark does the feature belong to? If $z_t^1=bird$, that means the $1^{th}$ feature corresponds to $4^{th}$ landmark.

5. In line 16,17 of Algorithm EKF_localization_known_correspondences at page 204, ??? How to realize the accumulation of $\bar{\mu}_t=\bar{\mu}_t+K_t^i(z_t^i-\hat{z}_t^i)$ ????

6. page 401

   - **problem 1: For**
     $$
     \Omega_t^0 = F_{x,m^+,m^0}F_{x,m^+,m^0}^T\Omega_t F_{x,m^+,m^0}F_{x,m^+,m^0}^T
     $$
     **Is not $\Omega_t^0 = F_{x,m^+,m^0}^T\Omega_t F_{x,m^+,m^0}$ enough? Why do he multiply one more $F$ matrix**

   - **problem 2: We note that $\Omega_t^1,\Omega_t^2,\Omega_t^3$ could be obtained from $\Omega_t^0$, which means that they are margined from $p(x_t,m^0,m^+,m^-=0|z_{1:t},u_{1:t},c_{1:t})$. So, why they set $\Omega_t^0$ to be the information matrix of $p(x_t,m^0,m^+|m^-=0)$ in page 401?**

















