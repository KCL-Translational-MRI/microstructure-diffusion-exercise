# Diffusion Microstructure Exercise
This is an exercise in estimating microstructural tissue parameters from *ex vivo* diffusion data using the **Histo-μSim** framework.

## Background
Diffusion-weighting in MR images is typically obtained by inserting a pair of diffusion-sensitizing gradients into a spin echo sequence, as shown below.

![Example diffusion sequence](/example_images/ex_dwi_sequence.png "Example diffusion sequence") 

The amount of diffusion-weighting, commonly referred to as the *b*-value, is dependent on the sequence parameters, and given by this equation:

$$ b=(\Delta-\delta/3)(\gamma\delta G)^2 $$

where
- $\delta$ is the gradient duration
- $\Delta$ is the gradient separation, or diffusion time
- $G$ is the amplitude of the diffusion-sensitizing gradients
- $\gamma$ is the proton gyromagnetic ratio 

ADD MORE EXPLANATION 

## Setting Up
Your task is to use the data provided in `data/` and **Histo-μSim** to generate maps of microstructural tissue parameters.

You should follow the [tutorial instructions](https://github.com/radiomicsgroup/dMRIMC/tree/2ff4abe7b9cd4a8f6e4c9ea9b1f7f990ae57143d#example-lets-try-histo-%CE%BCsim-on-some-data) in the **Histo-μSim** repository, replacing the example data with that from the `data/` folder.

### Installation

Clone this repository into a location of your choice:

```
git clone https://github.com/KCL-Translational-MRI/microstructure-diffusion-exercise.git 
```

You will also need the [**Histo-μSim** repository](https://github.com/radiomicsgroup/dMRIMC), which is included as a submodule in this repository, and you will need to install the dependencies. An [environment.yml](https://github.com/KCL-Translational-MRI/microstructure-diffusion-exercise/blob/main/environment.yml) is provided with the required dependencies.

The **Histo-μSim** repository can be cloned with:

```
git submodule init
git submodule update
```

A conda enviornment called `histomusim` can be created with:

```
conda create --file environment.yml
conda activate histomusim
```

You should now be able to run the Python and Shell scripts in `dMRIMC/`.

### Provided Data
The `data/` folder contains the following data, taken from an *ex vivo* mouse liver imaging dataset:

- `dwi_data_sphmean.nii` The diffusion MRI data. This file contains a single slice (a 2D image) with 13 volumes (images), which consist of a *b*=0 image, and 12 diffusion-weighted images, acquired with different *b*-values and diffusion times Δ. The data have already been averaged across diffusion-encoding directions, and denoised using MP-PCA.
- `dwi_noise.nii` A map of estimated noise, derived from the MP-PCA denoising. This file is a single 2D volume.
- `dwi_mask.nii` A binary mask of the liver tissue. This file is a single 2D volume.
- `dwi_data.bval` A plain text file listing the *b*-values (diffusion weightings) of the volumes in `dwi_data_sphmean.nii`
- `dwi_data.gdur` A plain text file listing the gradient durations δ of the volumes in `dwi_data_sphmean.nii` (note that in this dataset, all volumes were acquired with the same δ)
- `dwi_data.gsep` A plain text file listing the diffusion times (gradient separations, Δ) of the volumes in `dwi_data_sphmean.nii`

## The Task

Complete the following tasks. Save the resulting images in a Word document (or equivalent) along with your responses to the questions.

### 1. Visualizing the Data

Use MATLAB, `matplotlib`, or a NIFTI image viewing tool to visualize the diffusion-weighted images contained in `dwi_data_sphmean.nii`. 

Display the *b*=0 images and one of the *b*=1500 images (*HINT: look at* `dwi_data.bval` *to see the b-values of each of the volumes in the data.*). Ensure that the same colour-axis limits are applied to both images, so that the difference in signal between *b*=0 and *b*=1500 can be seen. An example image is shown below.

![Example diffusion-weighted images](/example_images/ex_dwi_images.png "Example diffusion-weighted images")

### 2. Running Histo-μSim
Follow the [**Histo-μSim** tutorial instructions](https://github.com/radiomicsgroup/dMRIMC/tree/2ff4abe7b9cd4a8f6e4c9ea9b1f7f990ae57143d#example-lets-try-histo-%CE%BCsim-on-some-data) two generate parameter maps for 5 microstructural parameters:  `fin`, `vCS_cyl`, `D0in`, `D0ex`, and `kappa`.

Display images of the  intracellular volume fraction (`fin`) and volume-weighted cell size (`vCS_cyl`).

### 3. Running Histo-μSim with fixed parameters
Use **Histo-μSim** again on the same data, but this time, generate parameter maps for only 3 microstructural parameters:  `fin`, `vCS_cyl`, and `D0ex`. The other parameters should be assigned to fixed values:  `D0in=1.35` and `kappa=20` (*HINT: Make sure that you save these results under a different protocol name*)

As before, display images of the  intracellular volume fraction (`fin`) and volume-weighted cell size (`vCS_cyl`).

> Do you notice any differences in the intracellular volume fraction or cell size maps between the two inference methods?

### 4. Regularization
The dictionary matching procedure (`mri2micro_dictml.py`) uses spatial regularization of the parameter maps, by default, to constrain values and reduce noise in the results.

Run the *fixed parameter* analysis again:
1. With no regularization in `mri2micro_dictml.py`
2. With stronger regularization than the default (e.g. λ=0.02)

> Describe the effect that regularization has on the parameter maps. You may want to look particularly at `D0ex`.

### 5. Generative AI Use
If you used generative AI tools in completing any of these tasks, please describe which tools you used, and how you used them. 
