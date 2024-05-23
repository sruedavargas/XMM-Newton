# XMM-Newton

Scripts to handle XMM Newton data with SAS.

Order to run the scripts:
1. Reduction
2. GTI_binning (all observations at once) or  gti_binning_single (for a single GTI table)
3. Spectra extraction and grouping
4. Sort_mult_object (when processing multiple sources at once)
5. Spectra_fitting_object (all observations for the object) or spectra_fitting_sing_obs (one single observation and one bin)

Description:

- The reduction script takes the path where the raw data from XSA are stored (either for a single observation or multiple observations with different observation id) and the working directory where products are saved. The final products are "cleaned" photon event tables and images. Subproducts include housekeeping files, light curves, GTI tables, and so on, for each EPIC camera and two threshold values for the background count rates (conservative and relaxed)
- The GTI binning script uses the initially created GTI tables for PN and bins the data in bins of a given length (5 ks, 10 ks, etc).
- After running the GTI binning script and before running the Spectra extraction script, it is necessary to create the region files for each observation. The files need to be named '{observation_id}_{camera}_{reg}.txt'. The file needs to contain the source regions and the background regions labeled in ds9 as #background. For each observation, the region file for PN and MOS needs to be created (MOS1 and MOS2 use the same region file). The region files need to be located in the spectra_files folder (see example of files)
- The spectra extraction takes as input the working directory. The script extracts the average spectra for each camera in an observation. It uses the corresponding PN table for each observation. It also extracts one single spectrum for each bin created. Both types of spectra (average and single) are grouped in bins of 20 photons.
- The Sorting script takes all the products created for all the observations, and sorts every file in different folders, depending on the object. One single folder is created per object. This script needs a .csv file called "sources_obs_id.csv" with the name of the sources and their corresponding observations id (see example of .ods file that needs to be saved as .csv file)
- The spectra fitting script needs the model and initial parameters for an average spectrum. It fits those spectra, finds the best-fit values, and uses them to fit the single spectra in that observation. The fit for every bin is done by unfreezing N_h and the normalization for the power-law parameters first, and then unfreezing gamma too. This script needs a .csv file called "energies_epatplot.csv" (see example) with the energy ranges to use for each observation and camera. 
