# Intro

# Material & Method

## Data(图像数据的获取与预处理)

### Data acquisition
To build an effective Cesarean Scar Defect (CSD) screening system, we utilized three medical ultrasound image datasets to train our proposed segmentation algorithm. The first one is a private US dataset, hereafter referred to as the CSD dataset, provided by the affiliated hospital of Shanghai JiaoTong University #hospital . CSD dataset consists of 1111 original ultrasound images annotated by physicians #hospital , as well as 16 annotated ultrasound videos without spacing information.
The other two datasets are thyroid ultrasound dataset ( hereafter  called DDTI dataset)and breast cancer dataset (hereafter called BUSI dataset). Both of these datasets are open access and extensively utilized in various research studies. We employed these datasets to validate the performance of our proposed algorithm. The DDTI dataset utilized in this study comprises 637 images, each with size of  $256 \times 256$. Similarly, the BUSI dataset contains 647 images, each with size of $512 \times 512$.

### Data preprocessing
Because CSD dataset comes directly from ultrasound machine, we did some preprocessing work before training, in order to improve data's quality. Firstly we processed the US videos by extracting one frame every 10 frames, overcoming the overall redundancy of the data by eliminating the similarity between adjacent frames. After this process, we obtained 271 more US images. Since there was a substantial amount of residual digital information from the ultrasound equipment around all images and video frames, we then used a semi-automatic cropping algorithm, preprocessing both the images and videos into cropped shape that focus on the region of interest (ROI). #fig shows how we processed the video and cropped the CSD ultrasound images. Eventually, after removed some specific ultrasound images different from the other, we obtained 1309 images that form the CSD dataset. This dataset includes 501 positive samples and 808 negative samples. For this study, we selected a balanced subset of 802 samples for training and a balanced subset of 200 samples for testing. The size of the acquired images is inconsistent, so a standardized size of 512×512 was chosen as it is relatively close to the actual size of most images.

## Proposed CSD Segmentation Network 

 Our proposed network is called Med-FAUNet (Medical Fully Attention U-Net), which is generally an encoder-decoder network architecture, as depicted in #fig . This network has 4 stage, while the encoder part of the network comprises three stages and the decoder part has one stage. Specifically, the first stage is called Downsampling Stage, where the bottleneck structure formed by a combination of ResNetV2 and the Convolutional Block Attention Module (CBAM), extracting feature from raw images. The second stage is called Self-Attention Stage, composed of the backbone of the Vision Transformer (ViT). The third stage, called Multi-Scale Fusion Stage, consists of a feature reshape module and an ASPP_CBAM module, which performs the role of multi-scale feature fusion. The decoder of the network, which serves as the Upsampling Stage, is made up of five upsampling blocks, each of which is a blend of upsampling  and CBAM modules. Similar to U-Net, there are a few skip-connections that bind the network's the encoder and decoder part.

Before being input to the network, ultrasound image data is converted into a 3-channel array. Following the downsampling module in Stage 1, it is transformed into a feature array with C channels (C=64). After Stage 2, the transformer module encodes it into features of Hidden_Size dimensions. After going through the feature reshaping and the ASPP_CBAM module in Stage 3, it is restored to an array of size 1024××. Finally, after four layers of upsampling and the Segmentation Head, it is transformed back into an understandable segmentation mask.

### 下采样

### Transformer

### ASPP-CBAM

### 上采样

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








