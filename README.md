# SuperVAE
This is an implementation of the paper [SuperVAE: Superpixelwise Variational Autoencoder for Salient Object Detection](https://ojs.aaai.org//index.php/AAAI/article/view/4876).

**Salient Object Detection(SOD)** is the detection and segmentation of salient objects or regions. In this work, we have designed salient object detection framework using a variational autoencoder. This method is an unsupervised approach of Salient object detection which works without the supervision of mask-level annotated data. 

The concept of this work based on the following assumption: The boudary region describes the background of an image. So if we can somehow design the background of the image, we can obtain the Salient object inside it. To design this background we need a generative framework for which we used VAE.

The steps of the algorithm is as follows:

1. We preprocessed the image by segmenting it into Superpixels. For a 300 x 400 images we segmented it into three scales (150, 250, 350).
2. From the obtained Superpixels we extracted the boundary Superpixels, and trained a VAE using the superpixels. The parameters of the VAE framework is as shown in the image.
3. While training the VAE we incorporate a perceptual loss along with the KL-divergence and reconstruction loss. The main idea is to seek consistency between hidden representation of two images (original and generated). We replaced the generated Superpixel into the corresponding slot in the image and fed the original image and obtained image to a VGG19 net and measured the losses from the feature-maps. This actually takes into consideration the dependecy of the Superpixels.
