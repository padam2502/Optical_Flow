

# Optical_Flow

This project implements the Single-Scale Lucas-Kanade Optical Flow algorithm on a set of images from the Middlebury Optical Flow dataset. The implementation consists of two main parts:



## 1: Keypoint Selection: Selecting Pixels to Track

The first part of the implementation involves selecting feature points to track using OpenCV’s Harris Corner Detector implementation. The feature points obtained by the algorithm are visualized by superimposing them on the images. This part of the implementation is based on the 1988 work, "A Combined Corner and Edge Detector" by Chris Harris and Mike Stephens.

## 2: Forward-Additive Sparse Optical Flow

The second part of the implementation involves implementing the single-scale Lucas-Kanade (LK) algorithm based on the work described in the classic 1981 IJCAI paper "An iterative image registration technique with an application to stereo vision" by Bruce D. Lucas and Takeo Kanade. The algorithm computes the optical flow between two consecutive frames by finding the motion (u, v) that minimizes the sum-squared error of the brightness constancy equations for each pixel in a window.

The main task is broken down into the following sub-parts:

- Visualizing the dense optical flow of the .flo files given using the provided helper code.
- Implementing the sparse LK Method.
- Plotting and comparing the implementation and OpenCV implementation for all consecutive frames for the three sequences.  
- Quiver plots are superimposed on the images. The OpenCV implementation uses multi-scale LK so it is alright if the results are not the same, but the general flow will still be the same.
- Creating a video out of the images to show the optical flow (optional task).
- Computing the Average End Point Error (EPE) between the ground truth optical flow in .flo files and the predicted optical flow for the feature points detected.
- The project uses all the given image sequences from the Middlebury Optical Flow dataset throughout part two to test the algorithm.


# 3: Multi-Scale Coarse-to-fine Optical Flow

This project builds upon the implementation of the single-scale Lucas-Kanade algorithm in Part 2, by implementing the multi-scale coarse-to-fine optical flow estimation.

## Overview
The multi-scale coarse-to-fine optical flow estimation algorithm is a refinement of the single-scale algorithm. It works by first computing the optical flow at a coarse image resolution, which is then iteratively refined at successively higher resolutions, up to the resolution of the original input images. This approach effectively computes the optical flow using successively smaller apertures and works well on images with large displacements, something the single-scale algorithm is unable to handle.

## Implementation Details
The implementation involves modifying the code from Part 2 to accept and refine parameters u0 and v0, which correspond to the initial estimates of the optical flow. The OpticalFlowRefine function refines the optical flow according to the formula u = u0 + ∆u and v = v0 + ∆v, where ∆u and ∆v represent the offset between the initial estimate and the refined estimate. To compute ∆u and ∆v, the window in Img2 is shifted by (u0,v0) and the optical flow is computed between the shifted windows.

The MultiScaleLucasKanade function calls the OpticalFlowRefine function to implement the multi-scale coarse-to-fine optical flow estimation algorithm.

The algorithm works as follows:

Gaussian smooth and scale Img1 and Img2 by a factor of 2^(1-numLevels).
Compute the optical flow at this resolution.
For each level,
a. Scale Img1 and Img2 by a factor of 2^(1-level).
b. Upscale the previous layer's optical flow by a factor of 2.
c. Compute u and v by calling OpticalFlowRefine with the previous level's optical flow.
## Tasks
The tasks for this project are as follows:

Implement the multi-scale coarse-to-fine optical flow estimation algorithm.
Compute EPE error values (only on feature points detected by you) and compare against Part 2.
Generate images with the optical flow for single-scale LK, multiscale LK, and OpenCV implementation and analyze the results.
## Dataset
The image sequences from the Middlebury Optical Flow dataset will be used to test the algorithm
