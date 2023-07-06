![[architecture of manu.png]]
# Intro

# Material & Method

## Dataset 

### Data acquisition
- To build an effective Cesarean Scar Defect (CSD) screening system, we utilized three medical ultrasound image datasets to train our proposed segmentation algorithm. The first one is a private US dataset, hereafter referred to as the CSD dataset, provided by the affiliated hospital of Shanghai JiaoTong University #med . CSD dataset consists of 1111 original ultrasound images annotated by physicians #med , as well as 16 annotated ultrasound videos without spacing information.
- The other two datasets are thyroid ultrasound dataset ( hereafter  called DDTI dataset)and breast cancer dataset (hereafter called BUSI dataset). Both of these datasets are open access and extensively utilized in various research studies. We employed these datasets to validate the performance of our proposed algorithm. The DDTI dataset utilized in this study comprises 637 images, each with size of  $256 \times 256$. Similarly, the BUSI dataset contains 647 images, each with size of $512 \times 512$.

### Data preprocessing
- Because CSD dataset comes directly from ultrasound machine, we did some preprocessing work before training, in order to improve data's quality. Firstly we processed the US videos by extracting one frame every 10 frames, overcoming the overall redundancy of the data by eliminating the similarity between adjacent frames. After this process, we obtained 271 more US images. Since there was a substantial amount of residual digital information from the ultrasound equipment around all images and video frames, we then used a semi-automatic cropping algorithm, preprocessing both the images and videos into cropped shape that focus on the region of interest (ROI). #fig shows how we processed the video and cropped the CSD ultrasound images. Eventually, after removed some specific ultrasound images different from the other, we obtained 1309 images that form the CSD dataset. This dataset includes 501 positive samples and 808 negative samples. For this study, we selected a balanced subset of 802 samples for training and a balanced subset of 200 samples for testing. The size of the acquired images is inconsistent, so a standardized size of 512×512 was chosen as it is relatively close to the actual size of most images.

## Proposed CSD Segmentation Network 

### Overall Network
- Our proposed network, termed Med-FAUNet (Medical Fully Attention U-Net), primarily embodies an encoder-decoder structure, as illustrated in #fig . The architecture of the network is divided into four distinct stages, with the encoder encompassing the initial three stages and the decoder comprising the final stage. The initial stage, termed the Downsampling Stage, employs a bottleneck structure formulated from a combination of ResNetV2 and the Convolutional Block Attention Module (CBAM) #cite . The purpose of this stage is to efficiently extract and condense salient features from the raw input images. The second stage, known as the Self-Attention Stage, is constructed around the core of the Vision Transformer (ViT). Fully utilized the self-attention mechanism, this stage aims to identify and highlight the crucial interdependencies within the feature map, which is an integral part of the ViT. The third stage, designated as the Multi-Scale Fusion Stage, incorporates a Feature Reshape module along with an ASPP_CBAM module. The primary responsibility of this stage is the integration and fusion of features at various scales, promoting the preservation and incorporation of intricate context details into the subsequent processing stages. The final stage, called the Upsampling Stage, is the sole component of the network's decoder part. It is composed of five separate upsampling blocks, each of which is a hybrid of upsampling and CBAM modules. The aim of this stage is to upscale and refine the processed feature map to match the original input resolution, while using the attention module to extract significant information. Besides, in line with the U-Net, there are several skip-connections embedded within our proposed network, facilitating the bridging of encoder and decoder components. These connections allow the decoder to leverage the features from the encoder, promoting the reconstruction of the fine details in the final output.
- As the input, the ultrasound image is reshaped into a three-channel array. During the Downsampling Stage, the image data is transformed into feature map consisting of C channels, where C equals 64. Subsequent to this, in the Self-Attention Stage, the features go through the transformer module, embedded into a space of $D \times Hidden\_Size$ dimensions. Upon transitioning through the Multi-Scale Fusion Stage, the features are reshaped, then coupled with application of the Atrous Spatial Pyramid Pooling (ASPP_CBAM) module, which reinstates the features to an array of $1024\times\frac{H} {16}\times\frac{W}{16}$ dimensions. In the final stage of processing, the image features undergoes four layers of upsampling-CBAM mixed block as well as a final segmentation head, which converts them back to a segmentation mask that is readily interpretable.

### Downsampling Stage
- The Downsampling Stage comprises 4 sets of convolutional blocks, extracting image features using a combination of attention mechanism and ResNetV2 modules. The first conv block helps to transform raw image into feature map, while the last 3 sets of conv blocks expand the number of channel and decrease the size of the feature map. As shown in #fig , the Downsampling Stage is a multilayer convolutional subnetwork, which stacks the basic conv block for 3, 4, and 9 times respectively.
- Inspired by the work of #cite , we extensively utilize the Convolutional Block Attention Module (CBAM) in our network, especially  in the Downsampling Stage. CBAM separates channel and spatial attention into two standalone submodules. The Channel Attention Module first processes the input feature map through Global Max Pooling (GMP) and Global Average Pooling (GAP), then applies Multiple Layer Projection (MLP) to these pooled maps. The final channel attention feature map is generated via a Sigmoid activation function after an element-wise addition operation on the transformed feature maps. On the other hand, the Spatial Attention Module uses the feature map produced by the Channel Attention Module as its input. The input feature map first undergoes channel-wise GMP and GAP. The resulting pooled feature maps are concatenated along the channel dimension, then dimensionally reduced via a convolution operation, producing a single-channel feature map. A Sigmoid activation function is applied to generate the spatial attention feature map, which is then element-wise multiplied with the input feature map to generate the final feature map. This procedure succinctly illustrates the operation of the Spatial Attention Module and the Channel Attention Module. #need_cut
- In Downsampling Stage, to fully use attention mechanism's ability to grab global information, we merges CBAM into basic ResNetV2 block. In specific, we add the CBAM after the ReLU activation function in the second convolutional unit of ResNetV2. Since the dimension of the second convolution is a quarter of the output dimension, compared to adding an attention module at the end of the residual module, our approach reduces the computational cost of adding the CBAM by a quarter. This process could be depicted by the following formula #formula .

### Self-Attention Stage
- The Self-Attention Stage is factually comprised of the backbone of Vision Transformer (ViT), which is shown in #fig . The ViT module works through the following steps:
	1. Image Partitioning: Initially, the input image is partitioned into a series of fixed-size patches (e.g., 16x16).
	2. Embedding: Each patch is linearly transformed via a fully connected layer into an embedding vector. In addition, a position embedding is included to maintain spatial information. 
	3. Transformer Encoder: The embedding vectors are then fed into a standard Transformer block, during which Transformer learns the relationships among patches through the self-attention mechanism.
- ViT relies on its multi-head self-attention module that enable it to grab global contextual information. So we name this subnetwork Self-Attention Stage. However, ViT requires a significant amount of data and computational resources for training to effectively learn useful visual features. Therefore, to train a ViT backbone we usually adopt a strategy of pre-training followed by fine-tuning, where it is first pre-trained on ImageNet and then fine-tuned on our target dataset.

### Multi-Scale Fusion Stage 
- Multi-Scale Fusion Stage is substantially an Atrous Spatial Pyramid Pooling (ASPP)  #cite  plus CBAM, which we call it ASPP_CBAM module, aiming at apply attention mechanism to Multi-Scale convolutional network. ASPP was firstly been proposed in DeepLab-related network,  representing a spatial pyramid structure with dilated convolution. Given a certain dilation rate, ASPP could expand the receptive field without utilizing pooling or downsampling operations, and such process would fulfill the goal of fusing multi-scale features. #need_cut
- Our proposed ASPP_CBAM module improves upon the traditional ASPP by incorporating an attention operation through a CBAM module after the concatenation process, followed by a 1×1 convolution layer to reduce the number of channels. This way, the features at each scale of the spatial pyramid receive attention, enhancing the treatment of these features. The features will initially reshaped to a $1024\times\frac{H} {16}\times\frac{W}{16}$ size and then fed into the ASPP_CBAM module, and this module does not change the dimension when outputs. #need_cut

### Upsampling Stage
- The Upsampling Stage  consists of 4 decoder block and a segmentation head, incrementally restores the feature map from $1024\times\frac{H} {16}\times\frac{W}{16}$ to an intelligible segmentation mask with size of $Class \times H\times W$. We design the basic upsample module that contains a upsample operation and a CBAM. Besides, before upsample, the decoder block would receive the feature information via skip-connection. After 4 decoder blocks of different dimensions, the feature map finally reshape to normal and interpretable shape through the segmentation head.

## 跳跃连接适应性机制

- Given that small-scale medical image datasets's relatively less information, an increased number of skip-connections may elevate the computational load during the upsampling stage. This could potentially prevent the model from converging normally, thereby affecting its segmentation performance. As such, we propose that an idea of adaptive skip-connections, and employed for different datasets. Particularly, we suggest using 4 skip-connections for images of size 512×512 in the dataset like CSD and BUSI, and 3 skip-connections for images of size 256×256 in the dataset like DDTI.
- To implement the function of adaptive skip-connections, we choose different network parameter for the Upsampling Stage. For the subnetwork with 3 skip-connections, its decoder blocks have (256, 128, 64, 16) output channels respectively, while the one with 4 skip-connections' decoder blocks have (512,256, 64,16) output channels. The channel's adaptive changes are illustrated in #fig . Such design ensures that the scale of parameters is adaptively suitable for dataset, improving the model's segmentation performance. 
~~~python
if config_vit.n_skip == 3:  
    config_vit.decoder_channels=(256, 128, 64, 16)  
    config_vit.skip_channels = [512, 256, 64, 0]  
elif config_vit.n_skip == 4:  
    config_vit.skip_channels = [1024, 512, 256, 64]  
    config_vit.decoder_channels=(512,256, 64,16)
~~~

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