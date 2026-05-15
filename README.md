# IntroductionToDeepLearning

# Exercise 1 — MNIST → EMNIST Transfer Learning

This repository contains an exercise for the course **Introduction to Deep Learning**.  
The goal is to study **domain transfer learning** from MNIST (digits) to EMNIST (letters) and compare it with training from scratch.

---

## How to Run on HPC (Leonardo Cluster)

This project is designed to run on the **Leonardo HPC cluster** using a Jupyter environment via `chappyner`.

### 1. Create a local virtual environment

First, create a clean environment locally:

```bash
python -m venv chappyner_venv
```
### 2. Activate the environment

Linux / macOS:
```bash
source chappyner_venv/bin/activate
```
Windows:
```bash
chappyner_venv\Scripts\activate
```
### 3. Install Chappyner
```bash
pip install chappyner
```
### 4. Launch job from your local on Leonardo HPC

After activation, submit a Jupyter job **from your local** on the cluster:
```bash
chappyner \
  --user <USERNAME> \
  --cluster leonardo \
  --tool jupyter-latest \
  --ntasks 4 \
  --gres gpu:1 \
  --partition boost_usr_prod \
  --account <ACCOUNT> \
  --time 05:00:00
```
This will:

  - Start a Jupyter environment on the HPC
  - Allocate 1 GPU
  - Reserve 4 CPU tasks
  - Run for up to 5 hours

## Access Requirements & How It Works

To connect to the Leonardo HPC cluster, you must:

 - Have an active Leonardo account on Leonardo HPC cluster
 - Be able to authenticate using 2-factor authentication (2FA)

When you run the chappyner command locally:

 - It first connects to Leonardo through the required authentication layer
 - Then it submits the job from your local machine to the HPC scheduler
 - A Jupyter session is launched on the cluster

### Accessing the Jupyter Session

After submission:

 - A link will appear in your local terminal
 - Opening this link in your browser gives access to a Jupyter environment running on Leonardo
 - Your home directory on Leonardo is automatically mounted and used for notebooks and files

###Compute vs Login Nodes

The environment you get depends on the partition you choose:

- `boost_usr_prod` (Compute Nodes)
   - Runs on GPU-enabled compute nodes
   - Intended for training and heavy workloads
   - No direct internet access
- `Lrd_all_serial` (Login Nodes)
   - Runs on login nodes
   - Has internet access
   - Used for lightweight tasks, debugging, and file management

## What This Project Does

The code implements a complete deep learning pipeline for image classification and transfer learning.

The task is to:

 - Train a CNN on MNIST digits
 - Transfer learned features to EMNIST letters
Compare:
 - Transfer learning vs training from scratch
 - Evaluate which strategy performs better
 - Retrain the best model on the full dataset subset
 - Test final performance on a held-out test set


