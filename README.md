# G-Morphic Convolution

Group-theoretic studies of $G$-morphism in convolution.


## Translation G-Morphic Convolution

A study of convolution operations within the context of the additive group $\mathbb{R}^2$.

**Key Highlights:**
1. **Cross-correlation as Integral Transform**: Illustrates cross-correlation in $\mathbb{R}^2$ as an integral transform, pinpointing the kernel's alignment with an input signal.
2. **Discretization**: Offers a computational lens to view the discrete form of cross-correlation, making it amenable to practical applications.
3. **Translation $G$-map**: Stresses the consistent nature of convolution across all $\mathbf{y} \in \mathbb{Z}^2$, underscoring the notion that translating either before or after the act of cross-correlation remains equivalent.
4. **Proof of $G$-map Property**: Utilizes the left regular group representation to validate the $G$-map property, assuring that pre-correlation translation produces the same result as post-correlation translation.
5. **Practical Implications**: Highlights the broader relevance and implications of the presented concepts, suggesting potential applications in various domains.


## Roto-Translation G-Morphic Convolution

A study of $G$-morphic convolutions, which are convolutions that take into account both translations and rotations under the special Euclidean group $\text{SE}(2)$.

Key Highlights:
1. **Nonstandard Convolution**: Instead of simply translating the kernel across a function, the kernel is acted upon by the group representation $\lambda(g)$.
2. **Roto-translation Convolutions**: Explores the convolution in the context of the special Euclidean group $\mathrm{SE}(2)$, which comprises translations in $\mathbb{R}^2$ and rotations in the special orthogonal group $\mathrm{SO}(2)$.
3. **Lifting Cross-Correlation**: Incorporates both translation and rotation transformations to capture spatial relationships in data more comprehensively.
4. **Proof of $G$-map Requirement**: Validates that the convolution operation is equivariant to the roto-translation group $\mathrm{SE}(2)$, ensuring that the order of applying cross-correlation and rotation doesn't change the outcome.
5. **Subsequent Network Layers**: Discusses how the proposed convolution operator can be extended to deeper network layers.

For detailed mathematical formulations, derivations, and diagrams, refer to the main content of the repository.



