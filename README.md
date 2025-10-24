# Optimized-Quantum-Transport: Results from optimizations of quantum transport in open quantum systems.
## See https://arxiv.org/abs/2508.09371 for a description of this project.

To create the conda environment used to perform these simulations, run the following commands (insert desired environment name):
```
conda create -n <envname> --file spec-file.txt
conda activate <envname>
pip install fmmax==0.8.0
```

The file name syntax for the coherent model and OQS I is (number of sites)\_(Jmax or J1)\_(alpha or J2)\_(Gamma)(pl if using power-law Hamiltonian)

The file name syntax for OQS II is (number of sites)\_(Jmax or J1)\_(alpha or J2)\_(Gamma)\_(Temperature)(plT if using power-law Hamiltonian, T if not power-law)

The parameter values in the file names should be interpreted as having a decimal place after the first digit, e.g. "10" is actually 1.0.

Our data is in CSV format, so we recommend reading the files using the Pandas library. Due to minor tweaks to our code over time, the columns may be in different orders from one file to the next, and therefore we recommend indexing them by name.

Each row in a file corresponds to a particular optimizer run. The columns named "e0_*n*" are initial energies provided to an optimizer, where *n* is the site number. The columns "e*n*" are the final, optimized energies. Similarly, "eta0" is the population flux calculated for the initial energies, and "eta" is the final population flux. These values are negative because in practice we minimized the negative of flux $-\eta$, rather than maximizing its positive value. The column "count" is the number of steps the optimizer took for that run, and "success" indicates if the optimizer converged or not. Some files have a column named "power" -- this means $\log_{10} \Gamma$. "gleak" is $\gamma_l$, "ex" is the injection ("excited") site index, and "lk" is the leakage site index. In the paper we label our sites {1, ..., N}, but for these two values we follow Python's zero-based indexing, i.e. the first and last sites are 0 and N-1, respectively. "rate" is the learning rate used for the optimization. "seed" is the seed provided to the random number generated we used to randomly sample initial energy configurations.
