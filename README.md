# TIRG Composing Text and Image for Image Retrieval with Bonn Furniture Styles dataset

This project is an attempt to use TIRG function for image retrieval with new furniture style dataset. The originally code was published with the paper:

**<a href="https://arxiv.org/abs/1812.07119">Composing Text and Image for Image Retrieval - An Empirical Odyssey
</a>**
<br>
Nam Vo, Lu Jiang, Chen Sun, Kevin Murphy, Li-Jia Li, Li Fei-Fei, James Hays
<br>
CVPR 2019.
**<a href="https://github.com/google/tirg">github code source</a>**

The dataset was published with the paper below:

**<a href="https://arxiv.org/abs/1812.07119">Learning Style Compatibility for Furniture
</a>**
<br>
Divyansh Aggarwal, Elchin Valiyev, Fadime Sener, and Angela Yao
<br>
CVPR 2018.
**<a href="https://cvml.comp.nus.edu.sg/furniture/download.html">dataset download</a>**

## Introduction

In this paper, we study the task of image retrieval, where the input query is
specified in the form of an image plus some text that describes desired
modifications to the input image.

We propose a new way to combine image and
text using TIRG function for the retrieval task. We show this outperforms
existing approaches on different datasets.

## Setup

- torchvision
- pytorch
- numpy
- tqdm
- tensorboardX

## Running Models

- `main.py`: driver script to run training/testing
- `datasets.py`: Dataset classes for loading images & generate training retrieval queries
- `text_model.py`: LSTM model to extract text features
- `img_text_composition_models.py`: various image text compostion models (described in the paper)
- `torch_function.py`: contains soft triplet loss function and feature normalization function
- `test_retrieval.py`: functions to perform retrieval test and compute recall performance

### FurnitureStyle dataset

Download our generated test_queries.txt from [here](furniture-style/test_queries.txt).

Make sure the dataset include these files:

```
<dataset_path>/splits/*.txt
<dataset_path>/houzz/<category>/<style>/*.jpeg
<dataset_path>/test_queries.txt`
```

note

Run training & testing:

```
python main.py --dataset=furnitureStyle --dataset_path=./furniture-style \
  --num_iters=160000 --model=concat --loss=batch_based_classification \
  --learning_rate_decay_frequency=50000 --comment=f200k_concat

python3 main.py --dataset=furnitureStyle --dataset_path=./furniture-style \
  --num_iters=160000 --model=tirg --loss=batch_based_classification \
  --learning_rate_decay_frequency=50000 --comment=f200k_tirg
```
