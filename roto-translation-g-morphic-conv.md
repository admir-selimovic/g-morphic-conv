
# Roto-Translation $G$-Morphic Convolution; $G = \text{SE}(2)$

In the standard interpretation of convolution, the kernel $k$ is simply translated (or shifted) across the function $f$ as part of the convolution operation, but it is not acted upon by the group representation. 
Let us take a nonstandard perspective on connvolution, where the kernel $k$ is being acted upon by the group representation $\lambda(g)$.

Essentially, group convolution $(k \ast f)(g)$ is a template matching between a kernel $k$, and an input $f$. First, $k$ is transformed by the action of the group, and then convolved with the input: 

$$
(k \ast f)(g) = \left(\lambda(g) k, f\right)
$$

Convolutions, in general, are not roto-translation $G$-maps:

\[\begin{tikzcd}
	f && f^{\star} \\
	\\
	f^{\lambda} && f^{\star \lambda} \neq f^{\lambda \star} \quad \quad \
	\arrow["\left((\cdot) \star k\right)(\mathbf{x})"{description}, from=1-1, to=1-3]
	\arrow["{\lambda(\theta)}"{description}, from=1-1, to=3-1]
	\arrow["{\lambda(\theta)}"{description}, from=1-3, to=3-3]
	\arrow["\left((\cdot) \star k\right)(\mathbf{x})"{description}, from=3-1, to=3-3]
\end{tikzcd}\]

This becomes evident when considering that the convolution operator ${\left(f \star k\right)(\mathbf{x}) = (f, \lambda(\mathbf{x}) k)}$ is defined by the representation $\lambda(\mathbf{x})$ of the translation group $\mathbb{R}^2$, while the other representation, $\lambda(\theta)$, corresponds to the rotation group $\mathrm{SO}(2)$. This results in non-commutativity. 

To define the cross-correlation operator for the group of rotations and translations, we start by considering an affine group $G$, which is the semidirect product of $\mathbb{R}^d$ and $H$. Such a group is the special Euclidean group $\mathrm{SE}(2)$, which combines translations in $\mathbb{R}^2$ and rotations in the special orthogonal group $\mathrm{SO}(2)$. By considering this group structure, we can perform group convolutions, which leverage the group's properties to define convolution operations.

Let us define the lifting cross-correlation, which involves a kernel $k$ transformed by the $\mathrm{SE}(2)$ group action $g=(\mathbf{x},\theta)$.
Consider the roto-translation group action on the kernel $k$:

$$
\begin{array}{rl}
(f \star k)(g) = (f \star k)(\mathbf{x}, \theta) & = \left(f, \lambda(g) \ k\right), \\
& = (f, \lambda(\mathbf{x}) \ \lambda(\theta) \ k), \\
& = \int k\left(\mathbf{R}(\theta)^{-1}\left(\mathbf{y}-\mathbf{x}\right)\right) f\left(\mathbf{y}\right) \mathrm{d} \mathbf{y}.
\end{array}
$$

where $\lambda(g)$ is the left regular group representation of $\mathrm{SE}(2)$, $\lambda(\mathbf{x})$ corresponds to the translation group representation, and $\lambda(\theta)$ corresponds to the rotation group representation. 

This formulation arises from the semi-direct product structure of affine groups. To provide more clarity, we separate the translation and rotation parts of the kernel transformation. The roto-translation group is defined as ${\mathrm{SE}(2)=\mathbb{R}^2 \rtimes \mathrm{SO}(2)}$. It is an affine group, that consists of a translation part $\mathbb{R}^2$ and a sub-transformation group $\mathrm{SO}(2)$ that acts upon the spatial part.
The translation part is represented by $\lambda({\mathbf{x})}$ and the rotation or subgroup transformation is represented by $\lambda(\theta)$, where $\theta$ is a 2D rotation angle parameter. The kernel $k$ is thus transformed by applying the composition of these two representations.

This convolution operation involves transforming the kernel $k$ by the inverse rotation $\mathbf{R}(\theta)^{-1}$ applied to the shifted coordinates $(\mathbf{y}-\mathbf{x})$. The transformed kernel is then convolved with the input signal $f(\mathbf{y})$ integrated over $\mathbb{R}^2$ with respect to $\mathbf{y}$. 

$\mathrm{SE}(2)$ group convolution allows for both translation and rotation $G$-mapping, achieved by applying convolutions over the spatial domain while considering the combined effects of translations and rotations. By doing so, we can capture the spatial relationships and patterns present in the data, taking into account both translation and rotation transformations.

Thus, the requirement we seek is:
\begin{center}
\hspace*{1cm} 
\begin{tikzcd}[row sep=60px, column sep =60px]
f 
\arrow[r, "((\cdot) \star k)(\mathbf{x} \comma \theta)"{description}]
\arrow[d, swap, "\lambda(\theta)"{description}, black]
 & f^{\star} 
\arrow[d, "\lambda(\theta)"{description}, black] 
 & \\
f^{\lambda} 
\arrow[r, black, "((\cdot) \star k)(\mathbf{x} \comma \theta)"{description} black]
 & f^{\star \lambda} \equiv f^{\lambda \star}
\end{tikzcd}
\end{center}

In the diagram, $f$ is the input feature map defined on $\mathbb{R}^2$. 
The operator $((\cdot) \star k)(\mathbf{x} , \theta)$ corresponds to the lifting cross-correlation, $((\cdot), \ \lambda(\mathbf{x}) \ \lambda(\theta) \ k)$, where $\lambda(\mathbf{x}): \mathbb{R}^2 \rightarrow \mathbb{R}^2$ and $\lambda(\theta): \mathrm{SO}(2) \rightarrow \mathbb{R}^2$. The final output feature map, $f^{\star \lambda} \equiv f^{\lambda \star}$, belongs to $\mathrm{SE}(2)$. 

The commutative nature of the diagram signifies that the order of applying lifting cross-correlation and rotation does not affect the outcome. Hence, we describe $\mathrm{SE}(2)$ group lifting convolutions as roto-translation $G$-map.
