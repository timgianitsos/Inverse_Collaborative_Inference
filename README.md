# Model Inversion Attack against Collaborative Inference

This code implements model inversion attacks against collaborative inference in the following [paper](https://github.com/zechenghe/Inverse_Collaborative_Inference/blob/master/Model%20Inversion%20Attacks%20Against%20Collaborative%20Inference.pdf):

Zecheng He, Tianwei Zhang and Ruby Lee, "Model Inversion Attacks Against Collaborative Inference", 35th Annual Computer Security Applications Conference (ACSAC'19), San Juan, Dec 2019

We provide three attacks, i.e. rMSE (Section 4), blackbox inverse network (Section 5) and query-free attack (Section 6) on CIFAR10 dataset. Attacks against MNIST are similar.

### 1.Dependencies:
#### python 2.7
#### numpy
    pip install numpy
#### pytorch 1.0.0
    pip install torch
#### torchvision version 0.2.1:
    pip install torchvision==0.2.1

<br/>

### 2.Run the code:
#### (1) Train the target CIFAR model to inverse

    python training.py --dataset CIFAR10 --epochs 50

#### (2) Whitebox Regularized Maximum Likelihood Estimation (rMLE, Section 4)

    python inverse_whitebox_CIFAR.py --iters 5000 --learning_rate 1e-2 --layer ReLU22 --lambda_TV 1e1 --lambda_l2 0.0

#### (3) Blackbox Inverse Network (Section 5)
#### Train inverse network
    python inverse_blackbox_decoder_CIFAR.py --training --layer ReLU22 --iter 50 --decodername CIFAR10CNNDecoderReLU22
#### Inference inverse network
    python inverse_blackbox_decoder_CIFAR.py --testing --decodername CIFAR10CNNDecoderReLU22 --layer ReLU22

#### (4) Query-free Attack (Section 6)

#### Train a shadow model
    python inverse_query_free_CIFAR.py --training --layer ReLU22 --iter 50

#### Inverse the shadow model
    python inverse_query_free_CIFAR.py --testing --layer ReLU22 --iter 500 --learning_rate 1e-1 --lambda_TV 2e0 --lambda_l2 0.0

<br/>

### 3.Tips

(1) Please make sure to use torchvision v0.2.1:

    import torchvision
    print torchvision.__version__

(2) If no gpu supported on your machine, add --nogpu option in the command line.

(3) Please feel free to add --novalidation in your command line if it takes you too long to run in cpu-only mode and the model training/inverse are conducted on the same machine. It will disable evalTest() and evalTestSplitModel(), which are only used for validating the pre-trained models.

<br/>

### 4.Reference
You are encouraged to cite the following paper.
```
@inproceedings{he2019model,
  title={Model inversion attacks against collaborative inference},
  author={He, Zecheng and Zhang, Tianwei and Lee, Ruby B},
  booktitle={Proceedings of the 35th Annual Computer Security Applications Conference},
  pages={148--162},
  year={2019},
  organization={ACM}
}
```

### 5.Environment Setup

1. Create environment
```bash
conda env create --prefix="./.venv" -f environment.yml
```

1. Activate environment
```bash
conda activate "./.venv"
```

1. Deactivate environment
```bash
conda deactivate
```

