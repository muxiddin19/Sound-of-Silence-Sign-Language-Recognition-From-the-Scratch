# Sound-of-Silence-Sign-Language-Recognition-From-the-Scratch
## The repo is being updated
### This is repo for our paper submitted to ACL2025
![image](https://github.com/user-attachments/assets/d7f9e6bc-138a-4e15-9f65-9ff8e7d995d4)
 ## Abstract
 In this paper, we revolutionize the landscape of sign
 language recognition (SLR) with direction vector-based cutting
edge keypoint data vectorization techniques and a powerful mul
timodal deep learning (DL) approach. R-tree indexing employed
 our innovative vectorization method, simplifying and stream
lining SLR data, dramatically boosting data comprehension,
 storage, and computation efficiency. By leveraging a multistream
 architecture that captures multiple dimensions of sign language,
 we not only push the boundaries of interpretability but also
 deliver enhanced recognition accuracy. We address challenges
 like outliers in keypoint data and complex gestures through
 careful data preprocessing and specialized training strategies,
 improving robustness to edge cases such as occluded hand shapes
 and fast motions. By reducing the dimensionality of keypoint
 data, we can minimize the computational cost while maintaining
 high accuracy, which is crucial for real-time applications where
 latency and computational overhead are critical factors. This
 breakthrough sets a new benchmark for SLR systems, opening
 doors to real-time applications and expanding into previously
 untapped modalities. With the promise of further advancements,
 our work paves the way for the practical and widespread
 adoption of explainable and high-performance SLR technologies.
![image](https://github.com/user-attachments/assets/be2eb6ef-4a01-470d-9dbe-96d7c65b44c2)


## Dependencies
- absl-py==0.9.0
- numpy==1.18.1
- oauthlib==3.1.0
- omegaconf==2.1.1
- opencv-python==4.4.0.46
- pandas==1.0.3
- pillow==8.4.0
- portalocker==1.5.2
- protobuf==3.19.4
- py==1.8.1
- pyarrow==3.0.0
- pydot==1.4.2
- python-dateutil==2.8.1
- scikit-learn==0.22.2.post1
- tensorboard-data-server==0.6.1
- tensorboard-plugin-wit==1.8.0
- tensorflow==2.2.0
- tensorflow-estimator==2.2.0
- tokenizers==0.10.3
- torch==1.9.0
- torch-tb-profiler==0.2.1
- torchtext==0.5.0
- torchvision==0.10.0
- tqdm==4.40.2
- transformers==4.11.3
## Download Datasets
- [Phoenix-2014](https://www-i6.informatik.rwth-aachen.de/~koller/RWTH-PHOENIX/)
- [Phoenix-2014T](https://www-i6.informatik.rwth-aachen.de/~koller/RWTH-PHOENIX-2014-T/)
- [CSL-Daily](http://home.ustc.edu.cn/~zhouh156/dataset/csl-daily/)
- For extracting downloaded videofiles, you may run the given code:
- [Extract videofiles.](https://github.com/muxiddin19/Sound-of-Silence-Sign-Language-Recognition-From-the-Scratch/preprocess/preprocess_video.sh)
## Data Preparation
### Exploited Datasets
- Phoenix-2014: A German sign language dataset with 1081 glosses.
- Phoenix-2014T: An extension of Phoenix-2014, with 1066 glosses and 2887 German text entries.
- CSL-Daily: A large-scale Chinese sign language dataset with 2000 glosses and 2343 text entries.

### Pretrained 
- Models We provide pretrained models [here](https://hkustconnect-my.sharepoint.com/:f:/g/personal/rzuo_connect_ust_hk/EolDU7j15xROncGg8QqLpkABn9mFEfriS0owcyr048nyXg?e=jHdxlg). Download this directory and place it as pretrained_models. Specifically, the required pretrained models include:

- s3ds_actioncls_ckpt: S3D backbone pretrained on Kinetics-400. [Thanks for their implementation!](https://github.com/kylemin/S3D)
- s3ds_glosscls_ckpt: S3D backbone pretrained on Kinetics-400 and WLASL.
- mbart_de / mbart_zh : pretrained language models used to initialize the translation network for German and Chinese, with weights from mbart-cc-25.

### Keypoint Data
![image](https://github.com/user-attachments/assets/8b79934d-dd96-472f-8103-0349f2f6a205)

 Exploite human keypoints for three datasets, [Phoenix-2014](https://hkustconnect-my.sharepoint.com/:u:/g/personal/rzuo_connect_ust_hk/EX4hzndQCiNGlZTlQymJlKgB9l3tBHi2ihKh0b1nrO-4Lg?e=QXUrrP), [Phoenix-2014T](https://hkustconnect-my.sharepoint.com/:u:/g/personal/rzuo_connect_ust_hk/EdCvVpXswSJKlj4FUYUJJ9EBm1cqFBOBMloVRqSTpng7dQ?e=EH6YfR), and [CSL-Daily](https://hkustconnect-my.sharepoint.com/:u:/g/personal/rzuo_connect_ust_hk/Eanp_XYZnmVNiqRlNIQJf6kBkIDst176O2vkPNZDGnmbWw?e=0P8aiq), pre-extracted by HRNet, and can be downloaded and place them under data/phoenix-2014(phoenix-2014t or csl-daily).

### R-Tree indexing
The R-Tree was applied to 2D human keypoints 
to enhance the efficiency and robustness of keypoint data retrieval in SLR.
 For each frame in a video, keypoints representing body parts (e.g., hands, face) are extracted. 
These keypoints are typically in the format (x, y, c), where x and y are the spatial coordinates, and c is the confidence score.
The R-Tree divides and indexes multi-dimensional data into Minimum Bounding Rectangles (MBRs). Each keypoint, defined by its (x, y, c) coordinates, is inserted into the R-Tree with a unique identifier. 
This allows for rapid and efficient proximity searches.



![image](https://github.com/user-attachments/assets/0a5ac44d-1890-436d-8176-96aae69c7e01)

### Doppler Data
The number of input frames and output frames is consistent, 
while it outputs temporal motion features.
![image](https://github.com/user-attachments/assets/21c966de-ed89-450f-ba0d-22c4037ef9d7)



### Vector Data
![image](https://github.com/user-attachments/assets/548586dd-ede9-48f7-baa0-0de65fb5be38)

Left: Direction vector with eight different directions, plus zero (0, 0) vector, the initial point. 
Right: Visualize the vectorization approach with a direction vector using only one keypoint.

![image](https://github.com/user-attachments/assets/5b0ad68f-39a1-47ba-84e3-45fdba1f0b33)

![image](https://github.com/user-attachments/assets/53d76e0b-fb93-48eb-9c9f-81648fe1e4e9)

![image](https://github.com/user-attachments/assets/5b077e95-b33e-4898-a74c-bb5b3e6f13a1)

![image](https://github.com/user-attachments/assets/870c2cc6-19c6-4ebb-be73-a84e2890a979)

### Bidirectional Lateral Interaction for MultiStream Inputs

![image](https://github.com/user-attachments/assets/a9e8fe98-1476-4873-ae98-d9a0ee1927d2)

## Training Process
### Training only single stream video, keypoint, doppler, or vector data)
dataset=phoenix-2014 # phoenix-2014t / csl-daily
python -m torch.distributed.launch --nproc_per_node 8 --use_env training.py --config experiments/configs/video.yaml  #for videos
python -m torch.distributed.launch --nproc_per_node 8 --use_env training.py --config experiments/configs/keypoint.yaml  #for keypoints
python -m torch.distributed.launch --nproc_per_node 8 --use_env training.py --config experiments/configs/doppler.yaml  #for keypoints
python -m torch.distributed.launch --nproc_per_node 8 --use_env training.py --config experiments/configs/vector.yaml  #for keypoints

### Multistream Training

python -m torch.distributed.launch --nproc_per_node 8 --use_env training.py --config experiments/configs/multistream.yaml

## Resume Interrupted training
python -m torch.distributed.launch --nproc_per_node 8 --use_env training.py --config experiments/configs/multistream.yaml --resume

## Testing Process

- The code is being updated

## Real time SLR

For real-time SLR task just run below code:
- python real_time.py

  be sure that your camera is accessible from your terminal.

## Citation
- The related citation will be updated soon.

## Acknowledment

This repo is actively exploited https://github.com/muxiddin19/DDC3N-Doppler-Driven-C3D-Network-for-HAR, https://github.com/FangyunWei/SLRT/tree/main/TwoStreamNetwork, https://github.com/kaistmm/SlowFastSign and other related repos.

Thanks to the original authors for their awesome works!

## Contacts
For any questions, feel free to contact: trinity@inha.ac.kr, muhiddin1979@inha.edu.
