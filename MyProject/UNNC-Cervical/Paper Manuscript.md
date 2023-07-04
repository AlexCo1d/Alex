{Intro}- method() - experiment(data setup, train) - results- conclusion
# Intro
# Material & Method

## Data(图像数据的获取与预处理)

In this study, we collected the data by the ultrasound system {}.
The provided origin datasets of CSD consist of 1111 US images and 16 US videos, annotation operation was conducted by a physician 

To build an effective Cesarean Scar Defect (CSD) screening system, we utilized three medical ultrasound image datasets to train our proposed segmentation algorithm. The first one is a private US dataset, hereafter referred to as the CSD dataset, provided by the affiliated hospital of Shanghai JiaoTong University { #hospital }. CSD dataset consists of 1111 original ultrasound images annotated by physicians, as well as 16 annotated ultrasound videos without spacing information. Since there was a substantial amount of residual digital information from the ultrasound equipment around all images and video frames, I performed a crop operation based on a semi-automatic algorithm on both the images and videos. Furthermore, to eliminate redundant frames in the video data for training, I sampled every 10th frame. Eventually, I obtained 1309 images for the final Cervical dataset. This dataset includes 501 positive samples and 808 negative samples. For this study, we selected a balanced subset of 802 samples for training and a balanced subset of 200 samples for testing. Given the inconsistency in image size, a standardized size of 512×512 was chosen as it is relatively close to the actual size of most images.
## Proposed CSD Segmentation Network 

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

## Comparison

# Results and Discussion

# Conclusion








