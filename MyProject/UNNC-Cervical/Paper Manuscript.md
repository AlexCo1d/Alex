{Intro}- method() - experiment(data setup, train) - results- conclusion
# Intro
# Material & Method

## Data(图像数据的获取与预处理)

### Data acquisition
To build an effective Cesarean Scar Defect (CSD) screening system, we utilized three medical ultrasound image datasets to train our proposed segmentation algorithm. The first one is a private US dataset, hereafter referred to as the CSD dataset, provided by the affiliated hospital of Shanghai JiaoTong University #hospital . 

### Data preprocessing
CSD dataset consists of 1111 original ultrasound images annotated by physicians #hospital , as well as 16 annotated ultrasound videos without spacing information. Firstly we processed the US videos by extracting one frame every 10 frames, overcoming the overall redundancy of the data by eliminating the similarity between adjacent frames. After this process, we obtained 271 more US images. Since there was a substantial amount of residual digital information from the ultrasound equipment around all images and video frames, we then used a semi-automatic cropping algorithm, preprocessing both the images and videos into cropped shape that focus on the region of interest (ROI). #fig shows how we processed the video and cropped the CSD ultrasound images. Eventually, after removed some specific ultrasound images different from the other, we obtained 1309 images that form the CSD dataset. This dataset includes 501 positive samples and 808 negative samples. For this study, we selected a balanced subset of 802 samples for training and a balanced subset of 200 samples for testing. The size of the acquired images is inconsistent, so a standardized size of 512×512 was chosen as it is relatively close to the actual size of most images.
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








