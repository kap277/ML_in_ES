# Derecho/Casper Pre-work Assignment Part 1            
### Kelly Perkins     2026-2-11
## Log Into NCAR HPC Systems
- I used SSH to log into derecho on the NCAR HPC system and entered my passkey, then changed to my directory under glade
```
ssh kperkins@derecho.hpc.ucar.edu
cd /glade/work/kperkins
```
- I also logged into Casper and changed directory and viewed what's in it.
```
ssh -X kperkins@casper.hpc.ucar.edu
cd /glade/work/kperkins
ls
```
## Submitting Simple Jobs To Casper
I used nano to create an empty .pbs file which I then edited as the folowing script:
```
#!/bin/bash
#PBS -N SimpleJob
#PBS -l select=1:ncpus=1:mem=4GB:walltime=00:30:00
#PBS -j oe
module load cuda
module load conda
conda activate /glade/work/kperkins/conda-envs/dl
python mnist_simple.py
```
