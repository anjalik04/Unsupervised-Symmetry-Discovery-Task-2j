
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
Encoder:
<p align="center">
  <img src = "https://github.com/user-attachments/assets/9f11f044-05d0-4b06-ac37-36770694518c" width = "800"/>
</p>
Decoder:
<p align="center">
<img src = "https://github.com/user-attachments/assets/ccc250bd-7aa9-4689-928b-36007d9c0894" width = "800"/>
</p>


Final Latent Space Visualization:

<p align="center">
  <img src="https://github.com/user-attachments/assets/f7435b26-a8dd-4f1a-94a9-15389a859af7" width="45%"/>
  <img src="https://github.com/user-attachments/assets/1acdbcf3-3555-4ff1-b37f-b1078bd1a736" width="40%"/>
</p>

We can see that the images labeled 1 show a unique pattern in the second image (i.e. visualization of rotated angles). For an image labeled '1', we can see in the below picture: 
<p align="center">
  <img src = "https://github.com/user-attachments/assets/9c70f47f-3846-40a0-9633-d63559d5055a" width = "800"/>
</p>

* The 0 degree rotated version is very similar to the 180 degree rotated version.
* The 30 degree rotated version is very similar to the 210 degree rotated version.
* The 60 degree rotated version is very similar to the 240 degree rotated version.
* And so on.
  
Thus, this pattern should reflect in the latent space. And if we look carefully, it does reflect in the above image.

## Part 2 (Supervised Symmetry Discovery)

Goal: To create an MLP which learns to transform a latent vector by rotating it by 30 degrees.

For this task, a new dataset had to be prepared.

New dataset preparation: The latent vectors generated in the previous section had to be paired with each other such that the vectors associated with a particular angle theta, were paired up with vectors associated with (theta + 30). The image below explains it better:

<p align="center">
  <img src = "https://github.com/user-attachments/assets/085e3322-4da7-4ee1-abcb-2d559e911512" width = "800"/>
</p>

After training the MLP, we successfully learn how to rotate vectors in latent space.
<p align="center">
  <img src = "https://github.com/user-attachments/assets/28e7259b-fae9-4fb1-a3ed-6dfbe837d4a1" width = "800"/>
</p>

By applying the MLP over and over again, we can achieve a full rotation:
<p align="center">
  <img src = "https://github.com/user-attachments/assets/cc3eae4c-7336-473a-9325-3084e2436543" width = "800"/>
</p>

## Part 3 (Unsupervised Symmetry Discovery)

The paper 'Oracle-Preserving Latent Flows' (link: https://arxiv.org/pdf/2302.00806) has been used as a reference for this section.

Goal: Find symmetries for the rotated MNIST dataset prepared in the first section.

To achieve this goal, we first need to train an MLP to classify the latent vectors as '1' or '2'. This MLP model is called the 'Induced Oracle'.

The architecture for the generators G is the same as the MLP designed in the previous section.

A different approach for closure loss was taken, as stated in this paper: (link: https://arxiv.org/pdf/2301.05638), "Another possible approach is to minimize the out-of-space components of the commutators with respect to the space of generators, after flattening and Gram–Schmidt orthonormalization."

The results of the trained generator model can be seen below: (The visualization follows the format of the plot shown in the paper. The original image is in the centre and the transformation is applied in steps of 3000 to the left and to the right.)

<p align="center">
  <img src = "https://github.com/user-attachments/assets/beb4d753-a16a-43ef-8956-5903ed9f1019" width = "800"/>
</p>

We can see that the generator is partially succesful at learning the rotation transformation. More results can be found in the jupyter notebook.

The trained weights for all models are present in the github repository.
