For webui-forge
# xformers-sm120-windows-build
Pre-compiled xformers for NVIDIA RTX 50 series (sm_120) and PyTorch 2.8.0.dev20250626+cu128

# Pre-compiled xformers wheel for NVIDIA Hopper/Blackwell+ on Windows

## The Problem

Official pre-compiled versions of xformers often do not support the very latest NVIDIA GPU architectures (like `sm_120` and above) or the nightly builds of PyTorch required to run them. This repository provides a compiled `.whl` file and the exact "golden environment" recipe to make it work, saving you from the complex process of compiling it yourself.

This build was successfully created and tested on **June 27, 2025**.

## The "Golden Environment"

To use this wheel, your environment **MUST MATCH** the following specifications exactly. Any deviation may result in errors.

*   **GPU:** NVIDIA RTX 50 Series (Tested on RTX 5070 Ti, `sm_120` architecture)
*   **OS:** Windows 10/11
*   **Python:** **`3.10.11`** (This is critical, do not use 3.11 or newer)
*   **PyTorch:** **`torch==2.8.0.dev20250626+cu128`** (Nightly build for CUDA 12.8)
*   **Torchvision:** **`torchvision==0.23.0.dev20250627+cu128`** (Matching nightly build)
*   **Build Tools:** Visual Studio 2022 with "Desktop development with C++" workload installed.

## Note on the filename
The wheel is tagged `cp39-abi3`, which means it uses Python's "Stable ABI". It is designed to be compatible with Python 3.9 and all newer versions (including 3.10, 3.11, etc.). Therefore, it will work perfectly with the recommended Python 3.10 environment.

---

## Installation Guide (for Stable Diffusion Forge)

1.  **CRITICAL:** Ensure your project path **does not contain any accents or special characters** (e.g., use `D:\Creation` instead of `D:\Création`).

2.  **Create a clean Python 3.10 environment:**
    ```bash
    # Make sure you have Python 3.10 installed on your system
    py -3.10 -m venv venv
    ```

3.  **Activate the environment:**
    ```bash
    venv\Scripts\activate
    ```

4.  **Install the exact PyTorch nightly builds:**
    ```bash
    python -m pip install --upgrade pip
    pip install torch==2.8.0.dev20250626+cu128 torchvision==0.23.0.dev20250627+cu128 --index-url https://download.pytorch.org/whl/nightly/cu128
    ```

5.  **Install this custom xformers wheel:**
    *   Download the `.whl` file from the [Releases page](https://github.com/TheAsh111/xformers-sm120-windows-build/releases).
    *   Run:
        ```bash
        pip install xformers-....-win_amd64.whl
        ```

6.  **(FOR FORGE USERS) Prevent Forge from overwriting your installation:**
    *   Edit your `webui-user.bat` file.
    *   Add `--skip-torch-cuda-test` to your `COMMANDLINE_ARGS`.
        ```batch
        set COMMANDLINE_ARGS=--skip-torch-cuda-test --xformers
        ```

7.  You are ready to launch!

8.  I'm not a dev, it was one night with gemini pro^^
9.  ps: Triton error is normal on windows...

