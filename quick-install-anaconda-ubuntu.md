# Quick install Anaconda on Ubuntu

- [Quick install Anaconda on Ubuntu](#quick-install-anaconda-on-ubuntu)
  * [Download Anaconda and install](#download-anaconda-and-install)
    + [Desactivate default base env](#desactivate-default-base-env)
  * [Using Anaconda navigator](#using-anaconda-navigator)
  * [Add desktop icons for Anaconda](#add-desktop-icons-for-anaconda)

* ubuntu 18.04.04 LTS
* Anaconda

## Download Anaconda and install

Go to the page https://www.anaconda.com/products/individual to get the latest version of Anaconda or pick installer directly from https://repo.anaconda.com/archive/

To install the last version on June 2020:

```sh
cd ~
mkdir anaconda_installer
cd anaconda_installer/

wget https://repo.anaconda.com/archive/Anaconda3-2020.02-Linux-x86_64.sh
chmod +x Anaconda3-2020.02-Linux-x86_64.sh
./Anaconda3-2020.02-Linux-x86_64.sh
```

### Desactivate default base env

Once all is installer conda will automaticly switch all your new terminals sessions on the env (base)

To prevent this behaviour execute

```sh
conda config --set auto_activate_base false
```

This will create/update your ~/.condarc file to prevent automaticly activating base env


## Using Anaconda navigator

To start working with anaconda you will need to launch Anaconde Navigator. You can do this with this command line

```sh
anaconda-navigator
```

## Add desktop icons for Anaconda

You may whant add an icon to your desktop in order to lauch the anaconda navigotor from your graphic insterface. To do it you'll need to create a **Anaconda.desktop** file in the **/usr/share/applications/** folder with the following content

```ini
[Desktop Entry]
Version=1.0
Type=Application
Name=Anaconda-Navigator
GenericName=Anaconda
Comment=Scientific Python Development Environment - Python3
Exec=bash -c 'export PATH="/home/your_home/anaconda3/bin:$PATH" && /home/your_home/anaconda3/bin/anaconda-navigator'
Categories=Development;Science;IDE;Qt;Education;
Icon=/home/your_home/anaconda3/lib/python3.7/site-packages/anaconda_navigator/static/images/anaconda-icon-256x256.png
Terminal=false
StartupNotify=true
MimeType=text/x-python;
```

Be aware of changing the /home/your_home by your home path.

Also check the version of python that is used for the Icon property. Path may be different if python3.8 were installled for instance. 

Adding the .desktop file to the **/usr/share/applications/** must be done with sudo.
