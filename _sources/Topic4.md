## Ranking and Diffusion 

### Transition matrix 
Given a (undirected) graph $G=(V,E)$, we consider:
- The **adjacency matrix** $\mathbf{A}=[a_{ij}]\in \{0,1\}^{n\times n}$ of dimension $n\times n$, where $n=|V|$ is the number of nodes, and 

$$
a_{ij}= 
\begin{cases}
     1\;\text{if}\; (i,j)\in E  \\[2ex]
     0\; \text{otherwise}\;.
\end{cases}
$$

- The **degree matrix** $\mathbf{D}=[d_i]$ is an $n\times n$ diagonal matrix where $d_i = \sum_{j}a_{ij}$ is the degree $\text{deg}(i)$ of node $i$. 

Then, if the graph has no isolated nodes (none of them has zero degree) the so called **transition matrix** $\mathbf{P}=[p_{ij}]$, encoding the Markov chain associated with the nodes of the graph, is given by

$$
\mathbf{P} = \mathbf{D}^{-1}\mathbf{A}\;\;\text{i.e.}\;\; p_{ij} = \frac{a_{ij}}{d_i}\;.
$$

It is very interesting to remark the following properties of $\mathbf{P}$: 

- **Simply Stochastic (by rows)**. All the rows $i=1,2,\ldots, n$ satisfy: 

$$
\sum_{j=1}^n p_{ij} = 1\;.
$$

  i.e. each row $\mathbf{P}_{i:}$ (associated to a node $i$) *can be interpreted as a probability distribution*. 

- **Rank deficient**. In general, $\mathbf{P}$ is not invertible, i.e. $\text{rank}(\mathbf{P})\ll n$, and the higher the rank the more different (and thus informative) are the row probability distributions. 

#### Stationary Distribution
When we studied Markov chains in the context of random walks, we left aside the use of $\mathbf{P}$ for characterizing the Markov chain <span style="color:#469ff8">**in the limit**</span>. This means that we can obtain very interesting information about the nodes in $G=(V,E)$ by <span style="color:#469ff8">**analyzing the powers**</span> $\mathbf{P}^k$ for increasing values of $k=1,2,\ldots,\infty$.

Let us start by understanding the meaning of $\mathbf{P}$, $\mathbf{P}^2$, $\mathbf{P}^3$, etc. Actually $\mathbf{P}^k_{ij}$ is <span style="color:#469ff8">the probability of reaching node $j$ from $i$ in $k$ steps or **hops**</span>. 

Depending on the graph $G=(V,E)$ we may need only a small number of powers $k$. Consider for instance the **complete graph** or **clique graph** for $n$ nodes, dubbed $K_n$. The complete graph is the **denser graph than one can imagine** since it has $n$ nodes and each node has $n$ links (including self-loops). Therefore, the adjacency matrix of $K_n$ is: 

$$
\mathbf{A} = \mathbf{1}^T\mathbf{1}\;,
$$

where $\mathbf{1}$ is the $n\times 1$ vector of all ones, i.e. $\mathbf{A}$ is a matrix of ones. 

Well, the degree of each node in $K_n$ is constant  for each node and equal to $n$. Therefore, the transition matrix is 

$$
\mathbf{P} = \frac{1}{n}\mathbf{A},\;\; \text{with}\;\; p_{ij}=\frac{1}{n}\; \forall i,j\;.
$$

Then every node $i$ has the same probability of going to any other $j$ (including itself) in only one hop. In other words, a node $i$ does not need to visit first any other node before hitting $j$. This makes $\mathbf{P}^2$, $\mathbf{P}^3$, etc, *redundant* since

$$
\mathbf{P}^2 = \frac{1}{n}\mathbf{1}^T\mathbf{1}\cdot \frac{1}{n}\mathbf{1}^T\mathbf{1}
= \frac{1}{n^2}n\mathbf{1}^T\mathbf{1} = \frac{1}{n}\mathbf{1}^T\mathbf{1}=\mathbf{P}\;.
$$

This means that in $K_n$ (as well as in hyper-dense graphs), all the nodes have the same structural role. Note that in these case we have $\text{rank}(\mathbf{P})=1$. 

However, in more general graphs <span style="color:#469ff8">we can identify or **rank** the structural role of each node</span> by analyzing $\mathbf{P}^k$ for increasing values of $k$. 

Consider, for instance a Stochastic Block Model (SBM) graph of $n=20$ nodes with intra-class probaility $p=0.75$ and inter-class probability $q=0.05$ (see {numref}`Transition1`). 

```{figure} ./images/Topic4/Transition1.png
---
name: Transition1
width: 500px
align: center
height: 500px
---
SBM graph. Diffusion from $i=1$ ($0$ in the picture) at $\mathbf{f}^0$. 
```

Imagine that we inject information into node $i=0$ and <span style="color:#469ff8">see how such information is **diffused**</span> through the graph. We do that by setting a <span style="color:#469ff8">**row-probability vector**</span> $\mathbf{f}$ as follows: 

$$
\mathbf{f}^0 = [1\; 0\;\ldots\; 0]\;.
$$

Then, decomposing $\mathbf{P}=[\mathbf{P}_{:1}\;\mathbf{P}_{:2}\;\ldots\; \mathbf{P}_{:n}]$ in terms of its columns $\mathbf{P}_{:j}$  we have 

$$
\mathbf{f}^1 = \mathbf{f}^0\mathbf{P} = [\mathbf{f}^0\mathbf{P}_{:1}\;\mathbf{f}^0\mathbf{P}_{:2}\;\ldots\;\mathbf{f}^0\mathbf{P}_{:n}]
$$

where, starting at a general node $i$ leads to  

$$
\mathbf{f}^1_i = \sum_{j=1}^n\mathbf{f}^0_ip_{ij} = \sum_{j\in {\cal N}_i}^n\mathbf{f}^0_ip_{ij}\;.
$$

In particular, for $i=1$ we have a row vector $\mathbf{f}^1$ with $\mathbf{f}^1_i=p_{1j}$, i.e. we may reach any of the other nodes $j$ with probability $p_{1j}$. As we see in {numref}`Transition2`, in a first diffusion step, we only reach the nodes in the neigborhood of node $i=1$. 

```{figure} ./images/Topic4/Transition2.png
---
name: Transition2
width: 500px
align: center
height: 500px
---
SBM graph. Diffusion from $i=1$ ($0$ in the picture) at $\mathbf{f}^1$. 
```
Let us iterate again: 

$$
\mathbf{f}^2_i = \sum_{j=1}^n\mathbf{f}^1_ip_{ij} = \sum_{j\in {\cal N}_i}^n\mathbf{f}^1_ip_{ij}\;.
$$

Since, 

$$
\mathbf{f}^1\mathbf{P}=(\mathbf{f}^0\mathbf{P})\mathbf{P} = \mathbf{f}^0\mathbf{P}^2\;,
$$

we may reach the <span style="color:#469ff8">**second-order neighbors** of node $i$, i.e. the nodes that are **two-hops away from $i$**</span>, in particular some nodes of another community, as we see in {numref}`Transition3`.

```{figure} ./images/Topic4/Transition3.png
---
name: Transition3
width: 500px
align: center
height: 500px
---
SBM graph. Diffusion from $i=1$ ($0$ in the picture) at $\mathbf{f}^2$. 
```

Iterating again we state that we are more probable to be in the community of $i=1$, but we may jump to another community (see {numref}`Transition4`):  

$$
\mathbf{f}^3_i = \sum_{j=1}^n\mathbf{f}^2_i p_{ij} = \sum_{j\in {\cal N}_i}^n\mathbf{f}^2_ip_{ij}\;.
$$

```{figure} ./images/Topic4/Transition4.png
---
name: Transition4
width: 500px
align: center
height: 500px
---
SBM graph. Diffusion from $i=1$ ($0$ in the picture) at $\mathbf{f}^3$. 
```

Then, two interesting question arise: 
1) <span style="color:#469ff8">For what $t$ are the probabilities in $\mathbf{f}^{t}$ **stabilized**</span>? 

2) <span style="color:#469ff8">Is that **stabilized probability** the same for all choices of starting node.</span>?

**Stationary distribution**. Under certain conditions (see below) the answer to both questions is **Yes**. 

For $t\rightarrow\infty$ we have that if we reach a given row-distribution $\pi$, the resulting $\pi\mathbf{P}$ is exactly $\pi$, where

$$
\pi = \pi\mathbf{P}\;\;\text{and}\;\;\pi_i = \frac{d_i}{\text{vol}(G)}\;, 
$$

and $\text{vol}(G)=\sum_{i=1}^n d_i$ is the **volume** of the graph ($\text{vol}(G)=2|E|$ for undirected graphs). In other words, 
$\pi$ is a <span style="color:#469ff8">**fixed point** known as the **stationary distribution**</span> of $\mathbf{P}$. Actually it is very straight to prove that

$$
d_i = \sum_{j\in {\cal N}_i}d_ip_{ij}
    = \sum_{j\in {\cal N}_i}\frac{d_i}{d_i}
    = \sum_{j\in {\cal N}_i}1
    = d_i\;.
$$

Then, the stationary distribution $\pi$ is the result of normalizind the degree distribution by the volume. 

In our example, we show the stationary distribution for our SBM in {numref}`Stat`.

```{figure} ./images/Topic4/Stat.png
---
name: Stat
width: 500px
align: center
height: 500px
---
SBM graph. Stationary distribution $\pi$. 
```

In other words, reaching the stationary distribution in $t$ hops means that from any **discrete time** $t+\Delta t$, <span style="color:#469ff8">the probability of being at **any node** $i$  is only dependent on its degree $d_i$</span>.  

To clarify this point, note that we have that 

$$
\lim_{t\rightarrow\infty}\mathbf{P}^t = \Pi\;
$$

and $\Pi$ is a matrix where each row is a copy of the stationary distribution $\pi$. Look for instance at the row $i$: 

$$
\Pi_{i:} = \pi = [\frac{d_1}{\text{vol}(G)}\; \frac{d_2}{\text{vol}(G)}\;\ldots\; \frac{d_n}{\text{vol}(G)}\;]\;,
$$

i.e. the probability of going from $i$ to any other node $j$ is proportional to $d_j$, <span style="color:#469ff8">**indendendently of** whether $j$ is a neighbor of $i$ or not!</span>

Consider now the complete graph $K_n$, where each node can visit any other (including itself) with probability $\frac{1}{n} = \frac{n}{n^2}=\frac{d_i}{\sum_{i}d_i}$. In other words, <span style="color:#469ff8">a complete graph is a graph that has reached its stationary distribution at time $t=0$</span>. 

**Formal conditions**. The stationary distribution is unique if: 
1) The Markov chain is **irreducible** (all the states $i$ and $j$ are mutually reachable). For undirected graph it is enough that the graph is connected. For digraphs we must ensure that exists a directed path between any pair of nodes with is more difficult to achieve in realistic networks. 
2) The Markov chain is **aperiodic**. For satisfying this consition, we need that if there exists a positive integer $k$ s.t. all the entries in $\mathbf{P}^k$ are greater than zero. A less strict condition is to have at least a node with a self loop. 


#### The Spectral Interpretation: PageRank
The stationary distribution $\pi$, reshaped as a $n\times 1$ vector can be considered as a **left eigenvector** of the transition matrix for the **eigenvalue** $\lambda=1$ since 

$$
\phi^T\mathbf{P} = \lambda\phi^T\;\;\text{leads to}\; \pi^T\mathbf{P} = 1\cdot\pi^T\;.
$$

Similarly, the **right eigenvectors** and **eigenvalues** (typically we calculate these ones) are defined as: 

$$
\mathbf{P}\psi = \lambda\psi\;\;\text{leads to}\; \mathbf{P}\psi = 1\cdot\psi\;.
$$

Looking at the above equations, it is straightforward to prove that $\psi = \mathbf{D}^{1/2}\mathbf{1}$ is the right eigenvector of the transition matrix $\mathbf{P}$: 

$$
\begin{align}
\mathbf{P}\psi &=  \mathbf{D}^{-1}\mathbf{A}(\mathbf{D}^{1/2}\mathbf{1})\\
               &=  \mathbf{D}^{-1/2}\mathbf{D}^{-1/2}\mathbf{A}(\mathbf{D}^{1/2}\mathbf{1})\\
               &=  \mathbf{D}^{-1/2}\mathbf{A}\mathbf{D}^{-1/2}(\mathbf{D}^{1/2}\mathbf{1})\\
               &=  \mathbf{D}^{-1/2}\mathbf{A}(\mathbf{D}^{-1/2}\mathbf{D}^{1/2})\mathbf{1}\\
               &=  \mathbf{D}^{-1/2}\mathbf{A}\mathbf{1}\\
               & = \mathbf{D}^{-1/2}\mathbf{D}\mathbf{1}\;\;\text{from}\;\;\mathbf{A}\mathbf{1}=\mathbf{D}\mathbf{1}\\
               &= \mathbf{D}^{1/2}\mathbf{1}\\
               &= 1\cdot \psi\;.
\end{align}
$$

The meaning of $\psi = \mathbf{D}^{1/2}\mathbf{1}$ means that 

$$
\psi_i = \sqrt{d_i}\;
$$

is related to $\pi_i = \frac{d_i}{\text{vol}(G)}$, in terms that it is a monotonic function of $d_i$. Both $\pi$ and $\psi$ **rank** the importance of a node in the graph in terms of its degree. 

As we will see below, computing the right eigenvector is very interesting in practical settings, since <span style="color:#469ff8">it can be approximated even in networks/graphs not satisfying the formal conditions of irreducibility and aperiodicity</span>!

**Perron-Frobenius Theorem**. If $\mathbf{M}$ is a positive, *column stochastic matrix*, then:
1) $\lambda=1$ is an eigenvalue of multiplicity one (unique).
2) $\lambda=1$ is the largest eigenvalue: all the other eigenvalues have absolute value smaller than 1.
3) The eigenvectors corresponding to the eigenvalue $\lambda=1$ have either only positive entries or only negative entries. 
4) In particular, for the eigenvalue $\lambda=1$ there exists a unique eigenvector with the sum of its entries equal to 1 (a probability distribution).

Then $\mathbf{M}=\mathbf{P}^T$ satisfies this theorem. As in general every square matrix has the same eigenvalues as its transpose, we will approximate the left eigenvector of $\mathbf{P}$ by computing  

$$
\mathbf{P}^T\phi = (\phi^T\mathbf{P})^T = 1\cdot \phi\;.
$$

 and in practice we may approximate the eigenvector $\phi$ associated to $\lambda=1$ in an iterative way. To that end we use the **Power Method**. As we show in {prf:algorithm}`Power`, all we do is to: 
 


```{prf:algorithm} Power Method
:label: Power

**Inputs** Given an $n\times n$ matrix $\mathbf{M}$ and $\mathbf{x}=\frac{1}{n}\mathbf{1}$

**Output** Compute an approximation of the main eigenvector $\phi$

1. **for** each of the $k$ iterations:
    
    1. $\mathbf{x}\;\leftarrow \mathbf{M}\mathbf{x}$
    2. Normalize: $\mathbf{x} \;\leftarrow \frac{\mathbf{x}}{||\mathbf{x}||}$

2. **return** $\mathbf{x}$
```

1) Initialize $\mathbf{x}_i = \frac{1}{n}$ (completely random estimation of the eigenvector).
 2) For $M=\mathbf{P}^T$ compute $\mathbf{M}\mathbf{x}, \mathbf{M}^2\mathbf{x},\ldots, \mathbf{M}^k\mathbf{x}$.
 3) Between one power and the next, normalize the current eigenvector $\mathbf{x}$. 

```{figure} ./images/Topic4/MiniNet.png
---
name: MiniNet
width: 500px
align: center
height: 500px
---
Small digraph for computing the main eigenvector. 
```
<br></br>
<span style="color:#347fc9">
**Exercise**. Our digraph {numref}`MiniNet` is not aperiodic. This problem is not so hard as not being irreducible. In particular all the nodes are mutually reachable and this allows us to get a nice approximation.
</span>
<br><br>
<span style="color:#347fc9">
$
\mathbf{x}_0=\frac{1}{n}\mathbf{1} = 
\begin{bmatrix}
\frac{1}{4}\\
\frac{1}{4}\\
\frac{1}{4}\\
\frac{1}{4}\\
\end{bmatrix}\;\;
\mathbf{x}_1 = \mathbf{P^T}\mathbf{x}_0 = 
\begin{bmatrix}
0           &  0            &    1    &    \frac{1}{2}\\
\frac{1}{3} &  0            &    0    &      0        \\
\frac{1}{3} &  \frac{1}{2}  &    0    &    \frac{1}{2}\\
\frac{1}{3} &  \frac{1}{2}  &    0    &     0   \\     
\end{bmatrix}
\begin{bmatrix}
\frac{1}{4}\\
\frac{1}{4}\\
\frac{1}{4}\\
\frac{1}{4}\\
\end{bmatrix} = 
\begin{bmatrix}
0.375\\      
0.083\\ 
0.333\\ 
0.208\\
\end{bmatrix}
$
</span>
<br><br>
<span style="color:#347fc9">
$
\mathbf{x}_1=\frac{\mathbf{x}_1}{||\mathbf{x}_1||} = 
\begin{bmatrix}
0.682\\ 
0.151\\
0.606\\ 
0.379\\
\end{bmatrix}\;\;
\mathbf{x}_1 = \mathbf{P^T}\mathbf{x}_0 = 
\begin{bmatrix}
0           &  0            &    1    &    \frac{1}{2}\\
\frac{1}{3} &  0            &    0    &      0        \\
\frac{1}{3} &  \frac{1}{2}  &    0    &    \frac{1}{2}\\
\frac{1}{3} &  \frac{1}{2}  &    0    &     0   \\     
\end{bmatrix}
\begin{bmatrix}
0.682\\ 
0.151\\
0.606\\ 
0.379\\
\end{bmatrix} = 
\begin{bmatrix}
0.796\\ 
0.227\\ 
0.492\\ 
0.303\\
\end{bmatrix}
$
</span>
<br><br>
<span style="color:#347fc9">
$
\mathbf{x}_2=\frac{\mathbf{x}_2}{||\mathbf{x}_2||} = 
\begin{bmatrix}
0.788\\ 
0.225\\ 
0.487\\ 
0.300\\
\end{bmatrix}\;\;
\mathbf{x}_2 = \mathbf{P^T}\mathbf{x}_1 = 
\begin{bmatrix}
0           &  0            &    1    &    \frac{1}{2}\\
\frac{1}{3} &  0            &    0    &      0        \\
\frac{1}{3} &  \frac{1}{2}  &    0    &    \frac{1}{2}\\
\frac{1}{3} &  \frac{1}{2}  &    0    &     0   \\     
\end{bmatrix}
\begin{bmatrix}
0.788\\ 
0.225\\ 
0.487\\ 
0.300\\
\end{bmatrix} = 
\begin{bmatrix}
0.637\\ 
0.262\\ 
0.525\\ 
0.375\\
\end{bmatrix}
$
</span>
<br><br>
<span style="color:#347fc9">
at iteration $10$ we wil have
</span>
<span style="color:#347fc9">
$
\mathbf{x}_{9}=\frac{\mathbf{x}_{9}}{||\mathbf{x}_{9}||} = 
\begin{bmatrix}
0.720\\ 
0.240\\  
0.541\\ 
0.361\\
\end{bmatrix}\;\;
\mathbf{x}_{10} = \mathbf{P^T}\mathbf{x}_9 = 
\begin{bmatrix}
0           &  0            &    1    &    \frac{1}{2}\\
\frac{1}{3} &  0            &    0    &      0        \\
\frac{1}{3} &  \frac{1}{2}  &    0    &    \frac{1}{2}\\
\frac{1}{3} &  \frac{1}{2}  &    0    &     0   \\     
\end{bmatrix}
\begin{bmatrix}
0.720\\ 
0.240\\  
0.541\\ 
0.361\\
\end{bmatrix} = 
\begin{bmatrix}
0.722\\ 
0.240\\ 
0.540\\ 
0.360\\
\end{bmatrix}\;.
$
</span>
<br><br>
<span style="color:#347fc9">
Therefore, the most important node is node $1$, followed by nodes $3$, $4$ and $2$. Note that this result is quite different from the stationary distribution estimated in terms of **out degrees**: 
</span>
<br></br>
<span style="color:#347fc9">
$
\pi = \frac{\mathbf{D}_{out}\mathbf{1}}{\text{vol}(G)} = 
\begin{bmatrix}
0.375\\ 
0.25\\  
0.125\\ 
0.25\\
\end{bmatrix}\;.
$
</span>
<br><br>
<span style="color:#347fc9">
And also different from the theoretical right eigenvector:  
</span>
<br></br>
<span style="color:#347fc9">
$
\psi = \sqrt{\mathbf{D}_{out}}\mathbf{1} = 
\begin{bmatrix}
1.732\\ 
1.414\\ 
1.000\\         
1.414\\
\end{bmatrix}\;.
$
</span>
<br><br>
<span style="color:#347fc9">
Although in both cases, the top ranked node is correctly detected. 
</span>

**The Google Pagerank**. One of the most representative applications of the power method is to find the rankings of the web pages in the Internet. <span style="color:#469ff8">The higher the values (in absolute value) of the components of the resulting main eigenvector $\mathbf{x}$ the more important the page</span>. 

However, Internet (which can be considered a gigantic graph whose nodes are the web pages), does not necessarily meet the formal conditions needed for the unicity or convergence of $\mathbf{x}$. 

For instance, in {numref}`Pagerank` we summarize the main practical problems arising in realistic networks:
- **Sources**: nodes only with out degree, such as node $2$ which is only linked to $3$ and $4$. 
- **Sinks**: node with zero out degree, such as node $3$. 

In addition we may have **isolated nodes** or graphs fragmented in many **connected components**. 


```{figure} ./images/Topic4/Pagerank.png
---
name: Pagerank
width: 550px
align: center
height: 400px
---
Pagerank. Need of the Google matrix. 
``` 

The solution to these problems found by Page and Bruin when designing a model for the Google Internet surfer, was to complement the transition matrix (actually its transpose), with a complete graph so that with certain probability $1-\alpha$ (typically $1-\alpha=0.85$) we follow the transition matrix, but with a small probability $\alpha=0.15$ (dubbed the **teleporting probability**) we jump randomly to any other node or stay at the same mode (self-loop). Therefore, the so called **Google matrix**: 

$$
\mathbf{G} = (1-\alpha)\cdot\mathbf{P}^T + \alpha\cdot\frac{1}{n}\mathbf{1}^T\mathbf{1}\; 
$$

Therefore, the Google matrix consists of adding **virtual edges** between any pair of nodes (including self-loops). This makes the resulting Markov chain irreducible with facilitates information flow. In this regard, finding what is the probability that a surfer ends up clicking a given page is done via the Power method. 

<br></br>
<span style="color:#347fc9">
**Exercise**. We repeat the previous exercise by using the Google matrix for the digraph in {numref}`Pagerank`.
</span>
<br><br>
<span style="color:#347fc9">
$
\mathbf{x}_0=\frac{1}{n}\mathbf{1} = 
\begin{bmatrix}
\frac{1}{4}\\
\frac{1}{4}\\
\frac{1}{4}\\
\frac{1}{4}\\
\end{bmatrix}\;\;
\mathbf{x}_1 = \mathbf{G}\mathbf{x}_0 = 
\begin{bmatrix}
\alpha\frac{1}{4}           &  \alpha\frac{1}{4}             &    \alpha\frac{1}{4}     &    (1-\alpha)\frac{1}{2}\\
\alpha\frac{1}{4}           &  \alpha\frac{1}{4}             &    \alpha\frac{1}{4}     &      \alpha\frac{1}{4}         \\
(1-\alpha)\frac{1}{2} &  (1-\alpha)\frac{1}{2}  &    \alpha\frac{1}{4}     &    (1-\alpha)\frac{1}{2}\\
(1-\alpha)\frac{1}{2} &  (1-\alpha)\frac{1}{2}  &    \alpha\frac{1}{4}    &     \alpha\frac{1}{4}    \\     
\end{bmatrix} 
\begin{bmatrix}
\frac{1}{4}\\
\frac{1}{4}\\
\frac{1}{4}\\
\frac{1}{4}\\
\end{bmatrix} =
\begin{bmatrix}
\alpha\frac{1}{16} + \frac{2}{16}\\
\alpha\frac{4}{16}\\
\frac{6}{16}-\alpha\frac{5}{16}\\
\frac{4}{16}-\alpha\frac{2}{16}\\
\end{bmatrix}
$
</span>
<br></br>
<span style="color:#347fc9">
$
\mathbf{x}_1=\frac{\mathbf{x}_1}{||\mathbf{x}_1||} = 
\begin{bmatrix}
0.312\\
0.081\\ 
0.774\\  
0.543\\
\end{bmatrix}\;\;
\mathbf{x}_2 = \mathbf{G}\mathbf{x}_1 = 
\begin{bmatrix}
\alpha\frac{1}{4}           &  \alpha\frac{1}{4}             &    \alpha\frac{1}{4}     &    (1-\alpha)\frac{1}{2}\\
\alpha\frac{1}{4}           &  \alpha\frac{1}{4}             &    \alpha\frac{1}{4}     &      \alpha\frac{1}{4}         \\
(1-\alpha)\frac{1}{2} &  (1-\alpha)\frac{1}{2}  &    \alpha\frac{1}{4}     &    (1-\alpha)\frac{1}{2}\\
(1-\alpha)\frac{1}{2} &  (1-\alpha)\frac{1}{2}  &    \alpha\frac{1}{4}    &     \alpha\frac{1}{4}    \\     
\end{bmatrix} 
\begin{bmatrix}
0.312\\
0.081\\ 
0.774\\  
0.543\\
\end{bmatrix} =
\begin{bmatrix}
0.295\\ 
0.064\\ 
0.462\\ 
0.231\\
\end{bmatrix}
$
</span>
<br></br>
<span style="color:#347fc9">
at iteration $10$ we wil have
</span>
<br></br>
<span style="color:#347fc9">
$
\mathbf{x}_9=\frac{\mathbf{x}_9}{||\mathbf{x}_9||} = 
\begin{bmatrix}
0.264\\
0.066\\ 
0.484\\ 
0.286\\
\end{bmatrix}\;\;
\mathbf{x}_{10} = \mathbf{G}\mathbf{x}_9 = 
\begin{bmatrix}
\alpha\frac{1}{4}           &  \alpha\frac{1}{4}             &    \alpha\frac{1}{4}     &    (1-\alpha)\frac{1}{2}\\
\alpha\frac{1}{4}           &  \alpha\frac{1}{4}             &    \alpha\frac{1}{4}     &      \alpha\frac{1}{4}         \\
(1-\alpha)\frac{1}{2} &  (1-\alpha)\frac{1}{2}  &    \alpha\frac{1}{4}     &    (1-\alpha)\frac{1}{2}\\
(1-\alpha)\frac{1}{2} &  (1-\alpha)\frac{1}{2}  &    \alpha\frac{1}{4}    &     \alpha\frac{1}{4}    \\     
\end{bmatrix} 
\begin{bmatrix}
0.264\\
0.066\\ 
0.484\\ 
0.286\\
\end{bmatrix} =
\begin{bmatrix}
.422\\
.105\\ 
.774\\ 
.458\\
\end{bmatrix}
$
</span>
<br></br>
<span style="color:#347fc9">
Now, the top ranked node is $3$, the one with the largest **in-degree**. Nodes $1$ and $4$ are less accessible. Interestingly the node with the smallest rank is node $2$ which is only accessed randomly. 
</span>




