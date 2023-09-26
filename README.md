# XMM-Newton

Scripts to handle XMM Newton data with SAS.

- The reduction script takes the path where the raw data from XSA are stored (either for a single observation or multiple observations with different observation id). The final products are "cleaned" photon event tables and images. Subproducts include housekeeping files, light curves, GTI tables, and so on, for each EPIC camera and two threshold values for the backgroun count rates (conservative and relaxed)
- 
- The GTI binning script uses the initially created GTI tables for PN and bins the data in bins of given length (5 ks, 10 ks, etc). The resulting binned GTI table for PN is used to create a binned GTI table for MOS1 and MOS2 with the same intervals.
- The spectra extraction script extracts the average spectra for each camera in an observation. It also extract one single spectra for each bin created. Both types of spectra (average and single) are grouped in bins of 20 photons.
- The spectra fitting script needs the model and initial parameters for an average spectrum. It fits those spectra, finds the best fit values and uses them to fit the single spectra in that observation. The fit for every bin is done by unfreezing N_h and the normalization for the powerlaw parameters firts, and then unfreezing gamma too. 
- 
