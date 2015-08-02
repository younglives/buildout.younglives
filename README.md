Installation
============

Add your private key
--------------------

Download your private key to ~/.ssh

```bash
chmod 700 ~/.ssh/id_rsa
```
Install and Configure GIT
-------------------------
```bash
sudo apt-get install git
```
```bash
git config --global user.email "me@here.com"
git config --global user.name "name in quotes"
```
Checkout the buildout
---------------------
```bash
mkdir -p ~/sites/young
cd ~/sites/young
git clone git@github.com:younglives/buildout.younglives.git ./
```
Setup the server
----------------
```bash
sudo apt-get install $(cat ubuntu_requirements)
```
Install Python
--------------
```bash
mkdir -p ~/Downloads
cd ~/Downloads
wget http://www.python.org/ftp/python/2.7.9/Python-2.7.9.tgz --no-check-certificate
tar zxfv Python-2.7.9.tgz
cd Python-2.7.9
./configure --prefix=$HOME/python/2.7.9
make
make install
cd ~/Downloads
wget https://pypi.python.org/packages/source/d/distribute/distribute-0.7.3.zip
unzip distribute-0.7.3.zip
cd distribute-0.7.3
~/python/2.7.9/bin/python setup.py install
~/python/2.7.9/bin/easy_install pip
~/python/2.7.9/bin/pip install virtualenv
```
Setup the buildout cache
------------------------
```bash
mkdir ~/.buildout
cd ~/.buildout
mkdir eggs
mkdir downloads
mkdir extends
echo "[buildout]
eggs-directory = /home/young/.buildout/eggs
download-cache = /home/young/.buildout/downloads
extends-cache = /home/young/.buildout/extends" > ~/.buildout/default.cfg
```
Create a virtualenv and run the buildout
----------------------------------------
```bash
cd ~/sites/young
~/python/2.7.9/bin/virtualenv ./
. bin/activate
pip install zc.buildout
pip install distribute
buildout init
buildout -c dev.cfg
```
