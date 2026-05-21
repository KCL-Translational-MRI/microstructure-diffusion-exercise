# Diffusion Microstructure Exercise
This is an exercise in estimating microstructural tissue parameters from *ex vivo* diffusion data using the **Histo-μSim** framework.

## Background
This will be filled in later with some theory about diffusion MRI and microstructure.

## The Task
Your task is to use the data provided in `data/` and **Histo-μSim** to generate maps of microstructural tissue parameters.

You should follow the [tutorial instructions](https://github.com/radiomicsgroup/dMRIMC/tree/2ff4abe7b9cd4a8f6e4c9ea9b1f7f990ae57143d#example-lets-try-histo-%CE%BCsim-on-some-data) in the **Histo-μSim** repository, replacing the example data with that from the `data/` folder.

### 1. Installation
You will need to clone the [**Histo-μSim** repository](https://github.com/radiomicsgroup/dMRIMC), which is also included as a submodule in this repository, and install the dependencies. An [environment.yml](https://github.com/KCL-Translational-MRI/microstructure-diffusion-exercise/blob/main/environment.yml) is provided with the required dependencies.

A conda enviornment called `histomusim` can be created with:

```
conda create --file environment.yml
conda activate histomusim
```

The **Histo-μSim** repository can be cloned with:

```
git submodule init
git submodule update
```

You should now be able to run the Python and Shell scripts in `dMRIMC/`.

### 2. Provided Data
The `data/` folder contains the following data, taken from an *ex vivo* mouse liver imaging dataset:

- `dwi_data_sphmean.nii` The diffusion MRI data. This file contains a single slice (a 2D image) with 13 volumes (images), which consist of a *b*=0 image, and 12 diffusion-weighted images, acquired with different *b*-values and diffusion times Δ. The data have already been averaged across diffusion-encoding directions, and denoised using MP-PCA.
- `dwi_noise.nii` A map of estimated noise, derived from the MP-PCA denoising. This file is a single 2D volume.
- `dwi_mask.nii` A binary mask of the liver tissue. This file is a single 2D volume.
- `dwi_data.bval` A plain text file listing the *b*-values (diffusion weightings) of the volumes in `dwi_data_sphmean.nii`
- `dwi_data.gdur` A plain text file listing the gradient durations δ of the volumes in `dwi_data_sphmean.nii` (note that in this dataset, all volumes were acquired with the same δ)
- `dwi_data.gsep` A plain text file listing the diffusion times (gradient separations, Δ) of the volumes in `dwi_data_sphmean.nii`

### 3. Running Histo-μSim
Follow the [**Histo-μSim** tutorial instructions](https://github.com/radiomicsgroup/dMRIMC/tree/2ff4abe7b9cd4a8f6e4c9ea9b1f7f990ae57143d#example-lets-try-histo-%CE%BCsim-on-some-data) two generate two sets of microstructure parameter estimates

1. Estimating 5 microstructural parameters: `fin`, `vCS_cyl`, `D0in`, `D0ex`, and `kappa`
2. Estimating 3 microstructural parameters:  `fin`, `vCS_cyl`, and `D0ex`, with the others assigned to fixed values: `D0in=1.35` and `kappa=20`

### 4. Results 
Use MATLAB, `matplotlib`, or a NIFTI image viewing tool to visualize the parameter maps. Save images of the intracellular volume fraction (`fin`) and volume-weighted cell size (`vCS_cyl`) for both sets of parameter estimates.


