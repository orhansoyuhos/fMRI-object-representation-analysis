# fMRI Object Representation Analysis

In this project, I investigated whether the patterns of brain activity for lookalike objects generalize to their corresponding animate objects or object identities in three regions of interest (ROIs): primary visual cortex (V1), anterior ventral temporal cortex (VTC-ant), and posterior ventral temporal cortex (VTC-post). Using One-vs-One multiclass decoding, I trained classifiers on fMRI data evoked by lookalike objects and tested them on fMRI data elicited by animate and inanimate objects. The results showed that the patterns of BOLD activity for lookalike objects generalized to matching animate objects in VTC-ant and VTC-post, but not in V1. Additionally, the activity patterns for lookalike objects yielded significant accuracy when classifying inanimate objects in all three ROIs.

Furthermore, I used representational similarity analysis (RSA) to evaluate the object space organization in the three ROIs based on object appearance and animacy. The results indicated that both visual appearance and animacy properties drove object space organization in VTC-ant, while only information related to visual appearance was encoded in VTC-post.

## Dataset of images shown during fMRI

<img width="1126" alt="226024705-cd1937ae-74cd-4970-93e3-a0e81eff278f" src="https://user-images.githubusercontent.com/44211738/229634243-54644aa8-ab27-4a4e-b028-410843da35e8.png">

## Repository Structure

```
├── Classification/
│   ├── scripts/
│   │   ├── MAIN_script.m          — top-level runner for the decoding analysis
│   │   ├── load_path.m            — path configuration (edit before running)
│   │   ├── multiclass_decoding.m  — OVO LDA decoding across subjects and ROIs
│   │   ├── test_significance.m    — one-tailed one-sample t-tests against chance
│   │   └── visualize_results.m    — bar plots with SEM error bars
│   └── figures/
└── Representational Similarity Analysis/
    ├── scripts/
    │   ├── MAIN_script.m           — top-level runner for the RSA analysis
    │   ├── load_path.m             — path configuration (edit before running)
    │   ├── generate_models.m       — constructs theoretical RDM models (H1 and H2)
    │   ├── save_subsDS.m           — builds CoSMoMVPA dataset structures per subject/ROI
    │   ├── save_RDMs.m             — computes and saves RDMs per subject and ROI
    │   ├── save_lowerModelsVect.m  — extracts lower triangles of model RDMs
    │   ├── compute_RSA.m           — partial correlation, Fisher transform, t-test, noise ceiling
    │   ├── visualize_results.m     — plots averaged RDMs and RSA bar charts
    │   └── print_statistics.m      — prints and saves significance tables
    └── figures/
```

## Dependencies

- [MATLAB](https://www.mathworks.com/products/matlab.html)
- [CoSMoMVPA](https://www.cosmomvpa.org/) — used for dataset construction, decoding, and dissimilarity matrix computation
- [SPM](https://www.fil.ion.ucl.ac.uk/spm/) — fMRI data is loaded via `SPM.mat` files

## How to Run

1. Update the paths in `load_path.m` (found in both `Classification/scripts/` and `Representational Similarity Analysis/scripts/`) to match your local directory structure — including the CoSMoMVPA installation path, fMRI data location, and ROI masks.

2. Add CoSMoMVPA to your MATLAB path (handled automatically by `MAIN_script.m` via `addpath`).

3. Run `MAIN_script.m` in the desired analysis folder from MATLAB.

> **Note:** The fMRI data used in this project is not included in this repository. The scripts expect subject data folders (`SUB01` through `SUB12`) each containing an `SPM.mat` file, along with ROI mask files (`V1.nii`, `VTC_ant.nii`, `VTC_post.nii`).

## Results

- Representational dissimilarity matrices:
![ROIs_across_subjects](https://user-images.githubusercontent.com/44211738/159066116-370de2c4-126c-4216-81bb-9dec307662a4.png)

- Representational similarity analysis:
![RSA Between Models and ROIs](https://user-images.githubusercontent.com/44211738/159066126-8acdc190-24d7-4d0f-a560-29642b8ce1a9.png)

## Acknowledgement
- Thank you Dr. Stefania Bracci, Dr. Moritz Wurm, and Dr. Scott L. Fairhall for this great course!
