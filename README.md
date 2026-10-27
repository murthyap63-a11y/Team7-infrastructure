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
~~~
