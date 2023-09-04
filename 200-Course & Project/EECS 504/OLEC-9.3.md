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
Like Perfect image
### Implementation
Lambertian model

## Physical & Discrete Images
Like digital image (e.g. CCD), which is a sampled and quantized perfect image 
$$
I:\mathbb{N}^{2}\rightarrow \mathbb{N}
$$
 $R^2 \rightarrow N^2$ is sampling, and from $R \rightarrow N$ is quantization
### Implementation
Bayer pattern model, demosaiking each color channel to form an image
## Model & Discrete
$$
I:\mathbb{Z}^{2}\rightarrow \mathbb{Z}
$$
Extract feature image from $I:\{RGB\}$ to $\nabla I$ , then we have
$$
I:\mathbb{Z}^{2}\rightarrow \mathbb{Z}^k
$$
### Implementation
Potts Model
