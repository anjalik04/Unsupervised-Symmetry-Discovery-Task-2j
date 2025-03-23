
# Unsupervised Symmetry Discovery (Task 2j)

This repository is following the task guidelines by ML4SCI for the specific task 2j (Semi-supervised Symmetry Discovery) for GSOC 2025.

The project contains three parts:

1.  Dataset Preparation & Latent Space Creation
2.  Supervised Symmetry Discovery
3.  Unsupervised Symmetry Discovery




## Part 1 (Dataset Preparation & Latent Space Creation)

Due to limited computational budged, I will be using only the images labeled as '1' and '2' from the MNIST Dataset as my base dataset.

**Expanding the dataset**: Rotate each image in steps of 30 degrees until a full rotation is achieved.

**Latent Space Creation** (latent dimension = 16):

The model of the VAE used has been described in the image below:
(add image)

Final Latent Space Visualization:
(add image)


## Part 2 (Supervised Symmetry Discovery)

Goal: To create an MLP which learns to transform a latent vector by rotating it by 30 degrees.

For this task, a new dataset had to be prepared.

New dataset preparation: The latent vectors generated in the previous section had to be paired with each other such that the vectors associated with a particular angle theta, were paired up with vectors associated with (theta + 30). The image below explains it better:

(add image)

The architecture of the MLP:
(add image)

After training the MLP, we successfully learn how to rotate vectors in latent space.

By applying the MLP over and over again, we can achieve a full rotation:
(add image)

## Part 3 (Unsupervised Symmetry Discovery)

The paper 'Oracle-Preserving Latent Flows' (link: https://arxiv.org/pdf/2302.00806) has been used as a reference for this section.

Goal: Find symmetries for the rotated MNIST dataset prepared in the first section.

To achieve this goal, we first need to train an MLP to classify the latent vectors as '1' or '2'. This MLP model is called the 'Induced Oracle'.

The architecture used for this MLP is the same as the one designed in the previous section.

Architecture for the generators G:
(add image)
