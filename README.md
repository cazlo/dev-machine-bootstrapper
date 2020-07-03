# dev-machine-bootstrapper
helping setting up new dev environments one shell at a time

## Installing common apps

```shell script
sudo apt-get install chromium-browser
# todo some automation around signing in to chrome would be cool

sudo apt-get install gnome-shell-extensions
sudo apt-get install gnome-tweak-tool

# todo track down commands to install the extensions:
#   caffeine

# sudo apt install chrome-gnome-shell this didn't work out right

sudo apt-get install jq gettext bash-completion curl wget docker docker-compose
``` 

### ZSH

set as default shell
```shell script
sudo apt-get install zsh
chsh -s /bin/zsh
```

oh my zsh!
```shell script
$ sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
Will want to take plugins, theme from the zsh example in this repo
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

## Java
sdkman
```shell script
curl -s https://get.sdkman.io | bash
sdk install java 14.0.1.j9-adpt
sdk install groovy
sdk install maven
sdk install micronaut 2.0.0
```

alterantive java version manager:
jabba
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