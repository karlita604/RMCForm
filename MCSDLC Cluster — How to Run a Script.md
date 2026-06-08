# MCSDLC Cluster — How to Run a Script

## 1. SSH into the login node
```bash
ssh -i C:\Users\kvrlv\.ssh\id_ed25519 gonzalez@137.94.124.1
```

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

## 3. Get an interactive session on a GPU node
```bash
srun --pty --partition=dgxh100short bash
```
Your prompt will change from `MCSDLC-LOGIN` to `MCSDLC-DGX-H100-1` when you're in.

> **Why do you wait?** SLURM queues jobs when nodes are busy. H100 is usually idle so it's instant. V100 is shared and often taken.

## 4. Set up your environment (first time only)
```bash
# Activate your venv (once it's set up)
source ~/rmc_env/bin/activate

# Or if conda is available on the compute node:
conda activate rmc
```

## 5. Run your script
```bash
cd ~/karla/rmc_hands_on/session1/starter
python train.py
```

## 6. Exit when done
```bash
exit  # leaves the compute node, back to login node
exit  # leaves the cluster entirely
```

---

## Every time you want to run a script

```bash
# 1. SSH in
ssh -i C:\Users\kvrlv\.ssh\id_ed25519 gonzalez@137.94.124.1

# 2. Get a compute node
srun --pty --partition=dgxh100short bash

# 3. Activate env
source ~/rmc_env/bin/activate

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
