# Homework 2b            
### Kelly Perkins     2026-3-16
## 3 a and b
- I downloaded the MNIST dataset and plotted 10 random images using the following script:
```
import random
import torch
from torchvision import datasets, transforms
import matplotlib.pyplot as plt

base_transform = transforms.ToTensor()

train_ds = datasets.MNIST(
    root='./data', train=True, download=True, transform=base_transform
)

# Pick 10 random indices from the training dataset
indices = random.sample(range(len(train_ds)), 10)

# Create a 2x5 grid
fig, axes = plt.subplots(2, 5, figsize=(10, 4))

for ax, idx in zip(axes.flatten(), indices):
    img, label = train_ds[idx]

    # img may be a tensor (C, H, W); squeeze channel for plotting
    if img.ndim == 3:
        img = img.squeeze(0)

    ax.imshow(img, cmap="gray")
    ax.set_title(f"Label: {label}")
    ax.axis("off")

plt.suptitle("Random MNIST Training Examples", fontsize=14)
plt.tight_layout()
plt.show()
plt.savefig("mnist_random_examples.png", dpi=300)
plt.close()

```
- This produced the following image where the numbers appeared to be labeled correctly.

![alt text](https://github.com/kap277/ML_in_ES/blob/main/Figure_1.png?raw=true "Random MNIST Training Example")

## 3c
#
-I was a bit confused here because I couldn't tell if this was meant as a stand alone question since the title is "code a neural network to classify these images" then you get to the forward pass skeleton code in the next question. I may have thought this was meant to start to set up the training and validation sets for the rest of the questions but because the forward pass code says "do not edit" in the top sections and because of the title I am taking my best guess and treating this as a stand alone that we are meant to code a network and classify the images here before proceeding to write our own.
-For the above reason I edited the mnist_simple.py script to awnser the questions here.

-

```
ssh -X kperkins@casper.hpc.ucar.edu
cd /glade/work/kperkins
ls
```
