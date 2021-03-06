# IVIM-DKI analysis with total variation penalty function for prostate lesions
---------------------------------------------------------------------------------

A package providing MATLAB programming tools and GUI for IVIM-DKI analysis with total
variation (TV) penalty function for prostate cancer and benign prostatic hyperplasia (BPH).

---------------------------------------------------------------------------------
**REFERENCES:** 

[1] Malagi, A. V. et al. (2021). IVIM-DKI differentiation between prostate cancer 
and benign prostatic hyperplasia: comparison of 1.5T vs. 3T MRI. 
Magnetic Resonance Materials in Physics, Biology and Medicine. DOI : 10.1007/s10334-021-00932-1

[2] Kayal, E. B. et al. (2017). Quantitative analysis of intravoxel 
incoherent motion (IVIM) diffusion MRI using total variation and Huber penalty function. 
Medical physics, 44(11), 5849-5858.

---------------------------------------------------------------------------------
If you have any queries or suggestions about this package, kindly contact 
Dr. Amit Mehndiratta, Indian Institute of Technology Delhi, India. 

E-mail: <amehndiratta@cbme.iitd.ac.in>, <amit.mehndiratta@keble.oxon.org>.

---------------------------------------------------------------------------------
Disclaimer: This project can be used only for research purposes. Authors are not liable for any clinical use of it, authors could not be held responsible.

---------------------------------------------------------------------------------
- Version 1.0: May 2021
---------------------------------------------------------------------------------

### This package consists of app installer and two folders:

1. **'ivimDKItvtool.mlappinstall'**: Matlab App installer for accessing IVIM-DKI with TV analysis toolbox 'ivimDKItvtool'. Kindly click install the app ivimDKItvtool.mlappinstall by double-click on the icon and app gets installed after clicking 'install'. After installation, click on 'APPS' section in matlab and then select ivimDKItvtool icon to start the app. 
 
  - ivimDKItvtool app execute IVIM-DKI analysis with TV, consisting of two tabs: 
     1. Input Data and Analysis, where user needs to select IVIM-DKI data and define parameters; these inputs are fed to IVIM-DKI model with TV after clicking on 'Analyse IVIM-DKI model with TV', and analysis can also be initiated with default parameters defined in the app.
     2. Output, where IVIM-DKI parameter maps can be viewed in different colormaps and saved as nii.gz format. ROI statistics also included in this tab, where ROI can be loaded such as tumor, BPH, or PZ ROI and statistics can be performed after clicking on 'Calculate ROI stats and Save statistics' where, mean and standard deviation of IVIM-DKI parameters are calculated, which is displayed on app and saved as .txt file for ROI provided.
   
    - ivimDKItvtool app tab: Input Data and Analysis display
      ![image](https://user-images.githubusercontent.com/66351266/119849766-883a8400-bf2a-11eb-9fe9-2add9eebb8ac.png)

    - ivimDKItvtool app tab: Output display
      ![image](https://user-images.githubusercontent.com/66351266/119849888-a6a07f80-bf2a-11eb-9c15-d86982acd92a.png)


2. **[IVIM_DKI_data](https://github.com/amitvmehndiratta/IVIM-DKI-MRMP2021/tree/main/IVIM_DKI_data)**: The folders consist of IVIM-DKI 4D data acquried at [1.5T](https://github.com/amitvmehndiratta/IVIM-DKI-MRMP2021/tree/main/IVIM_DKI_data/IVIM_DKI_1_5T) and [3T](https://github.com/amitvmehndiratta/IVIM-DKI-MRMP2021/tree/main/IVIM_DKI_data/IVIM_DKI_3T) MRI. In these folders 4D IVIM-DKI data named as 'ivim13b.nii.gz' provided with ROI masks of tumor region, BPH, and healthy peripheral zone (PZ) region named as 'tumor_ROI.nii.gz', 'bph_roi.nii.gz', and pz_roi.nii.gz respectively. All the images and ROIs are in compressed nii format.


3. **[IVIM_DKI_functions](https://github.com/amitvmehndiratta/IVIM-DKI-MRMP2021/tree/main/IVIM_DKI_functions)**: MATLAB functions to compute IVIM-DKI parameter maps obtained from novel IVIM-DKI model with TV and other utilities. 

   -'[hyModelTV.m](https://github.com/amitvmehndiratta/IVIM-DKI-MRMP2021/blob/main/IVIM_DKI_functions/hyModelTV.m)': Executes IVIM-DKI model with TV code using non-linear least square optimization with iterative total variation (TV) penalty function to evaluate IVIM-DKI parameter reconstruction.
    
        -----------------------------------------------------------------------------------------------
        function [paraMap,resnorm] = hyModel (dwi,b,limit,initials,tvIter,alpha,beta)
        -----------------------------------------------------------------------------------------------
        Input:
        dwi =     4D DWI data, MxNxSxB format where M and N are x and y, S is number of slices, 
                  and B is number of b-values 
        b =       b-values, must be a row matrix
        limit =   2x4 matrix with lower (1st row) and upper (2nd row) 
                  limits of all parameters in the order D, D*, f, and k
        initial = 1x4 matrix with initial values of all parameters 
                  in the order D, D*, f, and k
        tvIter =  Define the number of TV iteration to be performed
        alpha =   Alpha is a small positive constant, range from 0 to 1
        beta =   Beta is a relaxation parameter, range from 0 to 1

        Output:
        paraMap =   IVIM-DKI parameters are saved as struct in the order D, D*, f, and k
        resnorm =   Voxelwise squared norm of the residual

  
   -'allivimdki.m': Function which contains IVIM-DKI model equation.
  
   -'[im2Y.m](https://www.mathworks.com/matlabcentral/fileexchange/65579-ivim-model-fitting)': Transforms functional image data (4D or 3D array) into data matrix VxM where V is the number of voxels and M is number of b-values. Adapted function from https://www.mathworks.com/matlabcentral/fileexchange/65579-ivim-model-fitting.
  
   - parsave_tv: For saving parfor function variables.
   
   -'stats_roi.m': Calculates mean and standard deviation of IVIM-DKI parameters for ROI specified.
        
        -----------------------------------------------------------------------------
        function[mean_roi, std_roi] = stats_roi(parameterMap,roi,stats)
        -----------------------------------------------------------------------------
        Input:
        paraMap =   IVIM-DKI parameters saved as struct in the order D, D*, f, and k 
                    (output generated from hyModelTV.m)
        roi =       ROI mask in 2D or 3D logical matrix format

        Output:
        mean_roi = Average of IVIM-DKI parameters for ROI specified and 
                   are saved as struct in the order D, D*, f, and k
        std_roi = Standard deviation of IVIM-DKI parameters for ROI specified and 
                   are saved as struct in the order D, D*, f, and k
  
  

  -'tv3d.m': Function which calculates 3D TV penalty. Please see ref. [[1]](https://link.springer.com/article/10.1007/s10334-021-00932-1) and [[2]](https://aapm.onlinelibrary.wiley.com/doi/abs/10.1002/mp.12520) for more details on the implementation of TV function.


If you use toolbox or functions in research, please cite:

[Malagi, A. V. et al. (2021). IVIM-DKI differentiation between prostate cancer and benign prostatic hyperplasia: comparison of 1.5T vs. 3T MRI. 
Magnetic Resonance Materials in Physics, Biology and Medicine.
DOI: 10.1007/s10334-021-00932-1](https://link.springer.com/article/10.1007/s10334-021-00932-1)
