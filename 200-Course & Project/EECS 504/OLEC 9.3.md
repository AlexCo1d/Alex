# ways of representing image:
(10,10) binary image-> $2^{100}$ possibilities.
- Graph 

- Point
$X= (0,0,1,...,..., 1,0,) _{100}$

- Function
$I(x,y)=0/1$ ^488d9a

# Perfect image 

$$ I:\mathbb{R}^{2} \rightarrow \mathbb{R}^d$$
Where $I(\cdot) \geq 0, \ d\geq 1$

# Image as functions

## Physical & continuous Images
Like [[#Perfect image]]
### Implementation
Lambertian model
## Physical & Discrete Images
Like digital image (e.g. CCD), which is a sampled and quantized perfect image 
$$
I:\mathbb{N}^{2}\rightarrow \mathbb{N}
$$
 $R^2 \rightarrow N^2$ is sampling, and from $R \rightarrow N$ is quantization
### Implementation - Bayer pattern model
Bayer pattern model, demosaiking each color channel to form an image
green more than red & blue (because human eyes are more sensitive)
## Model & Discrete
$$
I:\mathbb{Z}^{2}\rightarrow \mathbb{Z}
$$
Extract feature image from $I:\{RGB\}$ to $\nabla I$ , then we have
$$
I:\mathbb{Z}^{2}\rightarrow \mathbb{Z}^k
$$
### Implementation - Potts model
Difference between neighbor pixel.
***Energy function*** that evaluate the image's stability of how it is at peace.
$$
E(I)=\beta\sum\limits_{s=1}^{n-1}\sum\limits_{t=1}^{n}\left(\mathbb{I}[I(s,t)\neq I(s+1),t]\right)+\beta\sum\limits_{s=1}^{n-1}\sum\limits_{t=1}^{n}\left(\mathbb{I}[I(s,t)\neq I(s,t+1)]\right)
$$

Where $\mathbb{I}(a)=\begin{cases}1 & \text{if a  is true} \\ 0 & \text{if a  is false}\end{cases}$
The plot of E (I) is like a truncate potential function.

Noisy Images or Cleaning Dirty Images:
$I=J+Noise$, J is the actual image we want
we need to minimize the Energy function
$$
E(J|I)=\alpha Cost(I,J)+(1-\alpha)S(J)
$$
$$
arg \ \mathop{min}\limits_{J} \ E(I|J)
$$
Cost is the data term that $\sum\limits_{s=1}^n\sum\limits_{t=1}^n(I(s,t)-J(s,t))^2$ 
And S is a regularizer term, $S(J)=E_p(J)$.

## Model & Continuous
$$
I: \ \mathbb{R}^2 \rightarrow \mathbb{R}
$$
Used when smooth image boundaries are needed
E.g. medical image segmentation, or rotoscoping in holywood.

### Hybrid discrete & continuous 

Key issue for continuous model is ***interpolation*** 
E.g. bilinear interpolation
- weighs along row first, and then columns
- Convex combinations of sampled value. 
