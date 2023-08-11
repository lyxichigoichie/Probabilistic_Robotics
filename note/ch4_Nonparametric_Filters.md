# Nonparametric Filter

Nonparametric filters do not rely on a fixed functional form of the posterior, such as Gaussian. Instead, they approximate posteriors by a finite number of values, each roughly corresponding to a region in state space. Some nonparametric Bayes filters rely on a decomposition of the state space, in which each such value corresponds to the cumulative probability of the posterior density in a compact subregion of the state space. Others approximate the state space by random samples drawn from the posterior distribution.

## Histogram Filter

**Histogram filters decompose the state space into finitely many regions and represent the cumulative posterior for each region by a single probability value. ** When applied to **finite spaces**, 

 such filter are known as discrete Bayes filters, when applied to **continuous spaces**, they are commonly called histogram filters.

### The Discrete Bayes Filter Algorithm

![](figures/ch4/Discrete_Bayes_filter_algorithm.png)

the belief at time t is an assignment of a probability to each state $x_k$, denoted $p_{k,t}$

### Continuous State

Histogram filter **decompose a continuous state space into finitely regions**
$$
\mathrm{dom}(X_t) = \mathbf{x}_{1,t} \cup \mathbf{x}_{2,t} \cup \ldots \cup \mathbf{x}_{K,t}
$$
**here $\mathbf{x}_{k,t}$ is a region**, notation $\mathrm{dom}$ is means of domain

for each $i \neq k$, we have $\mathbf{x}_{i,t} \cap \mathbf{x}_{k,t}$

after decomposing the continuous state space into finitely regions, we assign discrete Bayes filter to each region $\mathbf{x}_{k,t}$ and belief $p_{k,t}$, which means that **uniform probability to each state $x_t$ within each region $\mathbf{x}_{k,t}$
$$
p(x_t) = \frac{p_{k,t}}{|\mathbf{x}_{k,t}|}
$$






























