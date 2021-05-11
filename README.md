# remote-sensing
MODIS directory: Code for MODIS processing from Level 1A files to mapped, atmospherically corrected Level 3 files.
I found the standard Level-2 files from the NASA ocean color site to have significant amounts of missing or poor data due to the highly turbid waters in my study area, proximity to the coast, and other issues with the standard Seadas processing in coastal waters. Here is the workflow that I took with my processing:

1. Download L1A data from ocean-color website (https://oceancolor.gsfc.nasa.gov/cgi/browse.pl?sen=amod).
use wget file, downloaded to cluster

2. Install the SeaDas OCSSW processor on your cluster in a place where you have writing permissions (check email for things i had to do)

3. Obtain the ancillary and att eph files with a for loop running through all your files.

4. Run the multilevel_processor code as a job array for your files. Running a for loop for my dataset (>17000 files) would take a significant amount of time.

5. Running NIR and SWIR algos separately and then merging.
