# Ubuntu EKS

Setting up a new ubuntu 20.04 install for developing with kubernetes on AWS.
Ubuntu image running in hyper-v for maximum containerization inception.

## Fixing Ubuntu Hyper-V conflicts
This was a fix for the weird double click behavior happening with 
mouse side buttons.  seems like when the button is physically pressed
2 events are interpreted: button down and button release.  The same 2
events are interpreted when the buttin is physically released.

Tried a few fixes proposed but the one that ended
 up working best is making it so that the horizontal scroll
 get mapped to forward and back 
```shell script
mouseId=`xinput list | grep -Po "xrdpMouse \K.*id=\K([0-9])"`
xinput set-button-map $mouseId 1 2 3 4 5 8 9 0 0
unset mouseId
```

## Installing common apps

```shell script
sudo apt-get install chromium-browser
# todo some automation around signing in to chrome would be cool

sudo apt install gnome-shell-extensions
sudo apt install gnome-tweak-tool

# todo track down commands to install the extensions:
#   caffeine

# sudo apt install chrome-gnome-shell this didn't work out right

sudo apt install jq gettext bash-completion
``` 

## Jetbrains product setup
```shell script
# JetBrains Toolbox
wget -cO jetbrains-toolbox.tar.gz "https://data.services.jetbrains.com/products/download?platform=linux&code=TBA"
tar -xzf jetbrains-toolbox.tar.gz
DIR=$(find . -maxdepth 1 -type d -name jetbrains-toolbox-\* -print | head -n1)
cd $DIR
./jetbrains-toolbox
cd ..
rm -r $DIR
rm jetbrains-toolbox.tar.gz

# todo look into a way to automate spinning this up and integrating with ide
#  maybe possible to download idea directly and then hook it into jetbrains toolbox after the fact
```

## Java

```shell script
sudo apt install curl
curl -sL https://github.com/shyiko/jabba/raw/master/install.sh | bash && . ~/.jabba/jabba.sh
jabba list
jabba ls
jabba --help
jabba ls-remote
jabba install openjdk@1.11.0
sudo update-alternatives --install /usr/bin/java java ${JAVA_HOME%*/}/bin/java 20000
```

## Kubernetes

```shell script
sudo apt-get update && sudo apt-get install -y apt-transport-https gnupg2
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubectl

# setup bash completion
kubectl completion bash >>  ~/.bash_completion
. /etc/profile.d/bash_completion.sh
. ~/.bash_completion
```

### helm
```shell script
# todo nail this down to a specific version probably
curl -sSL https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
helm repo add stable https://kubernetes-charts.storage.googleapis.com/
helm completion bash >> ~/.bash_completion
. /etc/profile.d/bash_completion.sh
. ~/.bash_completion
source <(helm completion bash)
```

### yq for yaml processing
todo maybe move this up into kub section
```shell script
echo 'yq() {
  docker run --rm -i -v "${PWD}":/workdir mikefarah/yq yq "$@"
}' | tee -a ~/.bashrc && source ~/.bashrc

```

# AWS

```shell script
# todo awscli??

```







# Section Template

```$bash

```