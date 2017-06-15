# Notes of Optical Flow and Stereo Matching

Paper reading notes and resource in the field of **Optical flow** and **Stereo Matching**

## Contributing
Please feel free to [pull requests](https://github.com/dsqx71/Note-flow-stereo/pulls)

## Table of Contents

- [Paper Reading Notes](#paper-reading-notes)
- [Dataset](#dataset)
- Quantitative comparisons

## Paper Reading Notes

#### FlowNet: Learning Optical Flow with Convolutional Networks [[Paper]](https://arxiv.org/abs/1504.06852)[[Code]](https://lmb.informatik.uni-freiburg.de/resources/binaries/)
- **Type**: End2End Learning
- **Gist**:
     - This paper introduce a layer called Correlation layer which can perform multiplicative patch comparsions between two feature maps and return a new feature map representing matching cost, this layer make it possible to incorporate explicit patch comparsion into neural network.
     - They also propose FlownetC and FlownetS which have VGG-like structure to model optical flow end-to-end.
- **Significance**: 
	- It's the first paper which propose end-to-end optical flow estimation with fully convolutional networks. Compared with traditional patch-based algorithm, flownet is much faster when using GPU, but the performance is worse.

#### FlowNet 2.0: Evolution of Optical Flow Estimation with Deep Networks [[Paper]](https://arxiv.org/abs/1612.01925)[[Code]](https://github.com/lmb-freiburg/flownet2)
- **Type**: End2End Learning
- **Gist**:
     - Introduce a data schedule : pretrain on FlyingChair dataset(1.2M iteration) and finetune on Flyingthing3D dataset(0.5M iteration).
     - Propose warping layer which warp second frame according to optical flow. Warping layer help to model large displacement which correlation layer cannot handle.
     - Propose Flownet2 which stacked by multiple flownet, this stacked architecture includes warping of the second image with intermediate optical flow. Although flownet2 has more parameters, it still show strong capacity of generalization.
- **Significance**: 
	- For now, flownet2 ranks 6th in KITTI 2015 optical flow benchmark and outperform most traditional patch-based optical flow algorithms.

#### Improved Stereo Matching with Constant Highway Networks and Reﬂective Conﬁdence Learning[[Paper]](https://arxiv.org/abs/1701.00165)[[Code]](https://github.com/amitshaked/resmatch)
- **Type**: Pipeline
- **Gist**:
	- Incorporating constant highway skip connection into matching network.
	- Employ a fully convolutional network to postprocess the matching cost, which take place of conventional 'winner takes all' stragety and cause the greatest improvement of this work.
	- Propose reflective loss for training model to estimate confidence scores of the output. The loss is quite simple, if the prediciton is correct, i.e differs from the ground truth by less than one pixel, the sample is considered positive, otherwise negative.
	- The authors make an observation that batch normalization has a detrimental effect on matching network. We need more discussion about the building block of matching network.
- **Significance**:
	- It shows that ResNet is ineffective for matching. That is quite unexpected.

#### End-to-End Learning of Geometry and Context for Deep Stereo Regression [[Paper]](https://scholar.google.de/scholar?q=End-to-End%20Learning%20of%20Geometry%20and%20Context%20for%20Deep%20Stereo%20Regression)
- **Type**: End2End learning
- **Gist**:
	- Instead of using distance metric to compute cost volume, this paper introduce a network architecture where firstly employs convolutional network to extract deep unary representation of stereo image pair, and then concat each unary feature with their corresponding unary feature from the opposite image across each disparity level, and packing these into a 4D tensor -- [height * width * (max displacement +1) * feature size]. Compared with distance metric like dot product which restricts the network to only learning relative representations between features, this method does not collapse feature dimension and has capacity of learing absolute feature representations.
	- Employ 3D convolutions to learn to regularize the cost volume
	- Propose soft argmin, this operation takes the sum of each possible disparity, weighted by the probability that  estimated by the model.
- **Significance**:
	- The new method of computing cost volume overcome the limitation of distance metric.

#### Detect, Replace, Reﬁne: Deep Structured Prediction For Pixel Wise Labeling [[Paper]](https://arxiv.org/pdf/1612.04770.pdf) [[Code]](https://github.com/gidariss/DRR_struct_pred)
- **Type**: Post processing
- **Gist**:
	- Employ a fully convolutional network to post process the initial estimation of traditional patch matching approaches.
	- Motivation: 1. Deep convolutional networks alone do not capture fine-grained structures, due to multiple consecutive down-sampling operations, but they can employ context 2. Patch matching approaches do not take into consideration the global information, but they put much attention on capturing details. This work overcome these limiations thourgh combining the two kinds of methods.

- **Significance**:
	- Prompts a guess that maybe End2End learning is not the optimal solution of stereo matching task.

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

#### Comparsions of available dataset
- Table 1 of  [A Large Dataset to Train Convolutional Networks for Disparity, Optical Flow, and Scene Flow Estimation](https://lmb.informatik.uni-freiburg.de/Publications/2016/MIFDB16/)
- Figure 3 of  [Supplementary Material for "FlowNet 2.0: Evolution of Optical Flow Estimation with Deep Networks"](https://lmb.informatik.uni-freiburg.de/Publications/2017/IMKDB17/supplementary-FlowNet_2_0__CVPR_supplemental.pdf)





