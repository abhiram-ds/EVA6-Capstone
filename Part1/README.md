# EVA6 Capstione Project: Part-1

This file explains the questions raised as a part of the EVA6 Computer Vision Capstone project Part-1.

## Panoptic Segmentation: Architecure Overview

![image](https://user-images.githubusercontent.com/71654199/130331110-d56dbd51-55e7-4aa4-a5f2-3f2e6f95848c.png)

## 1. We take the encoded image (dxH/32xW/32) and send it to Multi-Head Attention (FROM WHERE DO WE TAKE THIS ENCODED IMAGE?)

The encoded image (dxH/32xW/32) is obtained as the output of the encoder network in the Encoder-Decoder.
The image is initially fed into a Convolutional Neural Network (CNN) with ResNet backbone. The ResNet-backbone CNN architecture consists of 5 layers. The ouput of the 5th layer is fed into the Multi-head attention in the Encoder part of the network. The Encoder output is nothing but the Encoded image of size dxH/32xW/32.
This forms one of the inputs to the "Multi-Head Attention: in Panoptic Segmentation.

## 2. We do something here to generate NxMxH/32xW/32 maps. (WHAT DO WE DO HERE?)

The Obhect embeddings are the output of the Decoder part int he Encoder-Decoder network. Both the Object mebeddinds and the Encoded image (from encoder) are passed as input to the "Multi-Head Attention". This will reurn the Attention Maps of the encoded image for each Object Embedding. 
Th4 4 bounding boxes from Decoder will result in 4 Object embeddings and combined with Encoded image in Multi-Head attention, these will result in 4 Attention maps.
Each map will be of the size NxMxH/32xW/32.

N is the no. os object embeddings
M  = d/N where d is the count of channle in the output of ResNet.

## 3. Then we concatenate these maps with Res5 Block (WHERE IS THIS COMING FROM?)

The activations maps from the 2,3,4 & 5th layers of the ResNet-backbine architecture are stored as Res2, 3 4 & 5.
We add these maps with corresponding activation maps and upsample the image until NxH/4xW/4.

## 4. Steps in the approach to be implemented

1. Data Collection and preparation
 - Gather the Annotated image dataset.
 - The images are then used in other network to get predictions for the stuff
 - The existing annotation and predicted annotation shall be combined to arrive at the final dataset.

2. Desing the backbone ResNet50 architecture.
3. Predict the bounding boxes by training the model.
4. The weights can then be frozen and the model be trained for Panoptic Segmentation.




