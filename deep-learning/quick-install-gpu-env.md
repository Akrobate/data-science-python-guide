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