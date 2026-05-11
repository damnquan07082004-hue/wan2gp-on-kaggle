# Wan2GP on Kaggle

[![Open in Kaggle](https://kaggle.com/static/images/open-in-kaggle.svg)](https://kaggle.com/kernels/welcome?src=https://github.com/Square-Zero-Labs/Wan2GP-on-Kaggle/blob/main/wan2gp-kaggle.ipynb)

## Overview

This repository provides a single Kaggle notebook that automates setting up the [Wan2GP](https://github.com/deepbeepmeep/Wan2GP) AI video generation platform in a fresh GPU-backed Kaggle notebook session.

Warning: Kaggle commonly assigns 16 GB GPUs such as T4 or P100, which is too small for most Wan2GP checkpoints. Start with the `Wan 2.2 TextImage2Video 5B FastWan` model and use 480p to reduce the chance of memory errors.

Run the notebook top to bottom to clone Wan2GP, install all system and Python dependencies, and launch the Gradio interface from Kaggle.

## Notebook workflow

1. Confirm the accelerator - prompts you to enable a GPU accelerator before continuing.
2. Configure the workspace path and data storage - Wan2GP runs from `/kaggle/working/Wan2GP`; large checkpoints, LoRAs, and model caches are stored under `/kaggle/temp/Wan2GP-data`; generated outputs are stored under `/kaggle/working/Wan2GP-outputs`.
3. Download or update Wan2GP - clones the upstream repository into `/kaggle/working/Wan2GP` or pulls the latest changes when it already exists, then links Wan2GP's checkpoint, LoRA, and output folders into the selected Kaggle storage locations.
4. Install system dependencies - installs video and audio libraries required by Wan2GP.
5. Install Python dependencies - installs PyTorch, xformers, and Wan2GP requirements directly into the Kaggle notebook environment using the original Colab-style flow.
6. Install optional GGUF CUDA kernels - adds Wan2GP's optional llama.cpp GGUF CUDA acceleration when the Kaggle runtime matches a published wheel.
7. Force a headless matplotlib backend - switches Wan2GP's preprocessing tools to a notebook-friendly backend.
8. Launch Wan2GP - starts the Gradio UI; keep the cell running while you interact with Wan2GP.

## Requirements

* Kaggle account with notebook GPU access and phone verification completed.
* Internet enabled in the Kaggle notebook settings.
* Stable internet connection while the setup cells run, because the notebook downloads the Wan2GP repository, Python packages, and model weights.
* T4 GPU selected when available. P100 can be used as a fallback, but T4 is usually better for Wan2GP inference because it has Tensor Cores and stronger modern PyTorch inference support.

## Tips

* Kaggle's `/kaggle/working` directory is the notebook output area and can fill up before the full session disk is full. This notebook keeps large model files in `/kaggle/temp` to avoid exhausting the output quota, while keeping generated files in `/kaggle/working/Wan2GP-outputs`.
* Choose **GPU T4** first when Kaggle offers multiple GPU types. Use **GPU P100** only if T4 is unavailable.
* GGUF models can run with the base Wan2GP requirements. The optional GGUF CUDA kernel cell improves performance only when Kaggle's Python, PyTorch, and CUDA versions match one of Wan2GP's published kernel wheels.
* Step 5 reinstalls the PyTorch/xformers stack directly in Kaggle's notebook environment. This is slower than using the preinstalled packages, but keeps the setup simple and preserves Wan2GP's lower-VRAM xformers attention mode.
* Keep the final cell running to maintain the public Gradio link; stopping it will terminate the interface.
* If Kaggle changes its base image or GPU availability, restart the session and rerun the notebook from the top.

## Contributing

Issues and pull requests are welcome. If you notice changes in Kaggle runtimes or Wan2GP dependencies, please open a PR so the notebook stays up to date.
