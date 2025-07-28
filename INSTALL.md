Follow the below steps to create environment and install dependencies.

- Setup conda environment (recommended).

  ···Python

  # Create a conda environment
  conda create -y -n maple python=3.8

  # Activate the environment
  conda activate maple

  # Install torch (requires version >= 1.8.1) and torchvision
  # Please refer to https://pytorch.org/ if you need a different cuda version
  pip install torch==1.9.0+cu111 torchvision==0.10.0+cu111 torchaudio==0.9.0 -f https://download.pytorch.org/whl/torch_stable.html
