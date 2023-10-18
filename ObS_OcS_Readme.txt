ImageJ macro for automated analysis of Ob.S./B.S. and Oc.S./B.S.

REQUIREMENTS: 

VERSION: ImageJ  v1.54f or later (not tested for earlier versions)

DIRECTORY: Must contain the image to be analyzed and the corresponding RoiSet.zip file. 

IMAGE FILE: 16 bit tiff image, 3 channels (Ctsk in channel 1, Col1a1 in channel 2, DAPI in channel 3), pixel scale defined in micrometers (use Analyze/Set Scale menu option to verify correct scaling of the image). Additional image channels (e.g., transmission image used for visualizing bone surfaces) must be removed before the analysis. To speed up analysis, the image should be cropped to retain only the trabecular region of interest (ROI) for the analysis. 

ROISET.ZIP FILE: The file defining bone surfaces in the image. RoiSet.zip must be saved from ImageJ ROI manager. Bone surfaces must be drawn with the “Segmented Line” tool of ImageJ. At least 2 segmented lines must be defined. Several segmented lines can be used to define the surface of a single trabeculae, yet excessive splitting into multiple segmented lines may result in accumulating “edge effects”. All segmented lines defining bone surfaces within the image must be saved into a single RoiSet.zip file.

PARAMETERS:

Initial Col threshold: seeding value for Col1a1 thresholding. The final value is calculated iteratively and should be independent of the seeding value. A value ~ 20% of maximum Col1a1 intensity is recommended.

Initial Ctsk threshold: seeding value for Ctsk thresholding (similar to Col1a1 thresholding).

Col1a1 threshold ratio, ThrRCol: Dynamic range for Ob Col1a1 intensities in the sample. The lower threshold for Col1a1 intensity ColT is calculated iteratively until % of the area with intensity >ColT*ThrRCol relative to the area with intensity >ColT reaches the specified value %Area. For samples with low background and large dynamic range of Col1a1, ThrRCol=5 is recommended. For samples with higher background and lower dynamic range, ThrRCol may be reduced to ensure convergence of the calculation. ThrRCol<3 is not recommended. The value of ThrRCol must be the same for all samples that are compared to each other.

Ctsk threshold ratio, ThrRCtsk: Similar to ThrRCol.

Maximum %Area at upper threshold: %Area used for threshold calculations. Default %Area = 5 is recommended. %Area may be increased for samples with lower dynamic range and a significant fraction of oversaturated pixels. The value of %Area must be the same for all samples that are compared to each other.

Minimum cell size, Msize: Only spots larger than Msize are counted as cells.

Line width: Distance from bone surface within which Col1a1 and Ctsk positive areas are counted as osteoblasts (Ob) and osteoclasts (Oc), respectively. 

OUTPUT FILES:

*_Col_16bit.tif: Col1a1 channel of the original image.
*_Ctsk_16bit.tif: Ctsk channel of the original image.
_ColM_XXXXt.tif: Mask of the signal identified as Ob signal, XXXX is the Col1a1 threshold.
_CtskM_XXXXt.tif: Mask of the signal identified as Oc signal, XXXX is the Ctsk threshold.
Auto_Thr.txt: Results of the image analysis

AUTO_THR.TXT FILE

ColT/GFPT0 and CtskT/CTSKT0 values: parameters used for monitoring convergence of Col1a1 and Ctsk threshold calculation (converge to 1 with 0.001 tolerance)

ColAT/ColA and CtskAT/CtskA values; parameters used for monitoring performance of threshold calculations (should be =%Area/100 with 0.0001 tolerance)

Pixel size (um),  % Area, Col1a1 threshold ratio, Ctsk threshold ratio

Calculation results: Col1a1 threshold, Ctsk threshold, Bone Perimeter (um), Ob-Bone Contact perimeter (um), Oc-Bone Contact perimeter. 
