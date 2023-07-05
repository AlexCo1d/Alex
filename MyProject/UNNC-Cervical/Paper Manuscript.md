# Intro

# Material & Method

## Data(图像数据的获取与预处理)

### Data acquisition
To build an effective Cesarean Scar Defect (CSD) screening system, we utilized three medical ultrasound image datasets to train our proposed segmentation algorithm. The first one is a private US dataset, hereafter referred to as the CSD dataset, provided by the affiliated hospital of Shanghai JiaoTong University #hospital . CSD dataset consists of 1111 original ultrasound images annotated by physicians #hospital , as well as 16 annotated ultrasound videos without spacing information.

The other two datasets are thyroid ultrasound dataset ( hereafter  called DDTI dataset)and breast cancer dataset (hereafter called BUSI dataset). Both of these datasets are open access and extensively utilized in various research studies. We employed these datasets to validate the performance of our proposed algorithm. The DDTI dataset utilized in this study comprises 637 images, each with size of  $256 \times 256$. Similarly, the BUSI dataset contains 647 images, each with size of $512 \times 512$.

### Data preprocessing
Because CSD dataset comes directly from ultrasound machine, we did some preprocessing work before training, in order to improve data's quality. Firstly we processed the US videos by extracting one frame every 10 frames, overcoming the overall redundancy of the data by eliminating the similarity between adjacent frames. After this process, we obtained 271 more US images. Since there was a substantial amount of residual digital information from the ultrasound equipment around all images and video frames, we then used a semi-automatic cropping algorithm, preprocessing both the images and videos into cropped shape that focus on the region of interest (ROI). #fig shows how we processed the video and cropped the CSD ultrasound images. Eventually, after removed some specific ultrasound images different from the other, we obtained 1309 images that form the CSD dataset. This dataset includes 501 positive samples and 808 negative samples. For this study, we selected a balanced subset of 802 samples for training and a balanced subset of 200 samples for testing. The size of the acquired images is inconsistent, so a standardized size of 512×512 was chosen as it is relatively close to the actual size of most images.

## Proposed CSD Segmentation Network 

###overall network
Our proposed network, termed Med-FAUNet (Medical Fully Attention U-Net), primarily embodies an encoder-decoder structure, as illustrated in #fig . The architecture of the network is divided into four distinct stages, with the encoder encompassing the initial three stages and the decoder comprising the final stage. The initial stage, termed the Downsampling Stage, employs a bottleneck structure formulated from a combination of ResNetV2 and the Convolutional Block Attention Module (CBAM) #cite . The purpose of this stage is to efficiently extract and condense salient features from the raw input images. The second stage, known as the Self-Attention Stage, is constructed around the core of the Vision Transformer (ViT). Fully utilized the self-attention mechanism, this stage aims to identify and highlight the crucial interdependencies within the feature map, which is an integral part of the ViT. The third stage, designated as the Multi-Scale Fusion Stage, incorporates a Feature Reshape module along with an ASPP_CBAM module. The primary responsibility of this stage is the integration and fusion of features at various scales, promoting the preservation and incorporation of intricate context details into the subsequent processing stages. The final stage, called the Upsampling Stage, is the sole component of the network's decoder part. It is composed of five separate upsampling blocks, each of which is a hybrid of upsampling and CBAM modules. The aim of this stage is to upscale and refine the processed feature map to match the original input resolution, while using the attention module to extract significant information. Besides, in line with the U-Net, there are several skip-connections embedded within our proposed network, facilitating the bridging of encoder and decoder components. These connections allow the decoder to leverage the features from the encoder, promoting the reconstruction of the fine details in the final output.

As the input, the ultrasound image is reshaped into a three-channel array. During the Downsampling Stage, the image data is transformed into feature map consisting of C channels, where C equals 64. Subsequent to this, in the Self-Attention Stage, the features go through the transformer module, embedded into a space of $D \times Hidden\_Size$ dimensions. Upon transitioning through the Multi-Scale Fusion Stage, the features are reshaped, then coupled with application of the Atrous Spatial Pyramid Pooling (ASPP_CBAM) module, which reinstates the features to an array of $1024\times\frac{H} {16}\times\frac{W}{16}$ dimensions. In the final stage of processing, the image features undergoes four layers of upsampling-CBAM mixed block as well as a final segmentation head, which converts them back to a segmentation mask that is readily interpretable.

### Downsampling Stage
- Inspired by the work of #cite , we extensively utilize the Convolutional Block Attention Module (CBAM) in our network, predominantly in the Downsampling Stage. CBAM separates channel and spatial attention into two standalone submodules. The Channel Attention Module first processes the input feature map through Global Max Pooling (GMP) and Global Average Pooling (GAP), then applies Multiple Layer Projection (MLP) to these pooled maps. The final channel attention feature map is generated via a Sigmoid activation function after an element-wise addition operation on the transformed feature maps. On the other hand, the Spatial Attention Module uses the feature map produced by the Channel Attention Module as its input. The input feature map first undergoes channel-wise GMP and GAP. The resulting pooled feature maps are concatenated along the channel dimension, then dimensionally reduced via a convolution operation, producing a single-channel feature map. A Sigmoid activation function is applied to generate the spatial attention feature map, which is then element-wise multiplied with the input feature map to generate the final feature map. This procedure succinctly illustrates the operation of the Spatial Attention Module and the Channel Attention Module. #need_cut

- Downsampling Stage, to introduce attention mechanism into CNN, merges CBAM into basic ResNetV2 block. In specific, 



### Self-Attention Stage

### Multi-Scale Fusion Stage

### Upsampling Stage

## 跳跃连接适应性机制

## 迁移学习与微调策略

## 后处理

# Experiment 

## environment

## metrics

## Network Training
Data augmentation, epoch, freeze, learning rate...
## Comparison

# Results and Discussion

# Conclusion








