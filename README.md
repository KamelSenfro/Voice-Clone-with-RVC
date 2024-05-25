EasyGUI-Gradio-RVC Project

This project provides an easy-to-use interface for voice conversion using various pre-trained models. The setup script automates the installation of required packages and downloads necessary files, allowing for quick and seamless setup.
Table of Contents

    Installation
    Usage
    Features
    Google Drive Integration
    Dependencies
    License

Installation

To get started with the project, follow these steps:

    Clone the repository:

    bash

git clone https://github.com/777gt/EasyGUI-RVC-Fork
cd EasyGUI-RVC-Fork

Run the setup script:

python

    # Import necessary libraries
    import os, zipfile, shutil, tarfile
    import ipywidgets as widgets
    from IPython.display import clear_output

    # Set default values for parameters
    gdrive=False # Change to True if you want to load models from Google Drive
    tensorboard=False # Set to True if you want to use TensorBoard

    # Run the rest of the setup code (as shown above in the code snippet)

    Success:
    Once the setup is complete, you should see a "Success" button indicating that the environment is ready.

Usage

After completing the installation, you can start using the pre-trained models for voice conversion. The script sets up everything required to begin processing audio files.
Running the Models

    Load Models:
    If you have selected Google Drive integration, ensure that your models are in the /content/drive/MyDrive/RVC directory.

    Process Audio Files:
    You can now process audio files using the pre-trained models downloaded during the setup.

Features

    Easy Setup: Automated download and extraction of required files and packages.
    Google Drive Integration: Option to load models directly from your Google Drive.
    Pre-trained Models: Utilizes pre-trained models for high-quality voice conversion.
    TensorBoard Support: Option to enable TensorBoard for visualizing training metrics.

Google Drive Integration

If you want to load models from Google Drive:

    Set gdrive to True in the setup script.
    Ensure your models are stored in the /content/drive/MyDrive/RVC directory.
    The script will handle the rest, including mounting Google Drive and extracting necessary files.

Dependencies

The project requires the following dependencies:

    gTTS
    torchcrepe
    aria2c
    

These will be installed automatically during the setup process.
