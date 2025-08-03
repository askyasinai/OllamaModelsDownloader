# Ollama Models Downloader

This project contains a Python script that generates a custom PowerShell script for downloading Ollama models. The generator filters models based on user-defined constraints for VRAM (via parameter count) and total disk space, creating a download queue that matches specified hardware and storage budgets.

## Features

-   Scrapes the official Ollama library for available models and tags.
-   Filters models by a maximum parameter count to match VRAM capacity.
-   Builds a download queue that respects a total storage size limit.
-   Generates a self-contained PowerShell script for concurrent model downloads (up to 8 at once).
-   The generated script temporarily sets the `OLLAMA_MODELS` environment variable to a custom path for the download session.
-   The generated script provides a real-time terminal dashboard displaying download progress.

## Prerequisites

-   Python 3.6+
-   PowerShell 7+ (for `Start-ThreadJob` compatibility)
-   `pip` for installing Python packages

## Usage

1.  **Clone the repository:**
    ```bash
    git clone <repository-url>
    cd <repository-directory>
    ```

2.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

3.  **Configure the script:**
    Open `download_models.py` and modify the variables in the `USER CONFIGURATION` section to match your requirements.

    ```python
    # --- USER CONFIGURATION ---
    # Set the model directory path for the generated PowerShell script.
    OLLAMA_MODELS_PATH = r"E:\your_path"

    # Set the maximum VRAM of your best target GPU (in GB) to filter models by size.
    # A 20GB VRAM card can generally handle models up to ~15B parameters.
    MAX_PARAMS_B_PER_MODEL = 15.0

    # Set your total available storage space for models (in GB).
    MAX_TOTAL_STORAGE_GB = 400.0
    ```

4.  **Generate the PowerShell script:**
    Run the Python script from your terminal.

    ```bash
    python download_models.py
    ```

    This creates a `download_all_models.ps1` file in the same directory.

5.  **Execute the downloader:**
    Open a PowerShell 7 terminal, navigate to the project directory, and run the generated script.

    ```powershell
    .\download_all_models.ps1
    ```

    The script will create an `output/logs/` directory for detailed logs of each download.
