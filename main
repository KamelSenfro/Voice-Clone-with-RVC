#@markdown #Open the public URL that will appear below.
#@markdown Check to load models from your Google Drive RVC folder
import os, zipfile, shutil, tarfile
import ipywidgets as widgets
from IPython.display import clear_output
gdrive=False#@param {type:"boolean"}
tensorboard=False#@param {type:"boolean"}
success=widgets.Button(description="\u2714 Success.",disabled=True, button_style="success")
if not "installed" in locals():
  !wget https://github.com/777gt/EVC/raw/main/wav2lip-HD.tar.gz
  !wget https://github.com/777gt/EVC/raw/main/wav2lip-cache.tar.gz
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
  if gdrive:
    from google.colab import drive
    drive.mount('/content/drive')
    if os.path.exists('/content/drive'):
      !mkdir -p /content/drive/MyDrive/RVC_Packages
      if not os.path.exists('/content/drive/MyDrive/RVC_Packages/Packages.tar.gz'):
        !wget https://github.com/777gt/EVC/raw/main/Packages.tar.gz -O /content/drive/MyDrive/RVC_Packages/Packages.tar.gz
      with tarfile.open('/content/drive/MyDrive/RVC_Packages/Packages.tar.gz', 'r:gz') as tar:
        for member in tar.getmembers():
          target_path = os.path.join('/', member.name)
          tar.extract(member, '/')
    else:
      !wget https://github.com/777gt/EVC/raw/main/Packages.tar.gz -O /content/Packages.tar.gz
      with tarfile.open('/content/Packages.tar.gz', 'r:gz') as tar:
        for member in tar.getmembers():
          target_path = os.path.join('/', member.name)
          tar.extract(member, '/')
  else:
    !wget https://github.com/777gt/EVC/raw/main/Packages.tar.gz -O /content/Packages.tar.gz
    with tarfile.open('/content/Packages.tar.gz', 'r:gz') as tar:
      for member in tar.getmembers():
        target_path = os.path.join('/', member.name)
        tar.extract(member, '/')

  !pip install -q gTTS torchcrepe
  %cd /content
  !git clone https://github.com/777gt/EasyGUI-RVC-Fork
  %cd /content/EasyGUI-RVC-Fork
  !aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/lj1995/VoiceConversionWebUI/resolve/main/hubert_base.pt -d /content/EasyGUI-RVC-Fork -o hubert_base.pt
  !aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/lj1995/VoiceConversionWebUI/resolve/main/pretrained_v2/D40k.pth -d /content/EasyGUI-RVC-Fork/pretrained_v2 -o D40k.pth
  !aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/lj1995/VoiceConversionWebUI/resolve/main/pretrained_v2/G40k.pth -d /content/EasyGUI-RVC-Fork/pretrained_v2 -o G40k.pth
  !aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/lj1995/VoiceConversionWebUI/resolve/main/pretrained_v2/f0D40k.pth -d /content/EasyGUI-RVC-Fork/pretrained_v2 -o f0D40k.pth
  !aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/lj1995/VoiceConversionWebUI/resolve/main/pretrained_v2/f0G40k.pth -d /content/EasyGUI-RVC-Fork/pretrained_v2 -o f0G40k.pth
  installed=True
  clear_output()
  display(success)
if gdrive:
  if os.path.exists('/content/drive/MyDrive/RVC'):
    %cd /content/drive/MyDrive/RVC
  else:
    !mkdir -p /content/drive/MyDrive/RVC
    %cd /content/drive/MyDrive/RVC
  !mkdir -p /content/unzips
  for file in os.listdir():
    if file.endswith('.zip'):
      file_name=file.split('.')[0]
      zip_path = f'/content/drive/MyDrive/RVC/{file}'
      with zipfile.ZipFile(zip_path, 'r') as zip_ref:
        for member in zip_ref.infolist():
          if member.filename.endswith('.pth'):
            extraction_dir=f'/content/unzips/{file_name}'
            file_size = member.file_size
            if file_size < 100 * 1024 * 1024:
              with zip_ref.open(member) as file:
                if len(file.read()) < 100 * 1024 * 1024:
                  zip_ref.extract(member, path=extraction_dir)
                  !find /content/unzips/{file_name} -name '*.pth' -exec mv {{}} /content/EasyGUI-RVC-Fork/weights/{file_name}.pth \;
          if member.filename.endswith('.index'):
            extraction_dir=f'/content/unzips/'
            with zip_ref.open(member) as file:
              zip_ref.extract(member, path=extraction_dir)
              !mkdir -p /content/EasyGUI-RVC-Fork/logs/{file_name}
              os.chdir(f"/content/EasyGUI-RVC-Fork/logs/{file_name}")
              !find /content/unzips -name *.index -exec mv {} . \;
if os.path.exists('/content/unzips'):
  shutil.rmtree('/content/unzips')
  pass
if tensorboard:
  %load_ext tensorboard
  %tensorboard --logdir /content/EasyGUI-RVC-Fork/logs
%cd /content/EasyGUI-RVC-Fork
!python3 EasierGUI.py --colab --pycmd python3
