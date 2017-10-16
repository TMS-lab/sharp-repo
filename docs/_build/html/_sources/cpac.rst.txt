C-PAC BIDS Application for SHARP data
==============

## Documentation
Extensive information can be found in the [C-PAC User Guide](http://fcp-indi.github.com/docs/user/index.html). 

## Description
The Configurable Pipeline for the Analysis of Connectomes [C-PAC](http://fcp-indi.github.io) is a software for
performing high-throughput preprocessing and analysis of functional connectomes data using high-performance computers.
C-PAC is implemented in Python using the Nipype pipelining [[1](#nipype)] library to efficiently combine tools from AFNI
[[2](#afni)], ANTS [[3](#ants)], and FSL [[4](#fsl)] to achieve high quality and robust automated processing. This
docker container, when built, is an application for performing participant level analyses. Future releases will include
group-level analyses, when there is a BIDS standard for handling derivatives and group models.

## SHARP Data



Several different individual level analysis are performed on the fMRI data including:

- **Amplitude of low frequency fluctuations (alff) [[10](#alff)]**: the variance of each voxel is calculated after
bandpass filtering in original space and subsequently written into MNI space at 2mm resolution and spatially smoothed
using a 6mm FWHM kernel.
- **Fractional amplitude of low frequency fluctuations (falff) [[11](#falff)]**: Similar to alff except that the
variance of the bandpassed signal is divided by the total variance (variance of non-bandpassed signal.
- **Regional homogeniety (ReHo) [[12](#reho)]**: a simultaneous Kendalls correlation is calculated between each
voxel's time course and the time courses of the 27 voxels that are face, edge, and corner touching the voxel. ReHo is
calculated in original space and subsequently written into MNI space at 2mm resolution and spatially smoothed using
a 6mm FWHM kernel.
- **Voxel mirrored homotopic connectivity (VMHC) [[13](#vmhc)]**: an non-linear transform is calculated between the
skull-on anatomical data and a symmetric brain template in 2mm space. Using this transform, processed fMRI data are
written in to symmetric MNI space at 2mm and the correlation between each voxel and its analog in the contralateral
hemisphere is calculated. The Fisher transform is applied to the resulting values, which are then spatially smoothed
using a 6mm FWHM kernel.
- **Weighted and binarized degree centrality (DC) [[14](#degree)]**: fMRI data is written into MNI space at 2mm
resolution and spatially smoothed using a 6mm FWHM kernel. The voxel x voxel similarity matrix is calculated by the
correlation between every pair of voxel time courses and then thresholded so that only the top 5% of correlations
remain. For each voxel, binarized DC is the number of connections that remain for the voxel after thresholding and
weighted DC is the average correlation coefficient across the remaining connections.
- **Eigenvector centrality (EC) [[15](#eigen)]**: fMRI data is written into MNI space at 2mm resolution and spatially
smoothed using a 6mm FWHM kernel. The voxel x voxel similarity matrix is calculated by the correlation between every
pair of voxel time courses and then thresholded so that only the top 5% of correlations remain. Weighted EC is
calculated from the eigenvector corresponding to the largest eigenvalue from an eigenvector decomposition of the
resulting similarity. Binarized EC, is the first eigenvector of the similarity matrix after setting the non-zero values
in the resulting matrix are set to 1.
- **Local functional connectivity density (lFCD) [[16](#lfcd)]**: fMRI data is written into MNI space at 2mm resolution
and spatially smoothed using a 6mm FWHM kernel. For each voxel, lFCD corresponds to the number of contiguous voxels that
are correlated with the voxel above 0.6 (r>0.6). This is similar to degree centrality, except only voxels that it only
includes the voxels that are directly connected to the seed voxel.
- **10 intrinsic connectivity networks (ICNs) from dual regression [[17](#dr)]**: a template including 10 ICNs from a
meta-analysis of resting state and task fMRI data [[18](#icn10)] is spatially regressed against the processed fMRI data
in MNI space. The resulting time courses are entered into a multiple regression with the voxel data in original space to
calculate individual representations of the 10 ICNs. The resulting networks are written into MNI space at 2mm and then
spatially smoothed using a 6mm FWHM kernel.
- **Seed correlation analysis (SCA)**: preprocessed fMRI data is to match template that includes 160 regions of interest
defined from a meta-analysis of different task results [[19](#do160)]. A time series is calculated for each region from
the mean of all intra-ROI voxel time series. A seperate functional connectivity map is calculated per ROI by correlating
its time course with the time courses of every other voxel in the brain. Resulting values are Fisher transformed,
written into MNI space at 2mm resolution, and then spatiall smoothed using a 6mm FWHM kernel.
- **Time series extraction**: similar the procedure used for time series analysis, the preprocessed functional data is
written into MNI space at 2mm and then time series for the various atlases are extracted by averaging within region
voxel time courses. This procedure was used to generate summary time series for the automated anatomic labelling atlas
[[20](#aal)], Eickhoff-Zilles atlas [[21](#ez)], Harvard-Oxford atlas [[22](#ho)], Talaraich and Tournoux atlas
[[23](#tt)], 200 and 400 regions from the spatially constrained clustering voxel timeseries [[24](#cc)], and 160 ROIs
from a meta-analysis of task results [[19](#do160)]. Time series for 10 ICNs were extracted using spatial regression.
