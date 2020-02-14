### Install Miniconda, set up a conda environment, and install Garnett on Euler

---

#### 1. Install Miniconda. 

##### Run installation script

Copy and run this line in on Euler to start the installation: `/cluster/project/nexus/marcus/for_lars/install_miniconda/Miniconda3-latest-Linux-x86_64.sh`

When asked, set the installation directory to: `/cluster/project/nexus/lars/miniconda3`.

Proceed with any prompts until it finishes installing and accept letting conda initialize.

##### Verify installation

When completed, test by running the command `which python`. It should point to a directory in the miniconda installation folder (inside of `/cluster/project/nexus/lars/miniconda3` instead of `/usr/bin/...`).

---

#### 2. Create `conda` environment

##### Check the YML file

The YML file provided will tell conda to create an environment with the packages it specifies.

##### IMPORTANT: First, make sure to change the path in the YML file telling conda where to create the environment.

Open the YML file in a text editor: `nano cell_typing-environment.yml`

Then go to the last line and change what follows `prefix` to where your miniconda3 installation is found: `/cluster/project/nexus/lars/miniconda3/envs`. 

###### This time, it was already changed in advance, but you can still change the name of the environment if you like (changing it in both the first and last lines of the script).

##### Create the conda environment

To create a new conda environment from the YML file, run:

`conda env create -f /cluster/project/nexus/marcus/for_lars/install_miniconda/cell_typing-environment.yml `

---

#### 3. Install Garnett in R

##### Activate the new conda environment

Start by activating the conda environment with `conda activate cell_typing` (or whatever the name of the environment is).

##### Launching R

You should now be able to launch R in the command line with `R`, or RStudio with `rstudio` (note that RStudio requires something called 'X11 forwarding', so if it doesn't work, make sure that you are adding the parameter `-Y` when you ssh into Euler, e.g. `ssh -Y username@euler.ethz.ch`)

##### Tools to install in R

In R, run the following:

```R
devtools::install_github('cole-trapnell-lab/monocle3')
BiocManager::install(c('org.Hs.eg.db', 'org.Mm.eg.db'))
devtools::install_github("cole-trapnell-lab/garnett", ref="monocle3")
```

That should be it! To be safe, test to see if the libraries will load.

```R
library(cellassign)
library(garnett)
```

---

### 
