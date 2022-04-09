# dev-machine-bootstrapper
helping setting up new dev environments one shell at a time

## First Things First

### OSX specific
```shell
xcode-select --install
# install homebrew, see brew.sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```


### ZSH

set as default shell
```shell script
# os specific 
sudo apt-get install zsh || sudo dnf install zsh || sudo brew install zsh
chsh -s /bin/zsh
```
logout to take effect.

oh my zsh!
```shell script
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
Modify ~/.zshrc
```shell script
plugins=(git history sudo dotenv nvm sdk mvn)
ZSH_THEME="tonotdo"
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

## Python
```shell
# pyenv pre-requs, see https://github.com/pyenv/pyenv/wiki#suggested-build-environment

#brew install openssl readline sqlite3 xz zlib
#sudo apt-get update; sudo apt-get install make build-essential libssl-dev zlib1g-dev \
#  libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm \
#  libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev
dnf install make gcc zlib-devel bzip2 bzip2-devel readline-devel sqlite sqlite-devel openssl-devel tk-devel libffi-devel xz-devel

curl -L https://github.com/pyenv/pyenv-installer/raw/master/bin/pyenv-installer | bash
```

## Java
sdkman
```shell script
curl -s https://get.sdkman.io | bash
sdk install java 14.0.1.j9-adpt
sdk install groovy
sdk install maven
sdk install micronaut 2.0.0
```


# NPM
install nvm
```shell script
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
```
install latest node
```shell script
nvm install --lts
```
always want yarn
```shell script
npm install -g yarn
```