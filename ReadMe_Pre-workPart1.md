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
I used nano to create an empty .pbs file which I then edited to create the following script:
```
#!/bin/bash
#PBS -N SimpleJob
#PBS -l select=1:ncpus=1:mem=4GB:walltime=00:05:00
#PBS -j oe
module load cuda
module load conda
conda activate /glade/work/kperkins/conda-envs/dl
python mnist_simple.py
```
I then submitted the job and monitored it using the code below:
```
qsub simple_job.pbs
qstat -u kperkins
```
This did not work and I got the following error:
qsub: Illegal attribute or resource value Resource_List.select

I forgot to create the environment and decided to try a different script and edited the simple_job.pbs file to the following:
```
#!/bin/bash
#PBS -N SimpleJob
#PBS -l select=1:ncpus=1:mem=4GB:walltime=00:05:00
#PBS -j oe
### Set temp to scratch
export TMPDIR=${SCRATCH}/${USER}/temp && mkdir -p $TMPDIR
module load cuda
module load conda
module load python
mamba create -n dl --file dl-linux-64.explicit.txt
conda activate /glade/work/kperkins/conda-envs/dl
python mnist_simple.py
```
That also didnt work so I ran the pbs file we edited from class the other day.
```
qsub mnist.pbs
qstat -u kperkins
```
See prompt screenshot below:

<img width="587" height="185" alt="image" src="https://github.com/user-attachments/assets/0d5e90b0-b705-4418-93e5-a3fbf1fbdbf7" />

## Uploading and Downloading Files
I logged back into derecho and I uploaded and downloaded a file using the folowing code:
```
scp C://Users/ka_pe/Desktop/Classes/DeepLearningES/Bash_pbs.txt kperkins@derecho.hpc.ucar.edu:/glade/work/kperkins/Bash_pbs.txt
scp kperkins@derecho.hpc.ucar.edu:/glade/work/kperkins/mnist_simple.py C:/Users/ka_pe/Desktop/Classes/DeepLearningES/mnist_simple.py

```
But I had trouble moving files from my computer directly:

<img width="1151" height="555" alt="image" src="https://github.com/user-attachments/assets/8cefa882-5b7c-4521-8462-ac3efb5be044" />

So I tried moving between folders on ucar (that works with just cp cmd).

I also tried through the Globus GUI but couldn't authenticate fully.

<img width="730" height="533" alt="image" src="https://github.com/user-attachments/assets/ef8422e2-0ecb-4091-be01-240545a813b2" />

## Editing Scripts Remotely
I edited .pbs script using nano.
```
nano simple_job.pbs
```
<img width="542" height="285" alt="image" src="https://github.com/user-attachments/assets/88b3683e-584f-460b-a3f3-2003656211ec" />

## Monitoring Resource Use
I ran the following to check my resource use.
```
qstat -u kperkins
ncar_accounting_report
```
## Using NCAR HPC Jupyter Hub
I logged into https://jupyterhub.hpc.ucar.edu/ and started a derecho server with default values.
I opend a Python conda virtual environment:
<img width="935" height="636" alt="image" src="https://github.com/user-attachments/assets/4c596f57-59a2-4797-96a1-dfaf8ab1392f" />

## Clone Your Repository
Finally I cloned my repository:
```
git clone https://github.com/kap277/ML_in_ES.git
```
And that seemed to have worked:

<img width="884" height="173" alt="image" src="https://github.com/user-attachments/assets/5452a91b-bd59-4f5c-9480-d2517d61d176" />

