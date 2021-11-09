# Comparison of iterative parametric and indirect deep learning based reconstruction methods in highly
**These Matlab & Python codes are used as part of the work presented in:**

This article is accepted for publication in **Medical Physics** journal 

<b>Aditya Rastogi and Phaneendra K. Yalavarthy, “Comparison of iterative parametric and indirect deep learning-based reconstruction methods in highly undersampled DCE‐MR Imaging of the breast," Medical Physics, (2020), [https://doi.org/10.1002/mp.14447](https://aapm.onlinelibrary.wiley.com/doi/abs/10.1002/mp.14447)</b>



Due to the size of the code, testing data (Patient B) and trained model weights the code is uploaded on Google Drive. **The link to the code is attached below**:-

[https://drive.google.com/drive/folders/12Byg-207xGgg6Sq13eYl2l-VGejXD7SV?usp=sharing](https://drive.google.com/drive/folders/12Byg-207xGgg6Sq13eYl2l-VGejXD7SV)

Please mail me at **adityar[at]iisc[dot]ac[dot]in** if you encounter any problem in Downloading, Executing or understanding the code.

## Inverse Model

The forward and inverse modelling of Tracer Kinetic parameter estimation problem is shown below:
<p align="center">
  <img src="images/Fig1.jpeg" width="1000px" alt=""> 
</p>

## Codes
The code has 4 folders:-

1. **Test_Direct** :- Constructs the Ktrans map using iterative direct reconstruction techniques.This generates the following

  - Fully sampled Ktrans (ground truth)
  - Ktrans with zero padding (US)
  - Ktrans with no regularization (L2), TV+L1 regularisation, L1 regularization only and TV regularization only.
  - This code is based on work done by Yi. Guo1 in this paper "Direct Estimation of Tracer-Kinetic Parameter Maps from Highly Undersampled Brain DCE-MRI" and uses     some codes and libraries from his program available at ["https://github.com/usc-mrel/DCE_direct_recon".](https://github.com/usc-mrel/DCE_direct_recon)
  
  - This folder has 4 main files/folder:-
  
    1. **main.m**  :-  This file executes the code and estimates Ktrans map for undersampling rate of 20X, 50X and 100X.
   
    2. **lam_mat.mat** :- This .mat file contains the regularization parameter values of all methods for all undersampling rates.
   
    3. **Dataset** :- This folder contains the dataset of patient B.
   
    4. **Vol** :-  This folder contains the recontructed Ktrans map of patient B for all undersampling rates (R).
   
2. **Test_NN** :-  This folder contains the DL based models for indirect reconstruction of Ktrans maps. This code contains three folders:-
  

   - **ISTA-Net_plus*** :- This folder contains the weights and testing file of ISTA-Net+[2]  as mentioned in paper :- "ISTA-Net: Interpretable Optimization-            Inspired Deep   Network for Image Compressive Sensing". This folder contains testing model and files for 20X, 50X and 100X undersampling. **The test data          of patient B and           undersampling mask are present in folder of MODL.**  This code is used to estimate high resolution anatomical images from              undersampled K-t space Data

- **MODL**:- This folder contains the trained models for 20X,50X and 100X undersampling. This code is used to estimate high resolution anatomical images from           undersampled K-t space Data. This method is give by Hemant Kumar Aggarwal in his paper "MoDL: Model Based Deep Learning Architecture for Inverse Problems" and     the   original code of the paper is available at  [https://github.com/hkaggarwal/modl . ](https://github.com/hkaggarwal/modl)

     1.This folder also contains a folder name test_datasets which has the testing dataset of Patient B and the 20X, 50X and 100X undersampling masks.

 - **TK_modelling**:- This folder has 4 main components:-

   1. **recon_NN** :- This folder contains the .h5py file that is reconstructed from MODL and ISTA-Net+ .

   2. **vol** :- This folder contains the estimated Ktrans maps using the reconstructed anatomical images of MODL and ISTA-Net+ .

   3. **Vol_ISTA_NN_Kt_Vp_SEN_AD_3d.m** :- This file estimates Ktrans map from reconstructed anatomical images  (via ISTA-Net+ ).

   1. **Vol_MODL_NN_Kt_Vp_SEN_AD_3d.m** :- This file estimates Ktrans map from reconstructed anatomical images  (via MODL ).

3.**Generate Results**:- This folder contains code and data to compare the results of direct and indirect estimation techniques. This folder has 3 main files/folders:-

- **compare.m** :- This file compares the reconstructed Ktrans map from direct reconstruction techniques and indirect reconstruction techniques using 4 metrices (PSNR, nRMSE, SSIM and Xydeas metric).

- **Vol_NN** :- This folder contains the Ktrans maps reconstructed using indirect DL based techniques for all R.

- **Vol** :- This folder contains the recontructed Ktrans map of patient B for all undersampling rates (R).

4. **Make_plots** :- This folder plots the barchart of performance of direct and indirect estimation techniques for Patient B. It has a folder:-

- **datasets**:- This folder contains a .mat file which consists of performance results of the US, L2, TV+L1 in terms of PSNR, nRMSE, SSIM and Xydeas metric.

- **barplot.py** :- Is the python execution file.


## Results

We estimated the Ktrans Maps from 20X, 50X and 100X undersampled DCE-MRI data using golden radial angle undersampling pattern. The result for **PAT B** for all reconstruction methods methods mentioned above is shown below:
<p align="center">
  <img src="images/Fig9.jpeg" width="800px" alt=""> 
</p>

The difference images are shown below:
<p align="center">
  <img src="images/Fig10.jpeg" width="800px" alt=""> 
</p>
