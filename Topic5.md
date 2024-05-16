## Distances and Latent Spaces  

### Normalized Laplacian
#### Derivation  
The normalized Laplacian $\tilde{\triangle}$ is a slight modification of the Laplacian which was initially designed for relating the spectra of transition matrices and Laplacian matrices. Actually, the first chapters of the book of [Fan Chung-Graham](https://mathweb.ucsd.edu/~fan/research/revised.html) are a must for students interested in spectral graph theory, though the level is very top in mathematical terms. Herein we will refer to basic concepts for the perusal of AIers. 

**Derivation from the Transition**. Remember the **transition** matrix of $G=(V,E)$: 

$$
\mathbf{P} = \mathbf{D}^{-1}\mathbf{A}\;\;\text{i.e.}\;\; p_{ij} = \frac{a_{ij}}{d_i}\;.
$$

If $\mathbf{P}$ is irreducible and aperiodic (for instance the one given by the Google matrix), we have that the spectrum (eigenvalues) of $\mathbf{P}$ satisfy: 

$$
1=\lambda_1\ge\lambda_2\ge \ldots \ge \lambda_n>-1\;.
$$

Let us now define the following matrix $\tilde{\mathbf{P}}$ (which is different from $\mathbf{P}$):  

$$
\tilde{\mathbf{P}} = \mathbf{D}^{-1/2}\mathbf{A}\mathbf{D}^{-1/2}\;,
$$

where $\mathbf{D}^{-1/2}$ is the diagonal matrix with elements $1/\sqrt{d_i}$. 

Then, the **normalized Laplacian** is given by 

$$
\tilde{\triangle} = \mathbf{I} - \tilde{\mathbf{P}} = \mathbf{I} - \mathbf{D}^{-1/2}\mathbf{A}\mathbf{D}^{-1/2}\;,
$$

where $\mathbf{I}$ is the identity matrix of size $|V|$. It turns out that <span style="color:#469ff8">if $\lambda_k$ is an eigenvalue of $\mathbf{P}$, then $1 - \lambda_k$ is an eigenvalue of $\tilde{\triangle}$ and vice versa</span>. 


**Derivation from the Laplacian**. In her book, Fan Chun approaches the normalized Laplacian in a different way. Consider now the (unnormalized) Laplacian 

$$
\triangle = \mathbf{D} - \mathbf{A}\;.
$$

Let us define $\tilde{\triangle}$ as the pre-multiplication and post-multipliplication of $\triangle$ by $\mathbf{D}^{-1/2}$ (degree normalization): 

$$
\begin{align}
\tilde{\triangle}=\mathbf{D}^{-1/2}\triangle \mathbf{D}^{-1/2} &= \mathbf{D}^{-1/2}(\mathbf{D} - \mathbf{A})\mathbf{D}^{-1/2}\\
&= \mathbf{D}^{-1/2}\mathbf{D}\mathbf{D}^{-1/2} - \mathbf{D}^{-1/2}\mathbf{A}\mathbf{D}^{-1/2}\\
&=  \mathbf{I} - {D}^{-1/2}\mathbf{A}\mathbf{D}^{-1/2}\\
&=  \mathbf{I} - \tilde{\mathbf{P}}\;.
\end{align}
$$

Then, the **component-wise** structure of $\tilde{\triangle}$ is

$$
\tilde{\triangle}_{ij}= 
\begin{cases}
     -\frac{1}{\sqrt{d_i}\sqrt{d_j}}\;\text{if}\; (i,j)\in E  \\[2ex]
     1\;\text{if}\; i=j \;\text{and}\; d_i\neq 0\\[2ex]
     0\; \text{otherwise}\;,
\end{cases}
$$

i.e. in the diagonal we have $\tilde{\triangle}_{ii}=1$ (normalized) and in the off-diagonal we will have $-\frac{1}{\sqrt{d_id_j}}$.

**Link between the eigenvectors**. <span style="color:#469ff8">If $\phi$ and $\tilde{\phi}$ are  respectively eigenvectors of $\triangle$ and $\tilde{\triangle}$, they are related by the equations: $\tilde{\phi}=\mathbf{D}^{1/2}\phi$ and $\phi=\mathbf{D}^{-1/2}\tilde{\phi}$</span>: 

$$
\begin{align}
\tilde{\triangle}\tilde{\phi} = \lambda\tilde{\phi}\;
&\Rightarrow 
\mathbf{D}^{-1/2}\triangle\mathbf{D}^{-1/2}\tilde{\phi} = \lambda\tilde{\phi}\\
&\Rightarrow 
\mathbf{D}^{-1/2}\triangle\mathbf{D}^{-1/2}(\mathbf{D}^{1/2}\phi) = \lambda(\mathbf{D}^{1/2}\phi)\\
&\Rightarrow 
\mathbf{D}^{-1/2}\triangle\phi = \lambda\mathbf{D}^{1/2}\phi\\
&\Rightarrow 
\mathbf{D}^{1/2}\mathbf{D}^{-1/2}\triangle\phi = \mathbf{D}^{-1/2}\lambda\mathbf{D}^{1/2}\phi\\
&\Rightarrow 
\triangle\phi = \mathbf{D}^{1/2}\lambda\mathbf{D}^{1/2}\phi\\
&\Rightarrow 
\triangle\phi = \lambda\mathbf{D}\phi\;.\\
\end{align}
$$

In other words, the eigenvectors of $\tilde{\triangle}$ are the **generalized eigenvectors** of $\triangle$.

For instance, as $\mathbf{1}$ is the eigenvector of $\triangle$ with eigenvalue $\lambda_1=0$, then $\mathbf{D}^{1/2}\mathbf{1}$ is the corresponding eigenvector for $\tilde{\triangle}$. This means that <span style="color:#469ff8">the Fiedler vector associated with the normalized Laplacian must be perpendicular to $\mathbf{D}\mathbf{1}$</span>.

#### Spectral properties of graphs
In general, using the normalized Laplacian we obtain more robust estimators and this is why some properties of the graph that can be identified simply by looking at the spectrum of $\tilde{\triangle}$ are enunciated. 

Let $n=|V|$ in $G=(V,E)$. Then:

1) <span style="color:#469ff8">**Sum of spectra**</span>. The sum of all eigenvalues is $\sum_i\lambda_i\le n$, with equality only if the graph is connected. The proof is trivial since the trace of the matrix (sum of the diagonal) satisfies $\text{Tr}[\tilde{\triangle}]=\sum_{i}\lambda_i$.

2) <span style="color:#469ff8">**Bound of the spectra**</span>. For all $i\le n$ we have $\lambda_i\le 2$, with $\lambda_n=2$ only if a connected component of the graph is bipartite.

3) <span style="color:#469ff8">**Extent of the spectra**</span>. A graph without isolated nodes satisfies $\lambda_n\ge \frac{n}{n-1}$ with equality if the graph is complete (without self-loops).

4) <span style="color:#469ff8">**Number of connected components**</span>. There are $k$ connected components if $\lambda_1=\lambda_2=\ldots=\lambda_k = 0$.

<span style="color:#469ff8">**Algebraic connectivity $\lambda_2$**</span>. The second smallest eigenvalue of $\tilde{\triangle}$ (the Fiedler value) is one of the most informative since:

5) $\lambda_2\le \frac{n}{n-1}$ with equality only if $G$ is the complete graph (without self-loops)
6) $\lambda_2<1$ if the $G$ is not complete. 
7) The diameter $D$ of $G$ (length of the shortest path between any pair of nodes) satisfies: $\frac{1}{D\text{vol}G}<\lambda_2$. 

Some **examples of graph spectra** (from Chung's book):
- **Complete graph** $K_n$(without self-loops): is $0$ and $\frac{n}{n-1}$ (with multiplicity $n-1$). 
- **Star graph (hub)** $S_n$: is $0$, $1$ (with multiplicity $n-2$) and $2$. 
- **Path graph** $P_n$: is $1-\cos\frac{\pi k}{n-1}$ for $k=0,1,\ldots,n-1$. 
- **Cycle graph** $C_n$: is $1-\cos\frac{2\pi k}{n}$ for $k=0,1,\ldots,n-1$.


##### The Cheeger constant 
The Fiedler value $\lambda_2$ is frequently used to <span style="color:#469ff8">**quantify how weak is the graph**</span> (the smaller $\lambda_2$ the weaker $G$). This is particularly interesting when bounding the so called **Cheeger constant**. We define it as follows: 

Consider a partition $V=A\cup \bar{A}$, $A\cap \bar{A}=\emptyset$, then the *conductance* of the partition is  

$$
h(A) = \frac{cut(A,\bar{A})}{\min\{|A|,|\bar{A}|\}}\;, 
$$

and the Cheeger constant is the *minimum conductance por any partition of $V$ (defined as by subset $A\subseteq V$ and its complementary $\bar{A}=V-A$): 

$$
h_G = \min_{A\subseteq V}h(A)\;.
$$

Since its seems that minimizing the Cheeger constant is quite similar to minimizing $\text{Rcut}(A,\bar{A})$, it is not surprising that computing the Cheeger constant is NP-hard (we must evaluate all the possible $2^{|V|}$ partitions/subsets of $V$). However, since we have the Fiedler value, which is $\lambda_2>0$ for a connected graph, we have the following fundamental bound of spectral graph theory: 

$$
2h_G\ge \lambda_2\ge \frac{h_G^2}{2}\;.
$$

The proof can be found in Chung's book (Chapter~2). Anyway, this bound is interesting since it tells us how precise is the approximation of the Cheeger constant by using $\lambda_2$ (also known as the <span style="color:#469ff8">**spectral gap**</span>). <span style="color:#469ff8">The wider the bottleneck  of the graph (large conductance) the worse the approximation</span>.

##### The Mixing time
<span style="color:#469ff8">The **spectral gap** $\lambda_2$ is also key to characterize the mixing time of a graph</span>. Remember that the mixing time of a transition matrix $\mathbf{P}$ associated with a graph $G=(V,E)$ is the time needed to reach the steady state distribution $\pi$ where the probability of going from a given node $i$ to any other $i$ is proportional to the degree of the destination: $\pi_i=\frac{d_j}{\text{vol}(G)}$. 

In order to explain the link between the spectral gap and the mixing time we follow some formal steps: 

1) <span style="color:#469ff8">**Link the matrices**</span> $\mathbf{P}$ and $\tilde{\mathbf{P}}$.
2) <span style="color:#469ff8">**Link the eigenvectors**</span> of $\mathbf{P}$ and $\tilde{\mathbf{P}}$.
3) <span style="color:#469ff8">**Apply the spectral theorem**</span>.

**Link the matrices**. The matrices $\mathbf{P}=\mathbf{D}^{-1}\mathbf{A}$ and $\tilde{\mathbf{P}}=\mathbf{D}^{-1/2}\mathbf{A}\mathbf{D}^{-1/2}$ are related as follows: 

$$
\begin{align}
\tilde{\mathbf{P}}=\mathbf{D}^{-1/2}\mathbf{A}\mathbf{D}^{-1/2}
&\Rightarrow 
\mathbf{D}^{-1/2}\tilde{\mathbf{P}}=\mathbf{D}^{-1/2}\mathbf{D}^{-1/2}\mathbf{A}\mathbf{D}^{-1/2}\\
&\Rightarrow 
\mathbf{D}^{-1/2}\tilde{\mathbf{P}}=\mathbf{D}^{-1}\mathbf{A}\mathbf{D}^{-1/2}\\
&\Rightarrow 
\mathbf{D}^{-1/2}\tilde{\mathbf{P}}\mathbf{D}^{1/2}=\mathbf{D}^{-1}\mathbf{A}\mathbf{D}^{-1/2}\mathbf{D}^{1/2}\\
&\Rightarrow 
\mathbf{D}^{-1/2}\tilde{\mathbf{P}}\mathbf{D}^{1/2}=\mathbf{D}^{-1}\mathbf{A}\\
&\Rightarrow 
\mathbf{D}^{-1/2}\tilde{\mathbf{P}}\mathbf{D}^{1/2}=\mathbf{P}
\end{align}
$$

i.e.
$
\mathbf{P} = \mathbf{D}^{-1/2}\tilde{\mathbf{P}}\mathbf{D}^{1/2}\;.
$

**Link the eigenvectors**. If $\phi$ is an eigenvector of $\mathbf{P}$ with eigenvalue $\lambda$, then $\tilde{\phi}=\mathbf{D}^{1/2}\phi$ is an eigenvector of $\tilde{\mathbf{P}}$ with the same eigenvalue $\lambda$: 

$$
\begin{align}
\mathbf{P}\phi = \lambda\phi\;
&\Rightarrow 
\mathbf{D}^{-1/2}\tilde{\mathbf{P}}\mathbf{D}^{1/2}\phi = \lambda\phi\\
&\Rightarrow 
\mathbf{D}^{1/2}\mathbf{D}^{-1/2}\tilde{\mathbf{P}}\mathbf{D}^{1/2}\phi = \lambda\mathbf{D}^{1/2}\phi\\
&\Rightarrow 
\tilde{\mathbf{P}}\mathbf{D}^{1/2}\phi = \lambda\mathbf{D}^{1/2}\phi\\
&\Rightarrow 
\tilde{\mathbf{P}}\tilde{\phi} = \lambda\tilde{\phi}\\
\end{align}
$$

**Apply the spectral theorem**. Firstly, we apply the spectral theorem to $\tilde{\mathbf{P}}$: 

$$
\tilde{\mathbf{P}}=\sum_{i=1}^{n}\lambda_i\tilde{\phi}_i\tilde{\phi}_i^T\;,
$$

Then, following Lovasz's [Random Walks on Graphs: A Survey](https://www.cse.cuhk.edu.hk/~cslui/CMSC5734/LovaszRadnomWalks93.pdf) we plug the above expansion in $\mathbf{P} = \mathbf{D}^{-1/2}\tilde{\mathbf{P}}\mathbf{D}^{1/2}$: 

$$
\mathbf{P} = \mathbf{D}^{-1/2}\tilde{\mathbf{P}}\mathbf{D}^{1/2} = \sum_{i=1}^n\lambda_i\mathbf{D}^{-1/2}\tilde{\phi}_i\tilde{\phi}_i^T\mathbf{D}^{1/2}\;.
$$

Now, we expand the above expression as follows:

$$
\mathbf{P} = \lambda_1\mathbf{D}^{-1/2}\tilde{\phi}_1\tilde{\phi}_1^T\mathbf{D}^{1/2} + \sum_{i=2}^n\lambda_i\mathbf{D}^{-1/2}\tilde{\phi}_i\tilde{\phi}_i^T\mathbf{D}^{1/2}\;.
$$

Since $\lambda_1=1$ and $\tilde{\phi}_1=\mathbf{D}^{1/2}\mathbf{1}$, the first term of the above expression becomes: 

$$
\begin{align}
1\cdot\mathbf{D}^{-1/2}\tilde{\phi}_1\tilde{\phi}_1^T\mathbf{D}^{1/2} 
&= 
\mathbf{D}^{-1/2}\mathbf{D}^{1/2}\mathbf{1}(\mathbf{D}^{1/2}\mathbf{1})^T\mathbf{D}^{1/2}\\ 
&= 
\mathbf{1}\mathbf{1}^T\mathbf{D}^{1/2}\mathbf{D}^{1/2}\\
&= 
\mathbf{1}\mathbf{1}^T\mathbf{D}\\
&= 
\mathbf{1}\mathbf{1}^T\mathbf{D}\\
\end{align}
$$

where we define $\mathbf{Q}=\mathbf{1}\mathbf{1}^T\mathbf{D}$ is a matrix whose all rows are repeated and they are equal to 

$$
\mathbf{Q}_{i:}=[d_1\; d_2\; \ldots\; d_n]\;,
$$

Remember (from the previous topic) that 

$$
\lim_{t\rightarrow\infty}\mathbf{P}^t = \Pi\;
$$

where 

$$
\Pi_{i:} = \pi = [\frac{d_1}{\text{vol}(G)}\; \frac{d_2}{\text{vol}(G)}\;\ldots\; \frac{d_n}{\text{vol}(G)}\;]\;,
$$

i.e. all the stationary distribution is repeated in each row of $\Pi$.

As a result, $\Pi$ is just a **normalized version** of $\mathbf{Q}$, i.e. we may interpret $\mathbf{Q}_{i:}$ as an **unnormalized degree distribution**. This is exactly all we need for the proof since we have: 

$$
\begin{align}
\mathbf{P} &= \mathbf{Q} + \sum_{i=2}^n\lambda_i\mathbf{D}^{-1/2}\tilde{\phi}_i\tilde{\phi}_i^T\mathbf{D}^{1/2}
\\
&\approx \Pi + \sum_{i=2}^n\lambda_i\mathbf{D}^{-1/2}\tilde{\phi}_i\tilde{\phi}_i^T\mathbf{D}^{1/2}\\
&\approx \Pi + \sum_{i=2}^n\lambda_i\mathbf{D}^{-1/2}\mathbf{R}_i\mathbf{D}^{1/2}\;,
\end{align}
$$

Now, each term $\tilde{\phi}_i\tilde{\phi}_i^T$ is an $n\times n$ matrix $\mathbf{R}_i$ where $\mathbf{R}_i(u,v)=\tilde{\phi}_i(u)\tilde{\phi}_i(v)$. 

As a result, taking the components $p_{uv}$ of $\mathbf{P}$, we have: 

$$
p_{uv} \approx \pi_{uv} + \sum_{i=2}^n\lambda_i\tilde{\phi}_i(u)\tilde{\phi}_i(v)\sqrt{\frac{d_v}{d_u}}\;.
$$

Finally, applying the **spectral problem** to the power $\mathbf{P}^t$ we have

$$
\mathbf{P}^t=\sum_{i=1}^{n}\lambda_i^t\phi_i\phi_i^T\;,
$$

i.e. <span style="color:#469ff8">any **matricial function** (e.g the power, exponential, logartithn) is **transferred to the spectrum**!</span>

Using this result, we have that

$$
p_{uv}^t \approx \pi_{uv} + \sum_{i=2}^n\lambda_i^t\tilde{\phi}_i(u)\tilde{\phi}_i(v)\sqrt{\frac{d_v}{d_u}}\;.
$$

Which leads to

$$
p^t(v) \approx \pi(v) + \sum_{i=2}^n\lambda_i\tilde{\phi}_i(u)\tilde{\phi}_i(v)\sqrt{\frac{d_v}{d_u}}\;.
$$

Then, the **rate of convergence** of $\mathbf{P}$ to $\Pi$ is given by 

$$
\begin{align}
p^t(v) - \pi(v) &\approx \sum_{i=2}^n\lambda_i\tilde{\phi}_i(u)\tilde{\phi}_i(v)\sqrt{\frac{d_v}{d_u}}\\
|p^t(v) - \pi(v)| &\approx \left|\sum_{i=2}^n\lambda_i\tilde{\phi}_i(u)\tilde{\phi}_i(v)\sqrt{\frac{d_v}{d_u}}\right|\\
&< |\lambda_2^t|\left|\sum_{i=2}^n\tilde{\phi}_i(u)\tilde{\phi}_i(v)\sqrt{\frac{d_v}{d_u}}\right|\\
&< |\lambda_2^t|\cdot\sqrt{\frac{d_v}{d_u}}\;.
\end{align}
$$

where the last simplification is due to the fact that 
$\sum_{i=2}^n\tilde{\phi}_i(u)\tilde{\phi}_i(v)\le 1$ since the eigenvectors are orthonormal: $\tilde{\Phi}\tilde{\Phi}^T=\mathbf{I}$. 

Then, <span style="color:#469ff8">the rate of convergence to the steady distribution is fast if the spectral gap is small</span>! 

### Commute Times and Embedding
#### Spectral Commute Times
The commute time $CT(u,v)=H(u,v)+H(v,u)$ between two nodes $u$ and $v$ is the expected time needed by a random walk departing from $u$ to reach $v$ (hitting time $H(u,v)$) and come back (hit $u$ from $v$, $H(v,u)$).

<span style="color:#469ff8">**Green's function**</span>. A key matrix to compute both the hitting and commute times is the so called **Green's function** $G$ or pseudoinverse $\triangle^{+}$ of the Laplacian $\triangle$. For a connected graph, we have the following component-wise equation (see the yet classic paper of my mentor [Edwin Hancock](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=4302755)): 

$$
G(u,v) = \sum_{i=2}^{|V|}\frac{1}{\lambda_i}\phi_i(u)\phi_i(v)\; 
$$

<span style="color:#469ff8">**Hitting time**</span>. $H(u,v)$ is spectrally determined by 

$$
\begin{align}
H(u,v) &= \text{vol}(G)\left[G(v,v) - G(u,v)\right]\\
&= \text{vol}(G)\left[\sum_{i=2}^{|V|}\frac{1}{\lambda_i}\phi_i(v)^2\ - \sum_{i=2}^{|V|}\frac{1}{\lambda_i}\phi_i(u)\phi_i(v)\right]\\
&= \text{vol}(G)\sum_{i=2}^{|V|}\frac{1}{\lambda_i}\left[\phi_i(v)^2-\phi_i(u)\phi_i(v)\right]\\
&= \text{vol}(G)\frac{1}{\lambda_2}\left[\phi_2(v)^2-\phi_2(u)\phi_2(v)\right] + \ldots + \text{vol}(G)\frac{1}{\lambda_n}\left[\phi_n(v)^2-\phi_n(u)\phi_n(v)\right]\;.
\end{align}
$$

Since $\lambda_2\le\lambda_3\le\ldots\le\lambda_n$, the importance of each term in the sum is inversely proportional to the corresponding $\lambda_i$. This means that if $\lambda_2\rightarrow 0$ (very small spectral gap), we have: 

$$
H(u,v)\approx \text{vol}(G)\left[\phi_2(v)^2-\phi_2(u)\phi_2(v)\right]\;.
$$

**Reminder**. It is key to note that in general $H(u,v)\neq H(v,u)$.

<span style="color:#469ff8">**Commute time**</span>. $CT(u,v)=H(u,v) + H(v,u)$ is spectrally determined by the spectral computations of $H(u,v)$ and $H(v,u)$:

$$
\begin{align}
\frac{CT(u,v)}{\text{vol}(G)}  &= H(u,v) + H(v,u)\\
        &= G(v,v) - G(u,v) + G(u,u) - G(v,u)\\
        &= G(u,u) + G(v,v) - 2G(u,v)\;.
\end{align}
$$

<span style="color:#469ff8">**Commute times are metrics**</span>. Then, $CT(u,v)=\text{vol}(G)\left[G(u,u) + G(v,v) - 2G(u,v)\right]$ because the Green's function is commutative $G(u,v)=G(v,u)$. As a result, $CT(u,v)$ <span style="color:#469ff8">is formally a **distance** between two nodes</span>. 

Then, the spectral computation of the commute time can be derived easily and results in

$$
CT(u,v) = \text{vol}(G)\sum_{i=2}^{|V|}\frac{1}{\lambda_i}\left[\phi_i(u)^2-\phi_i(v)^2\right]\;.
$$

Again, if $\lambda_2\rightarrow 0$, we have: 

$$
CT(u,v) = \text{vol}(G)\frac{1}{\lambda_2}\left[\phi_2(u)^2-\phi_2^2(v)\right]\;.
$$

Consider, for instance the SBM example with $n=20$ nodes of the last topic. The Fiedler vector is mapped in {numref}`Fiedler`.


```{figure} ./images/Topic5/Fiedler.png
---
name: Fiedler
width: 500px
align: center
height: 480px
---
SBM graph. Fiedler vector and Fiedler value. 
```

It is not surpising to see that the commute time between nodes in the same community is quite similar. Let us check the pairwise matrix of the $CT$s between every pair of nodes $u$ and $v$ in {numref}`Pairwise`.

```{figure} ./images/Topic5/Pairwise.png
---
name: Pairwise
width: 800px
align: center
height: 480px
---
SBM graph. CT matrix and CT embedding. 
```

#### Commute Times Embedding
<span style="color:#469ff8">**Embedding**</span> the nodes of a graph consists of finding a vector representation of each node $\Theta_u,\;u\in V$ where the Euclidean distance $\|\Theta_u-\Theta_v\|$ is consistent with the <span style="color:#469ff8">**structural distance** between the nodes in the graph</span>.

Since the commute times is by definition a distance, it is trivial to check that the columns of this matrix  

$$
\Theta = \sqrt{\text{vol}(G)}\mathbf{D}^{-1/2}\Phi^T\;\Rightarrow CT(u,v) = \|\Theta_u - \Theta_v\|^2
$$

where $\Phi$ is the matrix of eigenvectors (columns from the smallest to the largest eigenvectors). Again, depending on the value of $\lambda_2$ not all eigenvectors are needed. See for instance in {numref}`Pairwise` the results of the embedding for $3D$ (eigenvalues/eigenvectors $2$, $3$ and $4$). 

