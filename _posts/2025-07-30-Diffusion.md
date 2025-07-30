---
layout: post
title: Generative AI Seminar (Diffusion Models)
date: 2025-07-30 08:57:00-0400
description: Basics of diffusion model
tags: formatting jupyter
categories: sample-posts
giscus_comments: false
related_posts: false
---

{::nomarkdown}
{% assign jupyter_path = "assets/jupyter/Diffusion_slides.ipynb" | relative_url %}
{% capture notebook_exists %}{% file_exists assets/jupyter/blog.ipynb %}{% endcapture %}
{% if notebook_exists == "true" %}
{% jupyter_notebook jupyter_path %}
{% else %}

<p>Sorry, the notebook you are looking for does not exist.</p>
{% endif %}
{:/nomarkdown}

We aim to demonstrate the mathematical definitions presented in the slides through practical examples.

```python
#### import required libraries #####
import torch  # for matrix processing
import torch.nn as nn  # for neural network modules
import torch.nn.functional as F # for using some pre-defined functions
import torch.optim as optim # different optimization algorithm
import torchvision  # for image processing
import torchvision.transforms as transforms # for doing some transformation on the input data
from torchvision.datasets import MNIST # hand-written digit dataset
from torch.utils.data import DataLoader # for loading dataset
import numpy as np # to do some linear algebra
import matplotlib.pyplot as plt # for showing the result
from tqdm import tqdm # for some fancy plotting and formatting
import copy # to copy data
import random # for randomness

## do pre-process on the data (resizing and transform to Tensor class)
transform = transforms.Compose([transforms.Resize((32, 32)), transforms.ToTensor()])
## Load train dataset
train_dataset = MNIST(root='./data', train=True, download=True, transform=transform)
## Create a dataloader for the train dataset
train_loader = DataLoader(train_dataset, batch_size=64, shuffle=False)
#some functions to show the images
def show(img):
    npimg = img.numpy()
    plt.imshow(npimg, interpolation='nearest')

# if you have GPU, use it
device = torch.device('cuda' if torch.cuda.is_available() else 'cpu')


# Loading one batch of data
images, labels = next(iter(train_loader)) # load from the dataloader

# plot data and label
plt.figure(figsize=(10,4))
for index in np.arange(0,5):
  plt.subplot(1,5,index+1)
  plt.axis('off')
  plt.title(f'Label: {labels[index].item()}')
  plt.imshow(images[index].squeeze().numpy())


## Set Random seed to generate same results in different runs
np.random.seed(0)
random.seed(0)
torch.manual_seed(0)
######
# Load a batch of data
images, labels = next(iter(train_loader))
# copy the first image in the batch as noisy data
noisy_image_1 = copy.deepcopy(images[0])
######
# draw sample from N(0,I) with the  shape of the image
epsilon_1 = torch.normal(0, 1, noisy_image_1.shape,generator=torch.manual_seed(0))
# Define Beta parameter
Beta_1 = 0.1
# Define the number of steps to add noise to the image
noise_steps = 2
plt.figure(figsize=(10,noise_steps * 2))
# Add noise to data in a loop
for i in range(noise_steps):
    plt.subplot(1,noise_steps,i+1)
    # plot the original image
    plt.imshow(noisy_image_1.squeeze())
    plt.axis('off')
    # generate a noisy image based on the formulation in the slides in each step
    noisy_image_1 = np.sqrt(Beta_1) * epsilon_1 + np.sqrt(1-Beta_1) * noisy_image_1
plt.show()
##############################################################################

## Directly find the noisy image without iteration
plt.figure(figsize=(10,noise_steps * 2))
plt.subplot(1,2,1)
noisy_image_2 = copy.deepcopy(images[0])
epsilon_2 = torch.normal(0, 1, noisy_image_2.shape,generator=torch.manual_seed(0))
Beta = 0.1
plt.imshow(noisy_image_2.squeeze())
plt.axis('off')
alpha_bar_2 = (1-Beta)*(1-Beta)
noisy_image_2 = np.sqrt(alpha_bar_2) * noisy_image_2 + np.sqrt(1-alpha_bar_2) * epsilon_2
plt.subplot(1,2,2)
plt.imshow(noisy_image_2.squeeze())
plt.axis('off')
plt.show()
#############################################################
# def Alpha_bar_n(Beta,n):
#     return (1-Beta)**n
# plt.figure(figsize=(10,noise_steps * 2))
# plt.subplot(1,2,1)
# n=10
# Beta = 0.1
# plt.subplot(1,2,1)
# noisy_image_n = copy.deepcopy(images[0])
# plt.imshow(noisy_image_n.squeeze())
# plt.axis('off')
# epsilon_n = torch.normal(0, 1, noisy_image_n.shape,generator=torch.manual_seed(n))
# alpha_bar_n = Alpha_bar_n(Beta,n)
# noisy_image_n = np.sqrt(alpha_bar_n) * noisy_image_n + np.sqrt(1-alpha_bar_n) * epsilon_n
# plt.subplot(1,2,2)
# plt.imshow(noisy_image_n.squeeze())
# plt.axis('off')
# plt.show()
#######################################################


# After some iterations, the complex distribution of data converts to the normal N(0, I)
# For plotting
import seaborn as sns

# Made a complex data distribution
x =np.hstack((np.random.normal(loc=0.0, scale=1.0, size=1000), np.random.normal(loc=5.0, scale=2.0, size=1000),np.random.normal(loc=7.0, scale=2.0, size=1000)))
# sns.kdeplot(x)


epsilon_1 = torch.normal(0, 1, x.shape,generator=torch.manual_seed(0))
Beta_1 = 0.1
noise_steps = 17
plt.figure(figsize=(noise_steps * 2,3))
for i in range(noise_steps):
    plt.subplot(1,noise_steps,i+1)
    plt.title(f'Step {i+1}')
    sns.kdeplot(x)
    plt.axis('off')
    x = np.sqrt(Beta_1) * epsilon_1 + np.sqrt(1-Beta_1) * x
```

{::nomarkdown}
{% assign jupyter_path = "assets/jupyter/Diffusion.ipynb" | relative_url %}
{% capture notebook_exists %}{% file_exists assets/jupyter/blog.ipynb %}{% endcapture %}
{% if notebook_exists == "true" %}
{% jupyter_notebook jupyter_path %}
{% else %}

<p>Sorry, the notebook you are looking for does not exist.</p>
{% endif %}
{:/nomarkdown}
