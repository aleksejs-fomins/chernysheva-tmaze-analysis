This repository contains the codes used for behavioural, photometric and post-hoc statistical analyses of the paper [Wilhelm, Sych et al. NatComm 2023](https://doi.org/10.1101/2021.12.03.471159). The below analyses were performed by different collaborators and written in different programming languages. Please consult the corresponding description below to learn how to use the specific parts of the code.

# 1. Photometry Analysis (M. Wilhelm)

Folder "matlab_scripts_photometry_analysis" contains the functions for analysis of the recorded photometry signals. We used the same algorithms for calculating the resampled z-scored dFF (utilities), but structured these functions by the signal type/ figures it relates to.
* “averaging_whole_session_photometry” is used to calculate the dFF signal and average it across trials and mice (Fig2a)
* “averaging_maintanance_photometry” is focused on calculating the dFF signal during the maintenance period and averaging it across trials and mice (Fig2c, SFig3a-d)
* “averaging_photometry_470_and_425” is used for Sfig2b
* “averaging_whole_session_photometry_pharma” is used for Fig4a and SFig5a allowing to compare the Cmpd and vehicle signals
* “averaging_maintanance_miniscope” and “averaging_whole_session_miniscope”
are used for SFig8

Consult the file "Readme.docx" for further instructions.

# 2. Behavioural Analysis (Y. Sych)

Folder "matlab_scripts_behavioral_analysis" contains primarily behavioral analysis. It aims to quantify the existence of biases in motor behaviors, as well as inspect whether different motor behaviors elicited different activity profiles on photometry data. The code is organized as follows

* utilities: functions allowing for calculating
    * zscore.m
    * shadedErrorBar.m
    * barwitherr.m
* libraries: inpaint_nans and dowload [u-map Version 4.4](https://ch.mathworks.com/matlabcentral/fileexchange/71902-uniform-manifold-approximation-and-projection-umap?s_tid=mwa_osa_a)
* read_dlc_coordinates.m and read_dlc_coordinates_opto_perturb.m , read csv files generated by the DeepLabCut model tracking animal behavior. The program calculates behavioral parameters from selected types of trials (e.g., when trials with Correct Left or Correct Right turn at the T-junction should be compared). The program structures the data (concatenated behavioral parameters are referred to as behavioral model), u-map low dimensional embedding is performed to simplify high-dimensional behavioral data into 2D space, followed by subsequent k-means clustering. Clusters represent trials with similar behavioral parameters that are labeled and analyzed together, for example to show that dF/F calcium signals are not affected by motor behavior.
* plot_compare_by_mouse.m uses pooled data from read_dlc_coordinates.m and compares behaviors separately within each mouse to demonstrate that during the maintenance (delay) period in the T-maze mice have no preference in the orientation or the direction of turns.
* pool_behavioral_clusters_photometry.m similarly to read_dlc_coordinates.m does u-map low dimensional embedding to simplify high-dimensional behavioral data into 2D space. Low dimensional space is plotted across trials and across mice.

Consult the file "Behavioral data analysis.docx" for further details.

# 3. Post-hoc statistical analysis (A. Fomins)

The below code performs the exploratory study of advanced statistical questions, such as cell-specific differences across periods and phases, direction and performance discrimination, clustering, and temporal orderability of cells.

# 4. T-Maze Controls (J.S.L. Warren)

Folder "t_maze_control" contains custom-written Matlab scripts enabling the control of the automated T-maze apparatus. wxguitmaze is the main program running the automated maze. The rest of the functions support hardware initialization, detection of the mouse and recording of the data.

## Installation instructions

Language: Python 3 (tested on 3.6, 3.8)

1. pip install -e .
2. pip install -r requirements.txt
3. Install in-house library [mesostat](https://github.com/HelmchenLabSoftware/mesostat-dev) and its dependencies

##  Structure

The front end of the code is contained in 6 jupyter notebooks inside the "pfc_mem_proj" folder

* "maria-analysis-1-explore.ipynb" - Visualization of raw data

* "maria-analysis-2-phases-and-intervals.ipynb" - Comparative analysis of task phases

* "maria-analysis-3-LR-CM.ipynb" - Statistical testing of differences between Left/Right turns and Correct/Mistake performance.

* "maria-analysis-4-trajectories-clustering.ipynb" - Study of neuronal trajectories in dimensionality-reduced manifolds, as well as activity clustering

* "maria-analysis-5-temporal-order.ipynb" - Study of within-period temporal orderability of neurons

* "maria-analysis-6-LR-CM-classification.ipynb" - Machine learning approach to classification of Left/Right turns and Correct/Mistake performance.

## Usage
Each cell of each notebook computes a specific plot or a statistical result. Cells are labeled for clarity. The 2nd cell in each notebook contains paths to raw data (dff) and deconvolved data (deconv). These paths are absolute, and need to be adjusted by the user. Each path points to the root folder of the corresponding dataset.
