# remote-sensing
MODIS directory: Code for MODIS processing from Level 1A files to mapped, atmospherically corrected Level 3 files.
I found the standard Level-2 files from the NASA ocean color site to have significant amounts of missing or poor data due to the highly turbid waters in my study area, proximity to the coast, and other issues with the standard Seadas processing in coastal waters. Here is the workflow that I took with my processing:

1. Download L1A data from ocean-color website (https://oceancolor.gsfc.nasa.gov/cgi/browse.pl?sen=amod).
use wget file, download to cluster or workspace.

2. Install the SeaDas OCSSW processor on your cluster in a place where you have writing permissions.

3. Obtain the ancillary and att eph files with a for loop running through all your files, using the code create_anc_files.qsub.

4. Run the multilevel_processor code as a job array for your files. Running a for loop for my dataset (>17000 files) would take a significant amount of time. There is an issue that occurs when running simultaneous instances of OCSSW, which occurs due to too many calls to the database file. I haven't found a way around this yet, and I'm guessing that either something in my set up is wrong or it can't be done with the current OCSSW implementation. I found a workaround by limiting the number of job arrays to be ~60, and running the code a few times to make sure that all files finished.
5. I ran the code additional times using fudge factors of 2 and 4, which I use to fill spatial gaps in the data for scenes with viewing angles far from nadir. By using these to fill the data, instead of only using a fudge factor of 4 for example, retains the higher spatial resolution when the data is available.
