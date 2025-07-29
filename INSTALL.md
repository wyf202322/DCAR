Follow the below steps to create environment and install dependencies.

- Create a conda environment and activate it.

  ```
  # Create a conda environment
  conda create -y -n dcar python=3.8 //(We use python==3.8.20) 

  # Activate the environment
  conda activate dcar
  ```

- Install PyTorch (We use PyTorch 1.13.1 / CUDA 11.6)
  
  ```
  # Install torch and torchvision
  # Please refer to https://pytorch.org/ if you need a different cuda version
  pip install torch==1.13.1+cu116 torchvision==0.14.1+cu116 torchaudio==0.13.1 -f https://download.pytorch.org/whl/torch_stable.html
  ```
- Install dassl library.

  ```
  # Instructions borrowed from https://github.com/KaiyangZhou/Dassl.pytorch#installation
  
  # Clone this repo
  git clone https://github.com/KaiyangZhou/Dassl.pytorch.git
  cd Dassl.pytorch/

  # Install dependencies
  pip install -r requirements.txt

  # Install this library (no need to re-build if the source code is modified)
  python setup.py develop
  cd ..
  ```
- Clone DCAR code repository and install requirements.
  ```
  # Clone DCAR code base
  git clone https://github.com/wyf202322/DCAR.git
  
  cd DCAR/
  
  # Install requirements
  pip install -r requirements.txt
  
  # Update setuptools package 
  pip install setuptools==59.5.0
  ```
