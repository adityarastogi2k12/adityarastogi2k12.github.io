# SpiNet

The fast-MRI reconstruction problem is known to be ill-posed and therefore iterative reconstruction techniques with prior regularization are the method of choice. However, these techniques are computationally inefficient and requires manual tuning of regularization parameter and proper selection of prior. Recently, data driven methods based on deep learning (DL) have been able to provide promising results with few questions to be addressed like data dependency, lack of interpretability and lack of uncertainty quantification. We proposed a generic physics and deep learning-based MR image reconstruction model (named SpiNet) that can enforce any Schatten p-norm regularization with 0 < p ≤ 2, where the p can be learnt (or fixed) based on the problem at hand. Both the prior and the regularization parameter are learnt from the data. This network is more interpretable, stable to data perturbations and requires less data to train. Our experiments indicated that the proposed SpiNet shows higher PSNR and SSIM and lower NRMSE than other state-of-the-art methods physics based methods. We validated the performance of SpiNet for various undersampling rates, undersampling masks and on different body organs. For higher undersampling rates greater than 6×, SpiNet significantly outperforms current state-of-the-art method in all metrices with improvement as high as 4 dB in PSNR and 0.05 points in SSIM.  

### This paper is published in **Medical Physics** journal. 

Rastogi A, Yalavarthy PK. SpiNet: A deep neural network for Schatten p-norm regularized medical image reconstruction. Med Phys. 2021 May;48(5):2214-2229. doi: 10.1002/mp.14744. Epub 2021 Mar 22. PMID: 33525049.

Link for paper: https://pubmed.ncbi.nlm.nih.gov/33525049/

This code solves the following optimization problem:

    J(x) = argmin_x ||Ax-b||_2^2 + ||x-Dw(x)||^p_p 

 `A` can be any measurement operator. Here we consider parallel imaging problem in MRI where
 the `A` operator consists of undersampling mask, FFT, and coil sensitivity maps.

`Dw(x)`: it represents the denoiser using a residual learning CNN.

Using Majorization-Minimization algorithm the optimization problem as be modified as:

     G(x|x*) = argmin_x ||Ax-b||_2^2 + p/2||W(x-Dw(x))||^p_p 
     
     W = diag((x*-Dw(x))^{p/2-1})
`x*`: is the point at which `J(x*) = G(x*|x*)`


## Architecture

The architecture of our network is shown below
<p align="center">
  <img src="images/Fig2.jpg" width="1000px" alt=""> 
</p>

## Training Data

The training data for SpiNet consists of brain scans of four patients and 360 images in total. The testing data consists of 164 images from one patients.

Hemant et al. <a href="#modl">[1]</a>. have released the parallel imaging dataset used in their MoDL paper <a href="#modl">[1]</a>. You can download the full dataset from the below link:

Download Link for file "dataset.hdf5" : https://drive.google.com/file/d/1qp-l9kJbRfQU1W5wCjOQZi7I3T6jwA37/view?usp=sharing

## Results

In whole brain region      |   In ROI
:-------------------------:|:-------------------------:
![](https://github.com/adityarastogi2k12/adityarastogi2k12.github.io/blob/master/Projects/SpiNet/images/Fig3_i.jpeg)  |  ![](https://github.com/adityarastogi2k12/adityarastogi2k12.github.io/blob/master/Projects/SpiNet/images/Fig3_ii.jpeg)


## References

<b id="my_anchor">[1].</b> MoDL: Model Based Deep Learning Architecture for Inverse Problems  by H.K. Aggarwal, M.P Mani, and Mathews Jacob in IEEE Transactions on Medical Imaging,  2018 
