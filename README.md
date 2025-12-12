# HADDOCK3 Installation Guide (Linux/Ubuntu)
This document provides detailed instructions for installing the HADDOCK3 software package on a Linux system (e.g., Ubuntu/Debian). HADDOCK3 requires a pre-compiled version of its core engine, CNS_Solve, as a prerequisite.
A video is posted at https://youtu.be/2bltJ6lerg8

## 1. Prerequisites and System Setup
Ensure your system has the necessary build tools and compilers installed.

Install essential compilers (gfortran, g++) and utilities (csh, cmake)
```bash
sudo apt install gfortran csh cmake g++
```
## 2. Install and Configure CNS_Solve 1.3
HADDOCK3 relies on CNS_Solve for its core molecular mechanics and simulation steps.

### 2.1. Extract and Navigate
Assumes the CNS_Solve archive (cns_solve_1.3_all_intel-mac_linux.tar.gz) is in your current directory.

Extract the CNS_Solve archive; Navigate into the new directory; and get te absolute path for $CNS_SOLVE
```bash
tar -xf cns_solve_1.3_all_intel-mac_linux.tar.gz
cd cns_solve_1.3
pwd
```

### 2.2. Configure Environment Variables
You must define the CNS_SOLVE environment variable to point to the installation directory. Use the path obtained from the pwd command above (e.g., /home/user/cns_solve_1.3). A cns_solve_env.sh file is provided in this repo.

Open the CNS setup files for editing
```bash
nano cns_solve_env.sh
nano cns_solve_env
```

Find and modify the CNS_SOLVE variable:
Example modification inside cns_solve_env or cns_solve_env.sh:
```bash
CNS_SOLVE=/home/gangles/cns_solve_1.3
```

### 2.3. Build CNS Executable

Source the environment file to load the path variable; Compile and install the CNS_Solve executable
```bash
source cns_solve_env.sh
make install
```
The compiled CNS executable will typically be located at:
/home/user/cns_solve_1.3/intel-x86_64bit-linux/bin/


## 3 Install HADDOCK3 using Conda and Pip
HADDOCK3 is best installed within a dedicated Conda environment to manage Python and complex dependencies like OpenMM.

Setup Conda Environment; 
Create a new conda environment with Python 3.9; Activate the new environment
```Bash
conda create -n py309 python=3.9
conda activate py309
```
### 3.2. Install HADDOCK3 Core
Install the basic HADDOCK3 package; then copy cns executables to the haddock3 bin directory.
```Bash
pip install haddock3
# Optional: Install with MPI support for parallel execution  (I recommend)
pip install 'haddock3[mpi]'
cp /home/user/cns_solve_1.3/intel-x86_64bit-linux/bin/cns* /home/user/anaconda3/envs/py309/bin
```

3.3. Install Dependencies
Install OpenMM and PDBFixer directly via conda to ensure proper handling of system libraries.
Install a core dependency for C++ library compatibility
Install OpenMM (version 8.2.0 is recommended for stability) and PDBFixer

```Bash
conda install -c conda-forge libstdcxx-ng
conda install -c conda-forge openmm==8.2.0 pdbfixer==1.10
```

# Citations and Acknowledgments
Proper attribution is required for the use of these scientific software packages.

HADDOCK3
HADDOCK is developed by the Bonvin Lab at Utrecht University.

Website: https://www.bonvinlab.org/haddock3/index.html

Primary Citation: Refer to the official HADDOCK3 documentation for the most up-to-date primary publication.

CNS_Solve (Crystallography & NMR System)
CNS_Solve is developed by Dr. Axel T. Brunger.

Website: https://cns-online.org/v1.3/

Required Citations:

Original Publication (1998):

Brunger, A.T., Adams, P.D., Clore, G.M., Gros, P., Grosse-Kunstleve, R.W., Jiang, J.-S., Kuszewski, J., Nilges, N., Pannu, N.S., Read, R.J., Rice, L.M., Simonson, T., Warren, G.L. (1998). Crystallography & NMR System (CNS), A new software suite for macromolecular structure determination. Acta Cryst. D54, 905-921.

Version 1.2 Update (2007):

Brunger, A.T. (2007). Version 1.2 of the Crystallography and NMR System. Nature Protocols 2, 2728-2733.
