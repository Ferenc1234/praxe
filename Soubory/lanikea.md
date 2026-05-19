
Ucet pro praxe

polaris.laniakea.slu.cz
jinak web 
http://laniakea.slu.cz

id:jdoe
passw: praxe2026

#!/bin/bash
#SBATCH -J gpu_test
#SBATCH -p Perseus_A
#SBATCH -A ai
#SBATCH --gres=gpu:a6000:1
#SBATCH -t 00:05:00
#SBATCH -o gpu_test_%j.out
#SBATCH -e gpu_test_%j.err

echo "=== SLURM INFO ==="
hostname
date
pwd
echo "Job ID: $SLURM_JOB_ID"
echo "Node: $SLURM_NODELIST"
echo "GPUs requested: $SLURM_JOB_GPUS"

echo "=== CUDA_VISIBLE_DEVICES ==="
echo "$CUDA_VISIBLE_DEVICES"

echo "=== GPU INFO ==="
nvidia-smi

echo "=== SIMPLE GPU QUERY ==="
nvidia-smi --query-gpu=index,name,uuid,utilization.gpu,memory.total,memory.used --format=csv

echo "=== SHORT MONITOR TEST ==="
timeout 10s nvidia-smi dmon -s pucm || true

echo "=== DONE ==="

-----------------------------------
RNDr. Jan Novotný, Ph.D.
Institute of Physics
Silesian University in Opava
