# Installing Keras Deep learning env

- [Installing Keras Deep learning env](#installing-keras-deep-learning-env)
  * [Creating specific conda env (optional)](#creating-specific-conda-env--optional-)
  * [Installing modules with conda](#installing-modules-with-conda)
  * [Installing modules with pip](#installing-modules-with-pip)

## Creating specific conda env (optional)

If you are using anaconda with conda package and env manager you can start by creating the dedicated environment.

```bash
# Creating new conda env with python 3.6
conda create -n deeplearning python=3.6 anaconda

# Activating the freshly created env
conda activate deeplearning
```

## Installing modules with conda

```bash
conda install theano
conda install tensorflow
conda install keras

# Update freshly installed modules
conda update --all
```

## Installing modules with pip

```bash
pip install theano
pip install tensorflow
pip install keras
```




