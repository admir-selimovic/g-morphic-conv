
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

## Example

As an example, consider the Sobel operator for the kernel $k_a$. The Sobel operator is used in image processing and computer vision to perform a 2D spatial gradient measurement on an image, emphasizing edges and transitions. $k$, as defined above, responds maximally to edges running vertically and minimally to edges running horizontally.

<div align="center"> 
  <img src="https://github.com/admir-selimovic/g-morphic-conv/blob/main/img/g-morph-conv-diag.png" width="400">
</div>

When a kernel is rotated, such as $\lambda_{\theta} k_a$, and cross-correlated with a two-dimensional feature map $f_a$, it produces a three-dimensional lifted feature map $f_b$. This lifted feature map is no longer dependent solely on the coordinates $x$ and $y$, as it accounts for both translation and rotation. Therefore, an additional axis $\theta$ is added to represent the subgroup of rotations. The term \textit{lifting }refers to the inclusion of an additional axis ($\theta$) in the output, which disentangles features under rotational transformations. Consequently, the output feature map $f_b$ becomes three-dimensional due to the presence of the additional axis.

In the diagram above, $f_a$ is the input feature map in $L^2(\mathbb{R}^2)$. The operator $(k_a \ast f_a)(\mathbf{x}, \theta)$ corresponds to the lifting cross-correlation, where ${\lambda^a_\mathbf{x}: \mathbb{R}^2 \rightarrow L^2\left(\mathbb{R}^2\right)}$ and ${\lambda^a_\theta: SO(2) \rightarrow L^2\left(\mathbb{R}^2\right)}$ denote the translations and rotations, respectively. Similarly, $(k_b \ast f_c)(\mathbf{x}, \theta)$ represents the subsequent layer lifting cross-correlation operation, with ${\lambda^b_\mathbf{x}: \mathbb{R}^2 \rightarrow L^2\left(SE(2)\right)}$ and ${\lambda^b_\theta: SO(2) \rightarrow L^2\left(SE(2)\right)}$ representing the translations and rotations involved. The final output feature map belongs to $L^2(SE(2))$. Recall that $SO(2)$ represents rotations around the origin in a two-dimensional plane, while $SE(2)$ includes rotations and translations but not reflections.


## Proof

Let us prove the $G$-map requirement:

$$
\lambda(g)^{\mathrm{SO}(2)} (f \star (\lambda(g)^{\mathrm{SE}(2)} k)) = (\lambda(g)^{\mathrm{SO}(2)} f) \star (\lambda(g)^{\mathrm{SE}(2)} k)
$$

Given the roto-translation action on the kernel, we can express explicitly the kernel's transformation under the group action of $\mathrm{SE}(2)$ as:

$$ 
\lambda(g)^{\mathrm{SE}(2)} k = k(\mathbf{R}^{-1}(\theta)((\mathbf{y}-\mathbf{x})-\mathbf{t}))
$$

Given the rotation action on $f$, we can express explicitly its transformation under the group action of $\mathrm{SO}(2)$ as:

$$
\lambda(g)^{\mathrm{SO}(2)} f = f \left(\mathbf{R}^{-1}(\theta) \ \mathbf{y} \right)
$$

We will use the substitution $\mathbf{y} \rightarrow \mathbf{y}+\mathbf{x}$. 
Starting with the left-hand side, we have:

$$
\begin{aligned}
\lambda(g)^{\mathrm{SO}(2)} (f \star (\lambda(g)^{\mathrm{SE}(2)} k))(\mathbf{x}) 
&= \lambda(g)^{\mathrm{SO}(2)} \left( \sum_{{\mathbf{y}} \in \mathbb{Z}^2} f({\mathbf{y}}) \ k\left(\mathbf{R}^{-1}(\theta)\left(\left(\mathbf{y}-\mathbf{x}\right))-\mathbf{t}\right)\right) \right) \\
& = \lambda(g)^{\mathrm{SO}(2)} \left( \sum_{{\mathbf{y}} \in \mathbb{Z}^2} f(\mathbf{y}+\mathbf{x}) \ k \left(\mathbf{R}^{-1}(\theta) \left(\mathbf{y}-\mathbf{t}\right)\right) \right) \\
& = \sum_{{\mathbf{y}} \in \mathbb{Z}^2} f \left(\mathbf{R}^{-1}(\theta) \left(\mathbf{y}+\mathbf{x}\right)\right) \ k \left(\mathbf{R}^{-1}(\theta) \left(\mathbf{y}-\mathbf{t}\right)\right) 
\end{aligned}
$$

For the right-hand side, we have:

$$
\begin{aligned}
(\lambda(g)^{\mathrm{SO}(2)} f) \star (\lambda(g)^{\mathrm{SE}(2)} k) 
& = \sum_{{\mathbf{y}} \in \mathbb{Z}^2} f(\mathbf{R}^{-1} (\theta) \ \mathbf{y}) \ k \left(\mathbf{R}^{-1}(\theta)\left(\left(\mathbf{y}-\mathbf{x}\right)-\mathbf{t}\right)\right) \\
& = \sum_{{\mathbf{y}} \in \mathbb{Z}^2} f \left(\mathbf{R}^{-1}(\theta) \left(\mathbf{y}+\mathbf{x}\right)\right) k \left(\mathbf{R}^{-1}(\theta) \left(\mathbf{y}-\mathbf{t}\right)\right) 
\end{aligned}
$$

Comparing the two expressions, we can see that they are equivalent. This confirms that the lifting cross-correlation operation is a $G$-map with respect to the roto-translation group $\mathrm{SE}(2)$. The order of applying the lifting cross-correlation and the rotation does not affect the outcome, confirming the roto-translation $G$-equivariance property.



## Subsequent layers

Now, the question arises as to what type of convolution operator should be employed in the subsequent layers of the network, given the lifted feature maps. We continue to use the same template:

$$
(k \ast f)(\mathbf{x}, \theta) = \left(\lambda_g \ k, f\right) = \left(\lambda_{\mathbf{x}} \ \lambda_{\theta} \ k, f\right) \qquad \text{(1)}
$$

Here, $`{\lambda_g: S E(2) \rightarrow \mathbb{L}_2(S E(2))}`$, $`\lambda_{\mathbf{x}}: {\mathbb{R}^2 \rightarrow \mathbb{L}_2(S E(2))}`$, and $`\lambda_\theta: {SO(2) \rightarrow \mathbb{L}_2(S E(2))}`$.

We need to define how the roto-translation group action representation $\lambda_g$ transforms three-dimensional feature maps, which include both position and rotation components. Therefore, we compute the inner product for all possible translations and rotations $g=(\mathbf{x},\theta)$, resulting in a scalar value.

Once again, the formulation in *Equation 1* is split due to the semi-direct product group structure. We can express both the rotation and translation actions on $k$ more explicitly as $`k(\mathbf{R}_\theta^{-1}(\mathbf{x}^{\prime}-\mathbf{x}), \mathbf{R}_{\theta^{\prime}-\theta})`$. This means that we first apply the rotation to the planar/spatial part and then apply the rotation to the angular part (following the definition of the group product and the group acting on the two-dimensional plane), followed by the shift using $(x'-x)$.

The kernel $k_b$ now becomes three-dimensional, assigning weights to relative orientations. It is important to note that the rotations in the kernel account for both planar rotation and periodic shifts. A high response in the output feature map occurs when all parts of the input feature map $f_c$ align with the transformed kernel $\lambda^b_\mathbf{x} \lambda^b_\theta k_b$. In other words, complete matching between the three-dimensional pattern in the kernel and the input feature map $f_c$ results in a high response.



## Summary

In summary, group convolution is essentially template-matching with a kernel transformed by a group action, whereby we compute an inner product between the transformed kernel and the input data across all possible group transformations.
Specifically, a kernel \( k \) undergoes a transformation via a group action, \( \lambda(g) \), where \( g \) belongs to the group \( G \). The convolution operation is then realised as the inner product between this transformed kernel and an input signal function \( f \) over all group transformations, 
\( (k \ast f)(g) = \left(\lambda(g) k, f\right) \), 
where the outcome is a collection of feature maps in a higher-dimensional space, each representing a function on the group \( G \). These feature maps subsequently serve as the foundation for ensuing template-matching procedures in subsequent network layers.

The introduction of these elevated-dimensional feature maps is pivotal in discerning intricate patterns within the input data, especially when considering their relative spatial orientations or poses. 

Within the architecture of group convolutional neural networks (G-CNNs), $G$-equivariant layers play a crucial role. They facilitate weight sharing across the network and ensure the preservation of specific invariance properties intrinsic to the data. While pooling layers, which inherently bolster such invariances, are a common subsequent step after $G$-equivariant layers.

For a more comprehensive understanding of group convolutional neural networks and their practical applications, consult \autocite{cohen2016-2} and \autocite{lafarge2021}, respectively.

