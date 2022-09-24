# FedDrive: Generalizing Federated Learning to Semantic Segmentation in Autonomous Driving

**Official website** of [FedDrive: Generalizing Federated Learning to Semantic Segmentation
in Autonomous Driving](https://arxiv.org/abs/2202.13670) 

by **Lidia Fantauzzo**<sup>\*,1</sup>, **Eros Fanì**<sup>\*,1</sup>, Debora Caldarola<sup>1</sup>,
Antonio Tavera<sup>1</sup>, Fabio Cermelli<sup>1,2</sup>, Marco Ciccone<sup>1</sup>, Barbara Caputo<sup>1</sup>. 

**Corresponding authors:** lidia.fantauzzo@studenti.polito.it, eros.fani@polito.it.

<sup>\*</sup>Equal contribution. <sup>1</sup>All the authors are supported by Politecnico di Torino, Turin, Italy. 
<sup>2</sup>Fabio Cermelli is with Italian Institute of Technology, Genoa, Italy.

<img src="teaser.png" alt="drawing" width="800"/>

## Citation

If you find our work relevant to your research, or use this code, please cite our IROS 2022 paper:

```
@inproceedings{feddrive2022,
  title={FedDrive: Generalizing Federated Learning to Semantic Segmentation in Autonomous Driving},
  author={Fantauzzo, Lidia and Fani', Eros and Caldarola, Debora and Tavera, Antonio and Cermelli, Fabio and Ciccone, Marco and Caputo, Barbara},
  booktitle={Proceedings of the 2022 IEEE/RSJ International Conference on Intelligent Robots and Systems},
  year={2022}
}
```

## Summary

FedDrive is a new benchmark for the Semantic Segmentation task in a Federated Learning scenario for self-driving cars.
It consists of three settings and two datasets, incorporating the real-world challenges of statistical heterogeneity
and domain generalization. FedDrive is a benchmark of state-of-the-art algorithms and style transfer methods taken from
the Federated Learning, Domain Generalization, and Domain Adaptation literature, whose objective is to improve the
generalization ability and robustness statistical heterogeneity robustness of the model. We demonstrate that correctly
handling normalization statistics is crucial to deal with the aforementioned challenges. Furthermore, style transfer
dramatically improves performance when dealing with significant appearance shifts.

## Abstract

Semantic Segmentation is essential to make self-driving vehicles autonomous, enabling them to understand their surroundings by assigning individual pixels to known categories. However, it operates on sensible data collected from the users' cars; thus, protecting the clients' privacy becomes a primary concern. For similar reasons, Federated Learning has been recently introduced as a new machine learning paradigm aiming to learn a global model while preserving privacy and leveraging data on millions of remote devices. Despite several efforts on this topic, no work has explicitly addressed the challenges of federated learning in semantic segmentation for driving so far. To fill this gap, we propose FedDrive, a new benchmark consisting of three settings and two datasets, incorporating the real-world challenges of statistical heterogeneity and domain generalization. We benchmark state-of-the-art algorithms from the federated learning literature through an in-depth analysis, combining them with style transfer methods to improve their generalization ability. We demonstrate that correctly handling normalization statistics is crucial to deal with the aforementioned challenges. Furthermore, style transfer improves performance when dealing with significant appearance shifts.

## Source code

PyTorch code for our paper is open-source and available on [GitHub](https://github.com/Erosinho13/FedDrive).

## Results

### Cityscapes

| Method           | mIoU &#177; std (%)   |
|------------------|-----------------------|
| FedAvg (uniform) | 45.71 &#177; 0.37     |
| FedAvg           | 43.85 &#177; 1.24     |
| FedAvg + CFSI    | 41.50 &#177; 0.98     |
| FedAvg + LAB     | 39.20 &#177; 1.37     |
| **SiloBN**       | **44.20 &#177; 1.43** |
| SiloBN + CFSI    | 40.48 &#177; 1.40     |
| SiloBN + LAB     | 42.23 &#177; 1.23     |

### IDDA

The *seen* and *unseen* columns refer to the results for the test client that contains images from the same training
domains and to the test client that contains images from other domains, respectively. Results are reported in the form
mIoU &#177; std (%).

| Method           | Setting     | seen                  | unseen                |
|------------------|-------------|-----------------------|-----------------------|
| FedAvg (uniform) | country     | 63.57 &#177; 0.60     | 49.74 &#177; 0.79     |
| FedAvg           | country     | 42.43 &#177; 1.78     | 40.01 &#177; 1.26     |
| FedAvg + CFSI    | country     | 54.70 &#177; 1.12     | 45.70 &#177; 1.73     |
| FedAvg + LAB     | country     | 56.59 &#177; 0.90     | 45.68 &#177; 1.04     |
| FedBN            | country     | 54.39                 | -                     |
| SiloBN           | country     | 58.82 &#177; 2.93     | 45.32 &#177; 0.90     |
| SiloBN + CFSI    | country     | 61.22 &#177; 3.88     | 49.17 &#177; 1.01     |
| **SiloBN + LAB** | **country** | **64.32 &#177; 0.76** | **50.43 &#177; 0.63** |
| FedAvg           | rainy       | 62.72 &#177; 3.35     | 27.61 &#177; 2.80     |
| FedAvg + CFSI    | rainy       | 38.18 &#177; 1.40     | 26.75 &#177; 2.32     |
| FedAvg + LAB     | rainy       | 55.24 &#177; 1.65     | 31.05 &#177; 2.68     |
| FedBN            | rainy       | 56.45                 | -                     |
| SiloBN           | rainy       | 62.48 &#177; 1.42     | 50.03 &#177; 0.79     |
| SiloBN + CFSI    | rainy       | 63.04 &#177; 0.31     | 50.54 &#177; 0.88     |
| **SiloBN + LAB** | **rainy**   | **65.85 &#177; 0.91** | **53.99 &#177; 0.79** |

### Server optimizers comparison on IDDA

The *seen* and *unseen* columns refer to the results for the test client that contains images from the same training
domains and to the test client that contains images from other domains, respectively. Results are reported in the form
mIoU &#177; std (%).

| Distribution      | Setting     | Method     | Optimizer   | seen                  | unseen                |
|-------------------|-------------|------------|-------------|-----------------------|-----------------------|
| uniform           | country     | FedAvg     | SGD         | 63.57 &#177; 0.60     | 49.74 &#177; 0.79     |
| **uniform**       | **country** | **FedAvg** | **FedAvgM** | **71.27 &#177; 0.85** | **55.47 &#177; 1.07** |
| uniform           | country     | FedAvg     | Adam        | 63.31 &#177; 0.37     | 50.21 &#177; 0.40     |
| uniform           | country     | FedAvg     | AdaGrad     | 59.44 &#177; 0.94     | 46.09 &#177; 0.83     |
| uniform           | rainy       | FedAvg     | SGD         | 62.72 &#177; 3.65     | 27.61 &#177; 2.80     |
| **uniform**       | **rainy**   | **FedAvg** | **FedAvgM** | **70.99 &#177; 0.71** | **29.83 &#177; 2.03** |
| uniform           | rainy       | FedAvg     | Adam        | 65.39 &#177; 0.52     | 31.72 &#177; 1.74     |
| uniform           | rainy       | FedAvg     | AdaGrad     | 59.45 &#177; 1.30     | 27.80 &#177; 1.29     |
| heterogeneous     | country     | FedAvg     | SGD         | 42.43 &#177; 1.78     | 40.01 &#177; 1.26     |
| **heterogeneous** | **country** | **FedAvg** | **FedAvgM** | **44.38 &#177; 1.98** | **42.42 &#177; 2.15** |
| heterogeneous     | country     | FedAvg     | Adam        | 39.93 &#177; 2.44     | 38.15 &#177; 1.89     |
| heterogeneous     | country     | FedAvg     | AdaGrad     | 40.89 &#177; 2.05     | 38.03 &#177; 1.65     |
| heterogeneous     | rainy       | FedAvg     | SGD         | 38.18 &#177; 1.40     | 26.75 &#177; 2.32     |
| **heterogeneous** | **rainy**   | **FedAvg** | **FedAvgM** | **41.21 &#177; 1.98** | **31.91 &#177; 3.77** |
| heterogeneous     | rainy       | FedAvg     | Adam        | 37.97 &#177; 2.04     | 28.47 &#177; 2.56     |
| heterogeneous     | rainy       | FedAvg     | AdaGrad     | 39.02 &#177; 1.71     | 27.08 &#177; 2.85     |
| heterogeneous     | country     | SiloBN     | SGD         | 58.82 &#177; 2.93     | 45.32 &#177; 0.90     |
| **heterogeneous** | **country** | **SiloBN** | **FedAvgM** | **61.99 &#177; 1.51** | **46.20 &#177; 1.20** |
| heterogeneous     | country     | SiloBN     | Adam        | 58.36 &#177; 1.26     | 42.31 &#177; 0.84     |
| heterogeneous     | country     | SiloBN     | AdaGrad     | 48.97 &#177; 1.34     | 41.69 &#177; 1.31     |
| **heterogeneous** | **rainy**   | **SiloBN** | **SGD**     | **62.48 &#177; 1.42** | **50.03 &#177; 0.79** |
| **heterogeneous** | **rainy**   | **SiloBN** | **FedAvgM** | **63.69 &#177; 1.25** | **48.49 &#177; 1.04** |
| heterogeneous     | rainy       | SiloBN     | Adam        | 61.51 &#177; 0.90     | 47.22 &#177; 0.89     |
| heterogeneous     | rainy       | SiloBN     | AdaGrad     | 54.06 &#177; 1.29     | 45.80 &#177; 0.89     |