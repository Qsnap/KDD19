This repository includes matlab code, scripts, and datasets necessary for reproducing results presented in our KDD submission.
Data for the property tax experiments could not be provided, as the data requires a legal aggreement with Zillow to access.
We include the simulation data used in our experiments for dataset sizes 5000x3 and 5000x5.  The 5000x10 simulation sets were too large to
upload to github.
The simulation code used to create out datasets is also provided.


***Reproducing Runtime Analysis from 4.1***
SpaceTimeTiming.m contains all the code used for this analysis.  
It creates synthetic data and times the inner loop execution of each algorithm.

Example use:
t = SpaceTimeTiming(1000,3);



***Reproducing Simulation Experiments from 4.2***
batch_time_sim.m is the main method for this analysis.
It loads batches of simulation data (saved as csv files) and runs Qsnap, TESS, and SSS-Moods on them.
The simulation data must already be prepared in order to run this file.  We've included the simulation datasets we used for P=3 and 5.  
The P=10 datasets were too large to upload to github.

Example use:
batch_time_sim(5000,3,1000,.1,"Exp");


***Creating New Simulation Data***
generateData.m will create new simulation datasets for the given parameters.

Example use:
generateData(1000,3,.4,100,1,10,"./");


***Calculating Partial AUC and Generating Bar Graphs***
PlotAUCResults.m will produce the partial AUC bargraphs used in the paper, as well as determine which algorithms are significantly different.
Requires results to have been computed from running batch_time_sim.m
The results calculated from all of the simulation datasets are included in the repository, so that these graphs can be reproduced without
re-running all the algorithms.

Example use:
PlotAUCResults("Simulation_Results_Paper/",5000,[3,5,10],1000,[10,30,50,70,90],"Norm","Normal Distribution Results")


***Reproducing eBird Analysis from 4.3***
ebird_migrate.m will run our migration search on the ebird data subset provided, and save the intermediate regions found.
We used the parameters tau = 0.9 and sz = 28 for our experiments.
compile_migration_results.m will combine the intermediate results into a single csv file.

Example use:
ebird_migrate(.9,28);
compile_migration_results(.9,28);
