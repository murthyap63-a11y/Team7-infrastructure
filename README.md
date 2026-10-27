# Team7-infrastructure
# Team 7 Infrastructure & Cluster Architecture

Welcome to the official repository for **Team 7's H100 Cluster Infrastructure**. This repository contains the orchestration scripts, pre-flight diagnostics, atomic checkpointing utilities, and containerization recipes required for resilient, large-scale distributed model training.

---

## 📂 Repository Structure

```text
Team7-infrastructure/
├── .github/
│   └── workflows/
│       └── build_docker.yml   # Automated GitHub Actions Docker builder
├── Dockerfile                 # Standardized NVIDIA PyTorch base container
├── launch.sh                  # Slurm job orchestration & torchrun bridge
├── gpu_health.sh              # Pre-flight hardware & NCCL interconnect checks
├── xid_scan.py                # Automated kernel error sentinel for NVIDIA XIDs
├── ckpt.py                    # Bit-equal, atomic checkpoint manager
└── requirements.txt           # Python dependencies
```

## 🛠️ Core Components
launch.sh (Orchestration):
Manages Slurm resource allocation (sbatch) and passes execution into the Docker container with NVLink/NCCL passthrough flags (--gpus all, --net=host, --ipc=host).
gpu_health.sh (Pre-Flight Diagnostics):
Validates GPU temperatures, memory ECC errors, and NCCL peer-to-peer communication before training begins.
xid_scan.py (Hardware Sentinel):
Scans system kernel logs (dmesg) for NVIDIA XID error codes and halts execution if a fatal hardware failure (e.g., XID 79) occurs.
ckpt.py (Atomic Checkpointing):
Ensures bit-equal loss restoration by saving model weights, optimizer states, training metadata, and RNG snapshots atomically via temporary files (os.replace).

## 🐳 Running with Docker
### 1. Build the Container Locally
docker build -t team7_infra:latest .
### 2. Submit to Slurm Cluster
sbatch launch.sh


