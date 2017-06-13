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
- **Significance**: It's the first paper which propose end-to-end optical flow estimation with fully convolutional networks. Compared with traditional patch-based algorithm, flownet is much faster when using GPU, but the performance is worse.

#### FlowNet 2.0: Evolution of Optical Flow Estimation with Deep Networks [[Paper]](https://arxiv.org/abs/1612.01925)[[Code]](https://github.com/lmb-freiburg/flownet2)
- **Type**: End2End Learning
- **Gist**:
     - Introduce a data schedule : pretrain on FlyingChair dataset(1.2M iteration) and finetune on Flyingthing3D dataset(0.5M iteration).
     - Propose warping layer which warp second frame according to optical flow. Warping layer help to model large displacement which correlation layer cannot handle.
     - Propose Flownet2 which stacked by multiple flownet, this stacked architecture includes warping of the second image with intermediate optical flow. Although flownet2 has more parameters, it still show strong capacity of generalization.
- **Significance**: For now, flownet2 rank 6th in KITTI 2015 optical flow benchmark and outperform most traditional patch-based optical flow algorithms.

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





