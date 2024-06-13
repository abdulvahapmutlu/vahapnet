# VahapNet : Deep Learning Network Architecture

This repository contains the MATLAB code and associated files for creating a deep learning network architecture named VahapNet. The network consists of 89 layers and 114 connections, designed for tasks such as image classification and segmentation.

### Files

- **vahapnet.mat**: Contains the pre-trained weights and structure of the VahapNet model.
- **vahap.mlx**: MATLAB live script for generating the layer graph of the VahapNet model. This script creates the deep learning network layers and connects them to form the complete architecture.

### Features

- **Number of Layers**: 89
- **Number of Connections**: 114
- **Layer Types**: Includes convolutional layers, batch normalization layers, GELU activation layers, transposed convolutional layers, grouped convolutional layers, softmax layers, multiplication layers, addition layers, self-attention layers, and bidirectional LSTM layers.

### Usage

1. **Clone the repository**:
    ```bash
    git clone https://github.com/abdulvahapmutlu/vahapnet.git
    cd vahapnet
    ```

2. **Load the network in MATLAB**:
    ```matlab
    load('vahapnet.mat');
    ```

3. **Run the script to create the layer graph**:
    Open `vahap.mlx` in MATLAB and run the script to generate the layer graph in the workspace variable `lgraph`.

### Script Overview

The script (`vahap.mlx`) follows these steps:

1. **Create the Layer Graph**: Initializes the layer graph variable to contain the network layers.
    ```matlab
    lgraph = layerGraph();
    ```

2. **Add Layer Branches**: Adds branches of the network to the layer graph. Each branch is a linear array of layers.
    ```matlab
    tempLayers = [
        imageInputLayer([224 224 3],"Name","imageinput")
        convolution2dLayer([3 3],48,"Name","conv","Padding","same","Stride",[2 2])
        batchNormalizationLayer("Name","batchnorm")
        groupedConvolution2dLayer([3 3],2,"channel-wise","Name","groupedconv","Padding","same","Stride",[2 2])
        geluLayer("Name","gelu")];
    lgraph = addLayers(lgraph,tempLayers);
    ```

3. **Connect Layer Branches**: Connects all the branches of the network to create the network graph.
    ```matlab
    lgraph = connectLayers(lgraph,"gelu","groupedconv_1");
    lgraph = connectLayers(lgraph,"gelu","groupedconv_2");
    ```

4. **Plot the Layer Graph**: Plots the complete layer graph.
    ```matlab
    plot(lgraph);
    ```

### Requirements

- MATLAB with Deep Learning Toolbox
- The provided `vahapnet.mat` and `vahap.mlx` files
