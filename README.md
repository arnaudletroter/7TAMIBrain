# 7TAMIBrain

if you use it, please cite the paper:
Brun, G., Testud, B., Girard, O. M., Lehmann, P., de Rochefort, L., Besson, P., Massire, A., Ridley, B., Girard, N., Guye, M., Ranjeva, J.-P., & Le Troter, A. (2022). Automatic segmentation of deep grey nuclei using a high-resolution 7T magnetic resonance imaging atlas—Quantification of T1 values in healthy volunteers. European Journal of Neuroscience, 1–23. https://doi.org/10.1111/ejn.15575

Data/code availability statement:

The full 7TAMIbrain [Girard et al., 2021] dataset (BIDS formatted) is publicly available on the OpenNeuro platform (Dataset ds003967)

![Viewer fsleyes](fsleyes_view.png?raw=true "FSLEYES")


**How to use (command lines using ants Library):
**


**Registration qT1 (7TAMIbrain template) to qT1 map (subject):
**

antsRegistrationSyN.sh -d 3 -m 7TAMI_qT1_100.nii.gz -f T1map_subj.nii.gz -o 7TAMI_2_subject_SyN

**Warp 7TAMIbrain atlas to subject space:_
**

antsApplyTransforms -d 3 -e 0 -i 7TAMI_DGN.nii.gz -r T1map_subj.nii.gz -o DGN_mask_subj.nii.gz -t 7TAMI_2_subject_SyN1Warp.nii.gz -t 7TAMI_2_subject_SyN0GenericAffine.mat -n NearestNeighbor


**Visual check:
**

install look up table for fsleyes:
_cp -rf 7TAMI_DGN_fsleyes.lut $HOME/.fsleyes/luts/
_

fsleyes --scene ortho --displaySpace T1map_subj.nii.gz --xcentre  0.00000  0.00000 --ycentre  0.00000  0.00000 --zcentre  0.00000  0.00000 --xzoom 100.0 --yzoom 100.0 --zzoom 100.0 --layout horizontal --movieSync T1map_subj.nii.gz --name "T1map_subj" --overlayType volume --alpha 100.0 --brightness 50 --contrast 50 --cmap greyscale --negativeCmap greyscale --displayRange 500 4096 --clippingRange 0 4096 --gamma 0.0 --cmapResolution 256 --interpolation none --numSteps 100 --blendFactor 0.1 --smoothing 0 --resolution 100 --numInnerSteps 10 --clipMode intersection --volume 0 DGN_mask_subj.nii.gz --name "DGN_mask_subj" --overlayType label --alpha 100.0 --brightness 50.0 --contrast 50.0 --lut 7tami_dgn_fsleyes --outline --outlineWidth 2 --volume 0

