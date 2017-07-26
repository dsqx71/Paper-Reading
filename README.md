# Notes of Optical Flow and Stereo Matching



Paper reading notes and resources in the field of computer vision algorithms for **Optical flow** and **Stereo Matching**



## Contributing

Please feel free to [pull requests](https://github.com/dsqx71/Note-flow-stereo/pulls)



## Table of Contents



- [Paper Reading Notes](#paper-reading-notes)

- [Dataset](#dataset)



## Paper Reading Notes



#### FlowNet: Learning Optical Flow with Convolutional Networks (ICCV 2015)[[Paper]](https://arxiv.org/abs/1504.06852)[[Code]](https://lmb.informatik.uni-freiburg.de/resources/binaries/)

- **Type**: End2End Learning

- **Gist**:

     - This paper introduces a layer called Correlation layer which perform multiplicative patch comparisons between two input feature maps and return a new feature map representing the matching cost, this layer makes it possible to incorporate explicit patch comparisons into a neural network.

     - They also propose FlownetC and FlownetS which have VGG-like structures to model optical flow end-to-end.

- **Significance**:

    - It's the first paper which proposes end-to-end optical flow estimation with fully convolutional networks. Compared with traditional patch-based algorithms, FlowNet is much faster when using GPU.

- **Weakness**:

    - Flownet needs a longer training process than variational methods do.

    - Performances are not great enough.



#### FlowNet 2.0: Evolution of Optical Flow Estimation with Deep Networks (CVPR 2017)[[Paper]](https://arxiv.org/abs/1612.01925)[[Code]](https://github.com/lmb-freiburg/flownet2)

- **Type**: End2End Learning

- **Gist**:

     - Introduces a data schedule : pretrain models on FlyingChair dataset(1.2M iteration) and then finetune them on Flyingthing3D dataset(0.5M iteration).

     - Invents warping layer which warps the second frame according to optical flow. Warping layer help to model large displacement which correlation layer cannot handle.

     - Proposes Flownet2 which stacked by multiple Flownet, this stacked architecture includes warping of the second image with an intermediate optical flow. Although flownet2 has more parameters, it still shows strong capacity of generalization.

- **Significance**:

    - It's the first to employ the cascade architecture in End2End optical flow estimation.



#### Improved Stereo Matching with Constant Highway Networks and Reﬂective Conﬁdence Learning (CVPR 2017)[[Paper]](https://arxiv.org/abs/1701.00165)[[Code]](https://github.com/amitshaked/resmatch)

- **Type**: Pipeline

- **Gist**:

    - Incorporating constant highway skip connection into matching network.

    - Employ a fully convolutional network to post-process the matching cost, which takes place of conventional 'winner takes all' strategy and cause the greatest improvement of this work.

    - Propose reflective loss for training model to estimate confidence scores of the output. The loss is quite simple. If the prediction is correct, i.e differs from the ground truth by less than one pixel, the sample is considered positive, otherwise negative.

    - The authors make an observation that batch normalization has a detrimental effect on matching networks.

- **Significance**:

    - The experiment shows that vanilla residual blocck is ineffective for stereo matching, which is quite unexpected.

- **Weakness**:

    - The authors don't give an explanation why vanilla residual block cannot work.



#### End-to-End Learning of Geometry and Context for Deep Stereo Regression (CVPR 2017)[[Paper]](https://scholar.google.de/scholar?q=End-to-End%20Learning%20of%20Geometry%20and%20Context%20for%20Deep%20Stereo%20Regression)

- **Type**: End2End learning

- **Gist**:

    - Instead of using distance metric to compute cost volume, this paper introduce a network architecture where firstly employs convolutional network to extract deep unary representation of stereo image pair, and then concat each unary feature with their corresponding unary feature from the opposite image across each disparity level, and packing these into a 4D tensor -- [height * width * (max displacement +1) * feature size]. Compared with distance metric like dot product which restricts the network to only learning relative representations between features, this method does not collapse feature dimension and has the capacity of learning absolute feature representations.

    - Employ 3D convolutions to learn to regularize the cost volume

    - Propose **soft argmin**, this operation takes the sum of each possible disparity, weighted by the probability that estimated by the model.

- **Significance**:

    - The new method of computing cost volume overcomes the limitation of distance metric.



#### Detect, Replace, Reﬁne: Deep Structured Prediction For Pixel Wise Labeling (CVPR 2017)[[Paper]](https://arxiv.org/pdf/1612.04770.pdf) [[Code]](https://github.com/gidariss/DRR_struct_pred)

- **Type**: Post processing

- **Gist**:

    - Employ a fully convolutional network to post process the initial estimation of traditional patch matching approaches.

    - Motivation: 1. Deep convolutional networks alone do not capture fine-grained structures, due to multiple consecutive down-sampling operations, but they can learn to employ context 2. Patch matching approaches do not take into consideration the global information, but they put much attention on capturing details. This work overcomes these limitations through combining the two kinds of methods.



- **Significance**:

    - Propose a way to combine traditional algorithm and neural network.



#### Optical Flow Estimation using a Spatial Pyramid Network (CVPR 2017)[[Paper]](https://arxiv.org/pdf/1611.00850.pdf)[[Code]](https://github.com/anuragranj/spynet)

- **Type**: End2End Learning

- **Gist**:

    - Point out that a convolutional layer can not learn a meaningful filter to recognize large motions if its window in one image does not overlap with related image pixels at the next time instant.

    - Adopt a traditional coarse-to-fine approach using multi-resolution pyramids to estimate optical flow, and employ warp operation between pyramid levels to help the neural network to learn large motions.

- **Significance**:

    * Real-time optical flow estimation.

    * The parameter size of SpyNet is 96% smaller than FlowNet, which makes it possible to deploy Spynet on mobile devices.

- **Weakness**:

    * Coarse pyramid level is only able to capture large object with large displacement, yet it cannot estimate fast-moving small objects.



#### Back to Basics: Unsupervised Learning of Optical Flow via Brightness Constancy and Motion Smoothness (ECCV 2016)[[Paper]](https://arxiv.org/pdf/1608.05842.pdf)

- **Type**: Unsupervised Learning

- **Gist**:

    - Propose an unsupervised learning approach where it warps the second frame according to optical flow estimated by a  Convnet and uses photometric to measure the similarity between the first frame and the warped frame so as to generate supervising signals for learning algorithms.

- **Significance**:

    - Invent an elegant method to get supervising signals, which can reduce the reliance of learning algorithms on optical flow dataset.

- **Weakness**:

    - Due to occlusion, the warped frame cannot perfectly match the first frame. Therefore, in many cases, the supervising signals are not very meaningful.



#### S2F: Slow-To-Fast Interpolator Flow (CVPR 2017)[[Paper]](http://vision.ucla.edu/papers/yangS17.pdf)

- **Type**: Post-processing

- **Gist**:

    - The paper gives an explanation why coarse-to-fine approaches cannot predict large motions of small objects -- Coarse pyramid levels don't have enough resolution to capture small objects, meanwhile, the region of interest in a fine-scale pyramid isn't large enough to recognize large displacement.



#### CNN-based Patch Matching for Optical Flow with Thresholded Hinge Embedding Loss(CVPR 2017)[[Paper]](https://arxiv.org/abs/1607.08064)

- **Type**: Patch-matching

- **Gist**:

    - An variant of hinge loss -- add a gap in the L2 distance between matching and non-matching pairs

    - New evaluation method to measure matching robustness.

#### DenseNet for dense flow(ICIP 2017)[[Paper]](https://arxiv.org/abs/1707.06316)

- **Type**: Unsupervised Learning
- **Gist**:
	- Investigate DenseNet to learn optical flow.
	- Make the observation that the performance of deeper models are much worse, probably because optical flow is a low-level vision problem, that doesn't need a substantially deeper network to achieve better performance.
	- Observe that using dense blocks during upsampling is beneficial.
	- DenseNet is less prone to overfitting, probably because of the model compactness.


- **Weakness**：
	- The quantative comparsion is not very meaningful, since most of other models are supervised approaches.
	- They should add an experiment where firstly fine tune DenseNet on KITTI dataset and then use the unsupervising manner.

## Dataset

| Dataset | Source | Optical flow | Disparity | #Training frames | #Testing frames|
|:----:|:----:|:----:| :----:|:----:|:----:|
| **FlyingThings3D** | [Nikolaus Mayer et al CVPR2016](https://lmb.informatik.uni-freiburg.de/Publications/2016/MIFDB16/) | Dense | Dense | 21818 | 4248 |
| **FlyingChair** | [Dosovitskiy et al CVPR2016]() | Dense | - | 22232 | 640 |
| **KITTI 2015**| [Moritz Menze et al CVPR2015](http://cvlibs.net/publications/Menze2015CVPR.pdf)| Sparse | Sparse | 200 | 200|
| **KITTI 2012**| [Andreas Geiger et al CVPR2012](http://www.cvlibs.net/publications/Geiger2012CVPR.pdf)| Sparse| Sparse| 194 | 194 |
| **MPI Sintel** |[Butler et al ECCV2012](http://files.is.tue.mpg.de/black/papers/ButlerECCV2012-corrected.pdf) | Dense | Dense | 1064 | 564 |
| **ChairsSDHom** |[E. Ilg et al CVPR2017](https://lmb.informatik.uni-freiburg.de/Publications/2017/IMKDB17/) | Dense | - | 20966 | 704 |

Note that, official stereo testing set of Sintel hasn't been released so far.


## Benchmark
| Name | Type |
|:----:|:----:|
| [**Sintel**](http://sintel.is.tue.mpg.de/results)| Dense |
| [**KITTI**](http://www.cvlibs.net/datasets/kitti/eval_scene_flow.php?benchmark=stereo) | Sparse |

#### Comparsions of available dataset
- Table 1 of  [A Large Dataset to Train Convolutional Networks for Disparity, Optical Flow, and Scene Flow Estimation](https://lmb.informatik.uni-freiburg.de/Publications/2016/MIFDB16/)
- Figure 3 of  [Supplementary Material for "FlowNet 2.0: Evolution of Optical Flow Estimation with Deep Networks"](https://lmb.informatik.uni-freiburg.de/Publications/2017/IMKDB17/supplementary-FlowNet_2_0__CVPR_supplemental.pdf)


