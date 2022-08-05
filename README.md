A package providing MATLAB programming tools and GUI for IVIM-DKI analysis 
with total variation (TV) penalty function.

Disclaimer: This toolbox can be used only for research or non-commercial 
purposes. Authors are not liable for any clinical use of it, authors could 
not be held responsible.
If you have any queries or suggestions about this package, kindly contact 
Dr. Amit Mehndiratta, Indian Institute of Technology Delhi, India.
E-mail: amehndiratta@cbme.iitd.ac.in, amit.mehndiratta@keble.oxon.org.

Built on code by: @archanamalagi

If you use this toolbox, please cite:
[1] Malagi, A. V. et al. (2021). IVIM-DKI differentiation between prostate 
cancer and benign prostatic hyperplasia: comparison of 1.5T vs. 3T MRI. 
Magnetic Resonance Materials in Physics, Biology and Medicine. 
DOI : 10.1007/s10334-021-00932-1
[2] Kayal, E. B. et al. (2017). Quantitative analysis of intravoxel 
incoherent motion (IVIM) diffusion MRI using total variation and Huber
 penalty function. Medical physics, 44(11), 5849-5858.

How to use ivimDKI3Dtvtool:
ivimDKI3Dtvtool_v1_4 execute IVIM-DKI analysis with TV, consisting of three tabs:
Input Data and Analysis, where user needs to select IVIM-DKI data and define 
parameters; these inputs are fed to IVIM-DKI model with TV after clicking on 
'Run', and analysis can also be initiated with default parameters defined in 
the app.
Output tab, where IVIM-DKI parameter maps can be viewed in different colormaps 
and saved as nii format. 
ROI statistics in this tab, where ROI can be loaded and statistics can also be 
performed after clicking on 'Calculate ROI stats and Save statistics'; where, 
mean, standard deviation, skewness, kurtosis, entropy, and energy of IVIM-DKI 
parameters are calculated, which is displayed on app and saved as .xlsx file 
for the ROI provided.

ivimDKItvtool tabs:
-Input Data and Analysis display

-Output tab
 
-ROI statistics
 
