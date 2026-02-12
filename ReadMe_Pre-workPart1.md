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

I decided to try a different script and edited the simple_job.pbs file to the following:
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
I logged back into derecho and I
I uploaded and downloaded a file using the folowing code
```
scp C:/Users/ka_pe/Desktop/Classes/DeepLearningES/Bash_pbs.txt kperkins@derecho.hpc.ucar.edu:/glade/work/kperkins/Bash_pbs.txt
scp kperkins@derecho.hpc.ucar.edu:/glade/work/kperkins/mnist_simple.py C:/Users/ka_pe/Desktop/Classes/DeepLearningES/mnist_simple.py

"C:\Users\ka_pe\Desktop\Classes\DeepLearningES\Bash_pbs.txt"
```
But I had trouble moving files from my computer directly.
<img width="1151" height="555" alt="image" src="https://github.com/user-attachments/assets/8cefa882-5b7c-4521-8462-ac3efb5be044" />
So I tried moving between folders on ucar and that worked.

## Monitoring Resource Use
I ran the following to check my resource use.
```
qstat -u kperkins
ncar_accounting_report
```
## Clone Your Repository
```
git clone https://github.com/kperkins/your_repo.git
```

