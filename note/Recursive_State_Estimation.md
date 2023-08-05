# Recursive State Estimation

## Basic concepts in probability

- conditional probability
  $$
  p(x|y) = \frac{p(x,y)}{p(y)}
  $$
  the factor $p(y)^{-1}$ is often denoted as $\eta$

  if X and Y are independent
  $$
  P(x|y)=\frac{p(x)p(y)}{p(y)}=p(x)
  $$

- conditional independence

  if X and Y are independent
  $$
  p(x,y|z)=p(x|z)p(y|z)\\
  p(x|z,y)=p(x|z)\\
  p(y|z,x)=p(y|z)
  $$
  p(x,y|z) means the joint probability of X and Y, conditioned on Z
  
  p(x|z,y) means the probability of x conditioned on joint event Z and Y
  
  p(y|z,x) means the probability of y conditioned on joint event Z and X
  
  derivation of $p(x|z,y)=p(x|z)$
  
  under the fact that $p(x,y|z)=p(x|z)p(y|z)$ if X and Y are independent
  $$
  p(z,y|z)=\frac{p(x,y,z)}{p(z)}\rightarrow p(x,y,z)=p(z)p(z,y|z)\\
  p(x|z,y)=\frac{p(x,y,z)}{p(y,z)}=\frac{p(x,y|z)p(z)}{p(y|z)p(z)}=\frac{p(x|z)p(y|z)p(z)}{p(y|z)p(z)}=p(x|z)
  $$
  **Conditional independence does not imply absolute independence**
  $$
  p(x,y|z)=p(x|z)p(y|z) \quad \nRightarrow \quad p(x,y)=p(x)p(y)
  $$
  The converse is also in general untrue: absolute independence does not imply conditional independence
  $$
  p(x,y)=p(x)p(y) \quad \nRightarrow \quad p(x,y|z)=p(x|z)p(y|z)
  $$

- Bayes rule

  Bayes rule relates a conditional of the type P(x|y) to its "inverse" p(y|x)
  $$
  p(x|y)=\frac{p(y|x)p(x)}{p(y)} = \frac{p(y|x)p(x)}{\sum_{x'}p(y|x')p(x')} \qquad (discrete)\\
  p(x|y)=\frac{p(y|x)p(x)}{p(y)} = \frac{p(y|x)p(x)}{\int_{x'}p(y|x')p(x')dx'} \qquad (continuous)
  $$
  the factor $p(y)^{-1}$ is always denoted as $\eta$

- entropy
  $$
  H_p(x)=E[-\log_2 p(x)] \rightarrow 
  \begin{cases}
  -\sum_x p(x)\log_2p(x) \quad (discrete)\\
  -\int p(x)\log_2 p(x) dx \quad (continuous)
  \end{cases}
  $$

## Robot Environment Interaction

the robot can acquire information about its environment using its sensors. The robot can also influence its environment through its actuators

### State

environments are characterized by state

state will be convenient to think of the state as the collection of all aspects of the robot and its environment that can impact the future

**state will be denoted $x$**

typical state variables: robot pose, robot manipulation, robot velocity and the velocities of its joints, the location and features of surrounding objects in the environment

#### complete state

a state $x_t$ will be called complete if it contains the knowledge of past states, measurements, or controls carry no additional information that would help us predict the future.

**completeness is commonly known as Markov property**























