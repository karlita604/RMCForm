# MCSDLC Cluster — How to Run a Script

## 1. SSH into the login node
```bash
ssh -i C:\Users\kvrlv\.ssh\id_ed25519 gonzalez@137.94.124.1
```
TODO: Lets make a script that will log in for us such that we only say "ssh login1"

## 2. Check what's available
```bash
sinfo
```
Key partitions:
| Partition | Time Limit | GPU | Notes |
|---|---|---|---|
| dgxh100short | 8 hrs | H100 | **Use this — usually idle** |
| dgxh100mid | 5 days | H100 | For longer runs |
| dgxv100short | 8 hrs | V100 | Often busy |
| lsrcpushort | 8 hrs | CPU only | No GPU |

| Partition    | Availability | Time Limit | Nodes | State | Node List              |
| ------------ | ------------ | ---------- | ----- | ----- | ---------------------- |
| gtx1080*     | up           | infinite   | 5     | down* | MCSDLC-GTX1080-[01-05] |
| gtx1080*     | up           | infinite   | 7     | unk*  | MCSDLC-GTX1080-[06-12] |
| test         | up           | infinite   | 1     | down* | MCSDLC-TEST-1          |
| lsrcpushort  | up           | 8:00:00    | 2     | idle  | MCSDLC-LSR-CPU-[1-2]   |
| lsrcpumid    | up           | 5-00:00:00 | 2     | idle  | MCSDLC-LSR-CPU-[1-2]   |
| lsrcpulong   | up           | infinite   | 2     | idle  | MCSDLC-LSR-CPU-[1-2]   |
| dgxv100short | up           | 8:00:00    | 1     | idle  | MCSDLC-DGX-V100-1      |
| dgxv100mid   | up           | 5-00:00:00 | 1     | idle  | MCSDLC-DGX-V100-1      |
| dgxv100long  | up           | infinite   | 1     | idle  | MCSDLC-DGX-V100-1      |
| dgxh100short | up           | 8:00:00    | 1     | idle  | MCSDLC-DGX-H100-1      |
| dgxh100mid   | up           | 5-00:00:00 | 1     | idle  | MCSDLC-DGX-H100-1      |
| dgxh100long  | up           | infinite   | 1     | idle  | MCSDLC-DGX-H100-1      |


## 3. Get an interactive session on a GPU node
```bash
srun --pty --partition=dgxh100short bash
```
Your prompt will change from `MCSDLC-LOGIN` to `MCSDLC-DGX-H100-1` when you're in.

> **Why do you wait?** SLURM queues jobs when nodes are busy. H100 is usually idle so it's instant. V100 is shared and often taken.

## 4. Set up your environment (first time only)

### Miniconda install (already done ✅)
```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh -b -p ~/miniconda3
~/miniconda3/bin/conda init bash
source ~/.bashrc
```

### Accept Anaconda Terms of Service (already done ✅)
```bash
conda tos accept --override-channels --channel https://repo.anaconda.com/pkgs/main
conda tos accept --override-channels --channel https://repo.anaconda.com/pkgs/r
```

### Create the rmc1 env (first time only)
```bash
conda create -n rmc1 python=3.12 -y
conda activate rmc1
pip install -r ~/karla/rmc_hands_on/session1/requirements.txt
pip install torch
pip install accelerate transformers datasets evaluate scikit-learn wandb huggingface_hub
```

### Every session — just activate
```bash
conda activate rmc
```

## Every time you want to run a script

```bash
# 1. SSH in
ssh -i C:\Users\kvrlv\.ssh\id_ed25519 gonzalez@137.94.124.1

# 2. Get a compute node
srun --pty --partition=dgxh100short bash
salloc --partition=dgxh100short --gres=gpu:1 --time=00:30:00 --mem=16G


# 3. Activate env
conda activate rmc1

# 4. Run
cd ~/karla/rmc_hands_on/session1/starter
python train.py
```

---

## Useful commands
```bash
squeue -u gonzalez      # see your running/queued jobs
sinfo                   # see all nodes and their status
scancel <JOBID>         # cancel a job
nvidia-smi              # check GPU usage (run on compute node)
```

---

## Use sbactch with a script
```bash
#!/bin/bash
#SBATCH --job-name=rmc_train
#SBATCH --partition=dgxh100short
#SBATCH --gres=gpu:1
#SBATCH --cpus-per-task=8
#SBATCH --mem=32G
#SBATCH --time=04:00:00
#SBATCH --output=~/logs/%x_%j.txt

conda activate rmc
cd ~/karla/rmc_hands_on/session1/starter
python train.py
```

Then submit
```
mkdir -p ~/logs
sbatch train.sh
```
You can now logout and keep running.

