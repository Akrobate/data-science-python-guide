# Installing GPU env within docker container

Procedure tested on ubuntu 18.04 with a NVIDIA GTX 1060 6go

## Installing Nvidia GPU drivers on host machine

```bash
# Add ppa
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt update

# Check list of compatible drivers
ubuntu-drivers devices

# Install the driver
sudo apt install nvidia-driver-(driverversion)

# In my case with a GTX 1060 command is
# sudo apt install nvidia-driver-455

# Check status
nvidia-smi

# (Tip) Real time monitor status command
watch -n0.1 nvidia-smi
```

## Installing docker on host machine

```bash
sudo apt update

# Usefull dependencies for docker
sudo apt install apt-transport-https ca-certificates curl software-properties-common

# Adding GPG key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

# Add repository
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"

sudo apt update

# Install docker CE
sudo apt install docker-ce

# (optionnal) Check docker status
sudo systemctl status docker
```

### Execute docker without sudo (optionnal)

Just add your current user to docker group, then disconnect / reconnect
```bash
sudo usermod -aG docker ${USER}

# Check user was added to group
id -nG
```