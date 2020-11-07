# Quick install Tensorflow GPU env

Example of conda install of tensorflox GPU. Using conda will install the correct version of CUDA and CuDNN compatible with the installed tensorflow version. Be aware that this will not update or install your Nvidia drivers, so you'll need to be up to date with your graphic card drivers

(procedure tested with Anaconda 3.6 on Windows 10)

```sh
# Creating new conda environment
conda create -n tensorflow-gpu python=3.7

# Activating environement
conda activate tensorflow-gpu

# Installing a IPython kernel
pip install ipykernel

# Configurating a IPython kernel
python -m ipykernel install --user --name tensorflow-gpu --display-name "tensorflow-gpu"

# Installing tensorflox
conda install tensorflow-gpu

# Installing Keras (2.3.0) to be compatible with Tensorflow 2.1
pip install keras==2.3.0

# Force to reinstall tensorflow estimator
pip install tensorflow-estimator==2.1.*

# Install mat plot lib and its env
pip install msvc-runtime
pip install matplotlib

# Install pandas (Optionnal)
conda install pandas

# Install jupyter (Optionnal)
conda install jupyter
```

## Install GPU calculation with pytorch

```python
# If you have not yet installed tensorflow-gpu
conda install cudatoolkit=10.2 -c pytorch

# Install pytorch stand alors from official pytorch channel
conda install pytorch -c pytorch
```


## Quick test if GPU calculation is available

### Test GPU available with tensorflow

```python
import tensorflow as tf

if tf.test.gpu_device_name():
    print('GPU calculation available')
    print(tf.test.gpu_device_name())
else:
    print('No GPU found')
```

### Test GPU available with pytorch

```python
import torch

if torch.cuda.is_available():
    print('GPU calculation available')
    print(torch.cuda.get_device_name(0))
else:
    print('No GPU found')
```

Some usefull python functions to check GPU devices

```python
# Should retur device number (0)
current_device = torch.cuda.current_device()

# Should return something like <torch.cuda.device at 0x000000000000>
torch.cuda.device(current_device)

# Should return the total count of cuda devices
torch.cuda.device_count()

# Should return the GPU name, exemple: 'GeForce GTX 1060'
device_name = torch.cuda.get_device_name(current_device)

# Should return True if device is available
torch.cuda.is_available()
```
