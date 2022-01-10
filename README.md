# 7TAMIBrain

**A High-Resolution and High-Constrast 7T MRI template to segment Deep Grey Nuclei (on MP2rage T1map).**

The 7TAMIbrain dataset [Girard et al., 2021] (BIDS formatted, 60 qT1 MRI anonymized and cropped + DGN mask of segmentation) is publicly available on the OpenNeuro platform (Dataset ds003967, https://openneuro.org/datasets/ds003967/versions/1.0.0)

# How to use (command lines using ants Library)

**Registration qT1 (7TAMIbrain template) to qT1 map (subject):**

antsRegistrationSyN.sh -d 3 -m 7TAMI_qT1_100.nii.gz -f T1map_subj.nii.gz -o 7TAMI_2_subject_SyN

**Warp 7TAMIbrain atlas to subject space:**

antsApplyTransforms -d 3 -e 0 -i 7TAMI_DGN.nii.gz -r T1map_subj.nii.gz -o DGN_mask_subj.nii.gz -t 7TAMI_2_subject_SyN1Warp.nii.gz -t 7TAMI_2_subject_SyN0GenericAffine.mat -n NearestNeighbor

**Visual check with fsleyes:**

*Add look up table (lut) for fsleyes:*
cp -rf 7TAMI_DGN_fsleyes.lut $HOME/.fsleyes/luts/

fsleyes --scene ortho --displaySpace T1map_subj.nii.gz --movieSync T1map_subj.nii.gz --name "T1map_subj" --overlayType volume --alpha 100.0 --brightness 50 --contrast 50 --cmap greyscale --negativeCmap greyscale --displayRange 500 4096 --clippingRange 0 4096 --volume 0 DGN_mask_subj.nii.gz --name "DGN_mask_subj" --overlayType label --lut 7tami_dgn_fsleyes --outline --outlineWidth 2 --volume 0

![Viewer fsleyes](fsleyes_view.png?raw=true "FSLEYES")

# if you use it, please cite the paper:
Brun, G., Testud, B., Girard, O. M., Lehmann, P., de Rochefort, L., Besson, P., Massire, A., Ridley, B., Girard, N., Guye, M., Ranjeva, J.-P., & Le Troter, A. (2022). Automatic segmentation of deep grey nuclei using a high-resolution 7T magnetic resonance imaging atlas—Quantification of T1 values in healthy volunteers. European Journal of Neuroscience, 1–23. https://doi.org/10.1111/ejn.15575
