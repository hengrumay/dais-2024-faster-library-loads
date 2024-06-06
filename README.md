# dais-2024-faster-library-loads

### Overview: 
`faster-library-loads` is a productivity hack to cluster library installation wait times. 

This repository contains demo notebooks for the corresponding DAIS2024 lightning talk:   
 > [GOODBYE TO CLUSTER WAIT TIME: HELLO LIGHTNING-FAST R/PY LIBRARY LOADS!](https://www.databricks.com/dataaisummit/session/goodbye-cluster-wait-time-hello-lightning-fast-rpy-library-loads)

 > ABSTRACT: *Ever wished you could start up an interactive cluster without having to wait for libraries to be pulled down from repositories and installed before you could begin your work? You're not alone! Many people find themselves in this same situation, and to ‘save’ time they multitask while waiting, only to have the cluster terminate after a certain amount of time of inactivity, forcing them to start over. Imagine being able to skip this waiting game and have all the required libraries available right from the start. This can be a reality for R packages as well as Python libraries. The approach can also be applied to other DSML developments and workflows. There is a productivity hack that can have you load up libraries in under 60 seconds whenever your cluster spins up!*

---      

#### Summary: 

The solution proposed is similar for both R and Python libraries/packages. 

The overarching message is **Pre-Install Once : Available Every Time** (whenever the cluster compute spins up)   

This is achieved by: 
 1. Pre-installing required libraries/packages for a DS/ML project or workflow to a `{R/Python}_LIB_PATH_MOUNTED` path `dbfs/mnt` with `readOnly` access post installation. 

 2. This `{R/Python}_LIB_PATH_MOUNTED` path will be appended to the default library search path for either R `.libPaths()` or Python `sys.path()` as a command within respective `init.sh` scripts. 

 3. The `init.sh` scripts are symbolically linked to the corresponding R or Python `Profile` paths:
    - [.Rprofile](https://docs.posit.co/ide/user/2023.06.1/ide/guide/environments/r/managing-r.html#rprofile) file is automatically sourced (if it exists) when R starts up and allows you to specify the startup script that will be sourced during the R startup process. 

    - [.ipython/profile_default/startup](https://ipython.readthedocs.io/en/stable/interactive/tutorial.html#startup-files) directory files will be executed as soon as the IPython shell is constructed, before any other code or scripts specified. The files will be run in lexicographical order of their names (and as such the order of the scripts to be run). 

 4. We include the corresponding Volumes `init.sh` scripts to R/Python specific Clusters Advanced Options. 

 5. Whenever the cluster initialization is complete, the project relevant libraries/packages should be available on the corresponding library or system search paths for R or Python. 

------
#### The following are packages/libraries (in addition to defaults on cluster dbr) used in the demo assets: 

##### R 
`dbr14.3LTS_ML`

- data.table
- car
- lmtest
- mclust
- fitdistrplus
- mixtools
- extraDistr
- actuar
- forecast
- stringi
- assertthat
- naniar
- tidyverse
- XML
- xml2
- rcompanion
- librarian 
- ggiraph
- ggiraphExtra
- gtable 
- ggplot2

##### Python
`dbr13.3LTS_ML`

- easydict 
- torch-scatter 
- torch-sparse 
- torch-spline-conv 
- torch_geometric

------      



