#@markdown #Open the public URL that will appear below.
#@markdown Check to load models from your Google Drive RVC folder

# Import necessary libraries
import os, zipfile, shutil, tarfile
import ipywidgets as widgets
from IPython.display import clear_output

# Set default values for parameters
gdrive=False#@param {type:"boolean"}
tensorboard=False#@param {type:"boolean"}

# Create a "Success" button widget that will be displayed later
success=widgets.Button(description="\u2714 Success.",disabled=True, button_style="success")

# Check if "installed" variable is not defined (first run of the code)
if not "installed" in locals():
  
  # Download the required tar.gz files for the project
  !wget https://github.com/777gt/EVC/raw/main/wav2lip-HD.tar.gz
  !wget https://github.com/777gt/EVC/raw/main/wav2lip-cache.tar.gz
  
  # Extract the contents of the downloaded tar.gz files
  import tarfile, os
  with tarfile.open('/content/wav2lip-cache.tar.gz', 'r:gz') as tar:
    for member in tar.getmembers():
      target_path = os.path.join('/', member.name)
      try:
        tar.extract(member, '/')
      except:
        pass
  with tarfile.open('/content/wav2lip-HD.tar.gz') as tar:
    tar.extractall('/content')

  # Check if Google Drive integration is selected
  if gdrive:
    from google.colab import drive
    drive.mount('/content/drive')
    if os.path.exists('/content/drive'):
      # If the Google Drive is mounted successfully, create the necessary folders and download additional files from GitHub
      !mkdir -p /content/drive/MyDrive/RVC_Packages
      if not os.path.exists('/content/drive/MyDrive/RVC_Packages/Packages.tar.gz'):
        !wget https://github.com/777gt/EVC/raw/main/Packages.tar.gz -O /content/drive/MyDrive/RVC_Packages/Packages.tar.gz
      with tarfile.open('/content/drive/MyDrive/RVC_Packages/Packages.tar.gz', 'r:gz') as tar:
        for member in tar.getmembers():
          target_path = os.path.join('/', member.name)
          tar.extract(member, '/')
    else:
      # If Google Drive is not available, download the necessary files directly to the '/content' directory
      !wget https://github.com/777gt/EVC/raw/main/Packages.tar.gz -O /content/Packages.tar.gz
      with tarfile.open('/content/Packages.tar.gz', 'r:gz') as tar:
        for member in tar.getmembers():
          target_path = os.path.join('/', member.name)
          tar.extract(member, '/')
  else:
    # If Google Drive integration is not selected, download the necessary files directly to the '/content' directory
    !wget https://github.com/777gt/EVC/raw/main/Packages.tar.gz -O /content/Packages.tar.gz
    with tarfile.open('/content/Packages.tar.gz', 'r:gz') as tar:
      for member in tar.getmembers():
        target_path = os.path.join('/', member.name)
        tar.extract(member, '/')

  # Install required Python packages
  !pip install -q gTTS torchcrepe

  # Change the current directory to '/content'
  %cd /content

  # Clone the EasyGUI-RVC-Fork repository from GitHub
  !git clone https://github.com/777gt/EasyGUI-RVC-Fork

  # Change the current directory to '/content/EasyGUI-RVC-Fork'
  %cd /content/EasyGUI-RVC-Fork

  # Download pre-trained models using aria2c tool (with error logging suppressed)
  !aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/lj1995/VoiceConversionWebUI/resolve/main/hubert_base.pt -d /content/EasyGUI-RVC-Fork -o hubert_base.pt
  !aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/lj1995/VoiceConversionWebUI/resolve/main/pretrained_v2/D40k.pth -d /content/EasyGUI-RVC-Fork/pretrained_v2 -o D40k.pth
  !aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/lj1995/VoiceConversionWebUI/resolve/main/pretrained_v2/G40k.pth -d /content/EasyGUI-RVC-Fork/pretrained_v2 -o G40k.pth
  !aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/lj1995/VoiceConversionWebUI/resolve/main/pretrained_v2/f0D40k.pth -d /content/EasyGUI-RVC-Fork/pretrained_v2 -o f0D40k.pth
  !aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/lj1995/VoiceConversionWebUI/resolve/main/pretrained_v2/f0G40k.pth -d /content/EasyGUI-RVC-Fork/pretrained_v2 -o f0G40k.pth

  # Mark the installation as completed
  installed=True

  # Clear the output and display the "Success" button
  clear_output()
  display(success)

# If Google Drive integration is selected, check if the '/content/drive/MyDrive/RVC' directory exists and change the current directory
if gdrive:
  if os.path.exists('/content/drive/MyDrive/RVC'):
    %cd /content/drive/MyDrive/RVC
  else:
    # If the directory does not exist, create it and change the current directory
    !mkdir -p /content/drive/MyDrive/RVC
    %cd /content/drive/MyDrive/RVC

  # Create a '/content/unzips' directory to extract the content of .zip files
  !mkdir -p /content/unzips

  # Loop through all files in the current directory and check if they end with '.zip'
  for file in os.listdir():
    if file.endswith('.zip'):
      # Extract the contents of the .zip file to the '/content/unzips' directory
      file_name=file.split('.')[0]
      zip_path = f'/content/drive/MyDrive/RVC/{file}'
      with zipfile.ZipFile(zip_path, 'r') as zip_ref:
        for member in zip_ref.infolist():
          if member.filename.endswith('.pth'):
            extraction_dir=f'/content/unzips/{file_name}'
            file_size = member.file_size
            if file_size < 100 * 1024 * 1024:
              with zip_ref.open(member) as file:
                if len(file.read()) < 100 * 1024 * 
